FROM debian:jessie
LABEL description="Git Server – SSH Protocol"

RUN apt-get update && apt-get install -y \
    git \
    openssh-server

# Add 'git' user with restricted shell
RUN adduser --shell /usr/bin/git-shell --quiet git

# Expose files/folders created by the container


VOLUME ["/kyes"]

EXPOSE 22

CMD ["/usr/sbin/sshd"]
