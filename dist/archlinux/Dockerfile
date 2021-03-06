FROM archimg/base-devel:latest
MAINTAINER Patrik Nilsson <asavartzeth@gmail.com>

# Setup build user/group
RUN useradd \
      --create-home \
      --uid '2000' \
      --shell /usr/bin/false 'travis'

# Compliment archimg/base-devel build environment
RUN pacman -Syu \
      --noconfirm \
      --needed \
      --noprogressbar \
      --verbose \
        git \
        meson && \
    # Clean .pacnew files
    find / -name "*.pacnew" -exec rename .pacnew '' '{}' \; && \
    # Clean package cache
    yes | pacman -Scc

USER travis

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/bin/core_perl

# Copy sudoers file
COPY contrib/etc/sudoers.d/travis /etc/sudoers.d/travis

# Add arch-travis script
COPY init.sh /usr/bin/arch-travis

# Simplify Travis CI caching
VOLUME ["/var/cache/pacman/pkg"]

ENTRYPOINT ["/usr/bin/arch-travis"]
