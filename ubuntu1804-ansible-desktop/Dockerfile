FROM geerlingguy/docker-ubuntu1804-ansible:latest
# https://github.com/geerlingguy/docker-ubuntu1804-ansible/blob/master/Dockerfile

LABEL maintainer="Ian Cleary"

# Setup enviroment variables
ENV DEBIAN_FRONTEND noninteractive

# Install dependencies.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       git \
       make \
       gnome-shell \
       gnome-session \
       gnome-terminal \
       dconf-gsettings-backend \
       dconf-editor \
       dconf-cli \
       gsettings-desktop-schemas \
    && rm -Rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean
