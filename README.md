## Web UI

> Wait at least 7min before trying to access the web UI.

User `root` and get password with:
```shell
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

## Runner

In order to register gitlab runner:
- got to http://localhost/admin/runners
- new instance runner -> check `Run untagged jobs` -> create runner
- run the command below

```shell
docker exec -it gitlab-runner \
gitlab-runner register \
    --non-interactive \
    --executor "docker" \
    --docker-image "alpine:latest" \
    --url "http://gitlab" \
    --token "<token>" \
    --docker-network-mode "<GITLAB-SERVICE-NAME>_<NETWORK-NAME>"  # docker inspect gitlab-runner | grep -in network

# other helpful commands
docker exec gitlab-runner gitlab-runner run
docker exec gitlab-runner gitlab-runner --help
```
