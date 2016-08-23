# Git Service Under Various Protocols
_using Docker technology_

This project demonstrates containerization practices on a subject of version control. Each of inspected Dockerfiles focuses on configuration of a runtime environment for bare repositories' distribution via specified data transfer protocol.

__Currently supported solutions are:__
- Git protocol
- SSH protocol

When built and run user is left with a container (an application) that serves user's provided Git repositories either to read-only public access or read-write access for contributors.

![Alt text](Resources/git.png)

## Run
### Git Protocol

To simply share your work with others on trusted network run the following command.
```bash
docker run -dP -v /PATH:/srv/git/public IMAGE
```

##### Clean up
```bash
docker-compose rm -v
```

### SSH Protocol

To let others contribute to your work add their public keys to a single file you'll later mount to the container.
```bash
docker run -d -p NUMBER:22 -v /PATH:/home/git/.ssh/authorized_keys -v /PATH:/srv/git/private felicio/ssh
```

## Clone
### Git Protocol
```bash
git clone git://HOST:PORT/PATH
```


### SSH Protocol
```bash
git clone ssh://git@HOST:PORT/PATH
```
