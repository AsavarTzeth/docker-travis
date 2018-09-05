FROM ubuntu:bionic
MAINTAINER Patrik Nilsson <asavartzeth@gmail.com>

# Setup build user/group
RUN useradd \
      --create-home \
      --uid '2000' \
      --shell /usr/bin/false 'travis'

# Compliment archimg/base-devel build environment
RUN apt-get update && \
    apt-get --assume-yes upgrade && \
    apt-get install --no-install-recommends git meson && \
    apt-get clean

USER travis

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/bin/core_perl

# Copy sudoers file
COPY files/etc/sudoers.d/travis /etc/sudoers.d/travis

# Add travis integration script
#COPY init.sh /usr/bin/travis-init

# Simplify Travis CI caching
VOLUME ["/var/cache/apt/archive"]

#ENTRYPOINT ["/usr/bin/travis-init"]
