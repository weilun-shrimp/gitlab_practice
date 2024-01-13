Reference: [GitLab CI 實作記錄(1) - 使用 Docker 在同台主機運行 GitLab 與 GitLab-Runner](https://eandev.com/post/devops/gitlab-and-runner-on-same-host-using-docker/)

# <span style="color:red">Attension!!</span><br>

Due to docker.sock issue. If you are running WSL on windows, you can't not install gitlab runner from scratch. You must run runner from officail image.

# <span style="color:red">Must to do!!</span><br>

add host、gitlab_container、gitlab_runner_container hosts file gitlab container DNS value.

# Docker

## Run

```bash
docker run -itd -p host_port:container_port --name gitlab_container_name -v project_path/config:/etc/gitlab -v project_path/logs:/var/log/gitlab -v project_path/data:/var/opt/gitlab gitlab/gitlab-ee:latest

docker run -itd --name gitlab_runner_container_name -v project_path/runner-docker.sock/docker.sock:/var/run/docker.sock -v project_path/runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest
```

# Init root credential

username: root

Password path: /etc/gitlab/initial_root_password

# Matenence commands

If you change any value of /etc/gitlab/gitlab.rb

```bash
gitlab-ctl reconfigure
```

start and stop and check status

```bash
gitlab-ctl start
gitlab-ctl stop
gitlab-ctl status
```

# GitLab Runner for CICD

[Manually install on GNU/Linux](https://docs.gitlab.com/runner/install/linux-manually.html)<br>
[Using the official GitLab repositories to install](https://docs.gitlab.com/runner/install/linux-repository.html)<br>
[Manage](https://docs.gitlab.com/ee/ci/runners/runners_scope.html#create-a-project-runner-with-a-runner-authentication-token)<br>
[Registering](https://docs.gitlab.com/runner/register/index.html)

Runner authentication token path: /etc/gitlab-runner/config.toml
