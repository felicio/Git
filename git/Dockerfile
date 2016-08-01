FROM debian:jessie
LABEL description="Git Server, Git Protocol"

RUN apt-get update && apt-get install -y \
    git

# Create non-login (and consider a system) 'git' user
RUN adduser --disabled-password --no-create-home --gecos "" git

# Create user (and its group) with read-only acces to folder of repositories
RUN adduser --disabled-password --no-create-home --gecos "" git-ro

# Create folder for storing repositories
WORKDIR /srv/git/data
# Seems like it's not allowed to set group ID bit
#RUN chown git:git-ro . && chmod 750 . && chmod g+s .
RUN chown git:git-ro . && chmod 755 .

# Add starting point repository
#RUN ...

# Expose files/folders created by the container
# Mount point holding external volumes from native host or other containers
VOLUME ["/srv/git"]

# The same counts for a firewall, if set up
EXPOSE 9418

# Run docker daemon as user with 'data' read-only permission
#USER git-ro

# Allow server to restart without waiting for old connnections to time out
CMD ["git", "daemon", "--reuseaddr", "--base-path=/srv/git/data", "/srv/git/data"]
# In need of shell expansion
#CMD ["sh", "-c", command]
