FROM jupyter/scipy-notebook:latest

# Add RUN statements to install packages as the $NB_USER defined in the base images.

# Add a "USER root" statement followed by RUN statements to install system packages using apt-get,
# change file permissions, etc.

# If you do switch to root, always be sure to add a "USER $NB_USER" command at the end of the
# file to ensure the image runs as a unprivileged user by default.

USER root
RUN apt-get update -y
RUN apt-get upgrade -y
USER $NB_USER

## ZSH Shell
USER root
RUN apt install -y zsh

## Oh My ZSH
# set the zsh theme
USER $NB_USER
ENV ZSH_THEME robbyrussell
# run the installation script
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

## Pip and Python Packages
RUN pip install --upgrade pip

## Jupyterlab
RUN pip install jupyterlab "ipywidgets>=7.5"
RUN jupyter nbextension enable --py widgetsnbextension

# Extensions for jupyterlab
# Avoid "JavaScript heap out of memory" errors during extension installation
# (OS X/Linux)
RUN export NODE_OPTIONS=--max-old-space-size=4096

# Jupyter widgets extension
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager

# Unset NODE_OPTIONS environment variable
# (OS X/Linux)
RUN unset NODE_OPTIONS

# Custom CSS
RUN mkdir -p /home/jovyan/.jupyter/custom/
COPY custom/custom.css  /home/jovyan/.jupyter/custom/custom.css

# set default shell
ENV SHELL=/usr/bin/zsh

###
# ensure image runs as unpriveleged user by default.
###
USER $NB_USER
