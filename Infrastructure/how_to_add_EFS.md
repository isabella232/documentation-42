# How to add EFS

To add EFS you need to use this module https://github.com/stakater/blueprint-storage-aws/tree/master/modules/efs

You also need to add two units to your instance's .yaml file.

```
    - name: data.mount
      content: |
        [Mount]
        What=EFS_DNS:/
        Where=/data
        Type=nfs
    - name: runcmd.service
      command: start
      content: |
        [Unit]
        Description=command
        [Service]
        RemainAfterExit=true
        Type=oneshot
        Environment="EFS_DNS=${efs_dns}"
        ExecStart=/bin/sh -c "AZ_ZONE=$(curl -s -L http://169.254.169.254/latest/meta-data/placement/availability-zone); \
                              sed -i \"s/EFS_DNS/$AZ_ZONE.$EFS_DNS/\" /etc/systemd/system/data.mount; \
                              systemctl daemon-reload; \
                              systemctl restart data.mount"
    # 1- Append current availability-zone to EFS_DNS Substring
    # 2- Replace EFS_DNS with the resulting value in systemd file
    # 3- Restart the systemd unit
```
These units require a variable named efs_dns so make sure you pass it to your yaml template file like this
```
data "template_file" "my-instance-user-data" {
  template = "${file("./user-data/my-instance.yaml")}"

  vars {
    efs_dns = "${replace(element(split(",", module.efs-mount-targets.dns-names), 0), "/^(.+?)\\./", "")}"
  }
}
```

Also if there are any other units that need to run after EFS has been mounted properly then add the following two dependencies to their units files. 
*Donot change the order of dependencies*
```
Requires=runcmd.service
After=runcmd.service
```
