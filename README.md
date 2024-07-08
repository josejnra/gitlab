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
    --url "http://gitlab" \
    --token "<token>" \
    --docker-image "alpine:latest" \
    --docker-network-mode "<GITLAB-SERVICE-NAME>_<NETWORK-NAME>"  # docker inspect gitlab-runner | grep -in network

# other helpful commands
docker exec gitlab-runner gitlab-runner run
docker exec gitlab-runner gitlab-runner --help
```

## Some Links
- [Connect CI Runner to Docker network](https://gitlab.com/gitlab-org/gitlab-runner/-/issues/1846)
- [Gitlab runner with dind](https://gitlab.com/TyIsI/gitlab-runner-docker-compose/-/blob/main/docker-compose.yml?ref_type=heads)
- [Gitlab runner with dind 2](https://gist.github.com/benoitpetit/cbe19cdd369ec8c1e0defd245d91751f)
