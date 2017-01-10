# Preconditions for creating Infrastructure using Stakater

1. STACK_NAME should contain letters and `_` or `-` only. (No spaces)
2. Names of modules/apps etc should contain alphanumeric characters, ‘-’ or ‘_’ only. (No spaces)
3. During AMI-Blue Green deployment, the variable `ENV_STATE_KEY` refers to the terraform state key of the environment (e.g. prod) (which includes network, buckets etc) in which the deployment resources are to be created. Where as, the `DEPLOY_STATE_KEY` refers to the terraform state key file that will be created and will hold the deployment resources (Blue-green group resources i.e. autoscaling groups, elbs etc)
4. In `prod-deployment-reference` ELB Names for active and test ELB should be like `APP_NAME-ENVIRONMENT-elb-active` and `APP_NAME-ENVIRONMENT-elb-test` respectively. 
5. Add your house-keeping config repository link in house-keeper-user-data.yaml file
