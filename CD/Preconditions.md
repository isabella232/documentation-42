# Preconditions for CD (GoCD)

1. App_name should contain letters and `_` or `-` only. (No spaces)
2. App_name in GoCD `cruise-config` should match the docker-compose file’s mappings in `app` service
3. Value for `Environment` build pipelines should be one of `dev`, `test`, or `prod`
4. Value for `CLUSTER_ENV` in cluster deployment pipelines should be one of `dev` or `qa`

