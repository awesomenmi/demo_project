# demo_project
sudo systemctl start docker
sudo docker-compose up -d
sudo docker exec -it gitlab gitlab-rake "gitlab:password:reset[root]"

Создать проект
закоммитить в проект

Create the Docker volume:

docker volume create gitlab-runner-config

Start the GitLab Runner container using the volume we just created:

docker run -d --name gitlab-runner --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v gitlab-runner-config:/etc/gitlab-runner \
    gitlab/gitlab-runner:latest

docker compose up -d

Project -> CI/CD Settings -> Runners


[lumi@fhmtps91ba79aa5re88e ~]$ sudo docker exec -it gitlab-runner gitlab-runner register
Runtime platform                                    arch=amd64 os=linux pid=30 revision=656c1943 version=16.9.0
Running in system-mode.

Enter the GitLab instance URL (for example, https://gitlab.com/):
http://x.x.x.x:8080/
Enter the registration token:
GR1348941LZqbxjfZGfX3xA6vtR_y
Enter a description for the runner:
[a5e5fd00c7c7]: docker
Enter tags for the runner (comma-separated):
runner
Enter optional maintenance note for the runner:

WARNING: Support for registration tokens and runner parameters in the 'register' command has been deprecated in GitLab Runner 15.6 and will be replaced with support for authentication tokens. For more information, see https://docs.gitlab.com/ee/ci/runners/new_creation_workflow
Registering runner... succeeded                     runner=GR1348941LZqbxjfZ
Enter an executor: custom, docker, docker-windows, docker+machine, docker-autoscaler, instance, shell, ssh, parallels, virtualbox, kubernetes:
docker
Enter the default Docker image (for example, ruby:2.7):
docker:dind
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!

Configuration (with the authentication token) was saved in "/etc/gitlab-runner/config.toml"

Edit runner -> Indicates whether this runner can pick jobs without tags

troubleshooting

Getting source from Git repository
00:00
Fetching changes with git depth set to 20...
Reinitialized existing Git repository in /builds/project-1/.git/
fatal: 'mygitlab/root/my_project.git' does not appear to be a git repository
fatal: Could not read from remote repository.
Please make sure you have the correct access rights
and the repository exists.
ERROR: Job failed: exit code 1

Admin Area -> Settings -> General -> Custom Git clone URL for HTTP(S)
http://x.x.x.x:8080

$ docker login -u $REGISTRY_USER -p $REGISTRY_PASS
WARNING! Using --password via the CLI is insecure. Use --password-stdin.
error during connect: Post "http://docker:2375/v1.24/auth": dial tcp: lookup docker on 10.128.0.2:53: no such host

/etc/gitlab-runner/config.toml


