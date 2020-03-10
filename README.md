# Hoster

A simple "etc/hosts" file injection tool to resolve names of local Docker containers on the host.

hoster is intended to run in a Docker container:

    docker run --restart=unless-stopped -d \
        -v /var/run/docker.sock:/tmp/docker.sock \
        -v /etc/hosts:/tmp/hosts \
        thisisdevelopment/docker-hoster

The `docker.sock` is mounted to allow hoster to listen for Docker events and automatically register containers IP.

Hoster inserts into the host's `/etc/hosts` file an entry per running container and keeps the file updated with any started/stoped container.

## Container Registration

Hoster provides by default the entries 
- `<hostname>.<domainname>`
- `<service>.<project>.services.docker`
- `<container name>.containers.docker` (if no service/project name are found)
- `<container id>` for each container and the aliases for each network. Containers are automatically registered when they start, and removed when they die.

## Original code from

https://github.com/dvddarias/docker-hoster
