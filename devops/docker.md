# Docker

## Common commands

Use new management commands:

docker <command> <sub-command> (options)

old way:

docker <command> (options)

Both work.

`docker container ls -a`
Lists all contains

`docker images`
Lists all images

`docker container run -it` (`docker container run -it sh` to use the terminal)
Start a new container interactively

`docker container exec -it`
Run additional command in existing container

Containers
Use `docker container my_command`
`create` — Create a container from an image.
`start` — Start an existing container.
`run` — Create a new container and start it.
`ls` — List running containers.
`inspect` — See lots of info about a container.
`logs` — Print logs.
`stop` — Gracefully stop running container.
`kill` —Stop main process in container abruptly.
`rm` — Delete a stopped container.

Images
Use `docker image my_command`
`build` — Build an image.
`push` — Push an image to a remote registry.
`ls` — List images.
`history` — See intermediate image info.
`inspect` — See lots of info about an image, including the layers.
`rm` — Delete an image.

`docker system prune` — Delete all unused containers, unused networks, and dangling images.

## Networking

Each container connected to a private virtual network "bridge"

Each virtual network routes through NAT firewall on host IP

All containers on a virtual network can talk to each other without -p

Best practice is to create a new virtual network for each app:
network "my_web_app" for mysql and nginx containers
network "my_api" for mongo and nodejs containers

`docker network ls`
Show networks

`docker network inspect`
Inspect a network

`docker network create --driver`
Create a network

`docker network connect`
Attach a network to container

`docker network disconnect`
Detach a network from container

## Lifetime & persistent data - volumes

Containers are usually immutable and ephemeral. Sometimes we want data to persist, there are two ways we can achieve this:

Data volumes
Use `VOLUME` in Dockerfile
Add `VOLUME /var/some/locatin` to add files. These files will outlive the container
Volumes need manual deletion
Use `docker volume prune` for cleanup

Bind mounts
Maps a host file or directory to a container file or directory
Binds must be used via CLI commands
`docker container run -d --name psql -v psql:var/lib/postgresql/data postgres:9.6.1`
`psql(host directory):var/lib/postgresql/data(image directory, can find on docker hub)`

## Dockerfile for nodejs

## Docker Compose for development
