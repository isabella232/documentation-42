To create User roles, first save all your users and their hashed passwords in the GOCD's password file. It is located at /gocd-data/gocd-passwd/passwd in the container
The default format to add a user is <username>:{SHA}<password-hash> (one user per line)

Beginners can use this link to https://docs.go.cd/16.5.0/configuration/dev_authentication.html to do this from goCD GUI.

Advance users can do all this from the cruise-config file.

This snippet tells the location of passwd file and creates three roles test,developer and supervisor and assign roles to different users.
There is a special user-group of admin who have access to everything.

<security>
      <passwordFile path="/gocd-passwd/passwd" />
      <roles>
        <role name="test" />
        <role name="developer">
          <users>
            <user>developer</user>
            <user>developer1</user>
          </users>
        </role>
        <role name="supervisor">
          <users>
            <user>supervisor</user>
            <user>supervisor1</user>
          </users>
        </role>
      </roles>
      <admins>
        <user>admin</user>
	<user>supervisor1</user>
      </admins>
</security>

Next to control access to a certain pipeline group e.g Dev you can add an authorization tag. The authorization tag can have 3 sub-tags which decided the level of access allowed
1-view -> only allowed to view pipelines
2-operate -> allowed to run and stop pipelines
3-admin -> can update config of pipelines

Each of these 3 tags can have the following two types of tags and multiple tags are allowed:
1- role -> which roles have the specified level of access
2- user -> which users have the specified level of access

Make sure if you want to allow a user to operate a pipeline group then you also give him permission to view it

The following code snippet adds authorization so that all developers and supervisors can view the pipelines and a user with name developer and all supervisors can operate the pipeline

<pipelines group="Dev">
    <authorization>
      <view>
        <role>developer</role>
        <role>supervisor</role>
      </view>
      <operate>
        <user>developer</user>
        <role>supervisor</role>
      </operate>
    </authorization>
    <pipeline name="app-build-dev" isLocked="false" template="stakater_build">
      ....
    </pipeline>
    <pipeline name="app-deploy-dev" template="stakater_deploy_cluster">
      ....
    </pipeline>
</pipelines

References:
https://docs.go.cd/16.5.0/configuration/dev_authentication.html
