FROM debian:jessie
LABEL description="Git Server – Git Protocol"

RUN apt-get update && apt-get install --no-install-recommends -q=2 \
    git

# Create an user with read-only permissions to public directory, which will also run the daemon.
# And another one that will optionally serve as login account for SSH connections.
RUN adduser --system --group --no-create-home --quiet git-ro
RUN adduser --disabled-password --shell /usr/bin/git-shell --quiet git

# Enable interactive git shell with preconfigured set of commands.
COPY ["etc/git-shell-commands/", "/home/git/git-shell-commands"]

# Create folders for storing repositories
WORKDIR /srv/git

# Define access permissions and SETGID.
RUN mkdir -m 2750 public private
RUN chown git:git-ro public && chown git:git private

# Expose a mountpoint to hold external content from native host, data stores or other containers.
VOLUME ["/srv/git/public"]

# Keep in mind a firewall's restrictions.
EXPOSE 9418

USER git-ro

# Allow server to restart without waiting for old connnections to time out.
CMD ["git", "daemon", "--reuseaddr", "--base-path=/srv/git/public", "/srv/git/public", "--base-path-relaxed"]
