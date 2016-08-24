# Git Service Under Various Protocols
_using Docker technology_

[![Build Status](https://travis-ci.org/felicio/Git.svg?branch=master)](https://travis-ci.org/felicio/Git)

This project demonstrates containerization practices on a subject of version control. Each of inspected Dockerfiles focuses on configuration of a runtime environment for bare repositories' distribution via specified data transfer protocol.

__Currently supported solutions are:__
- [x] Git protocol
- [x] SSH protocol
- [ ] HTTP protocol
- [ ] HTTPS protocol

When built and run user is left with a container (an application) that serves user's provided Git repositories either to read-only public access or read-write access for contributors.

![Project's diagram](https://github.com/felicio/Git/blob/master/Resources/git.png)

## Build, Run
### Docker Engine
#### Git Protocol

To simply share your work with others on trusted network run the following command.
```bash
docker build -t IMAGE PATH/git
docker run -dP -v PATH/Resources/srv:/srv/git/public --name CONTAINER IMAGE
```

#### SSH Protocol

To let others contribute to your work add their public keys to a single file you'll later mount to the container.
```bash
docker build -t IMAGE -f PATH/ssh
docker run -dP -v PATH/Resources/authorized_keys:/home/git/.ssh/authorized_keys -v PATH/Resources/srv:/srv/git/private --name CONTAINER IMAGE
```

### Docker Compose

```bash
docker-compose up -d
```

## Clone
_from a running container_

```bash
git clone git://HOST:PORT/PATH
git clone ssh://git@HOST:PORT/PATH
```

## Clean Up
```bash
# Docker Engine
docker stop CONTAINER
docker rm -v CONTAINER
docker rmi IMAGE

# Docker Compose
docker-compose down -v --rmi all
```
