# Preconditions for CD (GoCD)

1. App_name should contain letters and `_` or `-` only. (No spaces)
2. App_name in GoCD `cruise-config` should match the docker-compose file’s mappings in `app` service
3. Value for `Environment` build pipelines should be one of `dev`, `test`, or `prod`
4. Value for `CLUSTER_ENV` in cluster deployment pipelines should be one of `dev` or `qa`
5. During AMI-Blue Green deployment, the variable `ENV_STATE_KEY` refers to the terraform state key of the environment (e.g. prod) (which includes network, buckets etc) in which the deployment resources are to be created. Where as, the `DEPLOY_STATE_KEY` refers to the terraform state key file that will be created and will hold the deployment resources (Blue-green group resources i.e. autoscaling groups, elbs etc)
