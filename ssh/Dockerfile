FROM debian:jessie
LABEL description="Git Server, SSH Protocol"

RUN apt-get update && apt-get install -y \
    git \
    openssh-server

# Add 'git' user with restricted shell
RUN adduser --shell /usr/bin/git-shell --quiet git

VOLUME ["/kyes"]

EXPOSE 22

CMD ["/usr/sbin/sshd"]
