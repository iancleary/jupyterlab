FROM docker.io/jupyter/base-notebook:latest

USER root

# Install all OS dependencies for fully functional notebook server
RUN apt-get update --yes && \
    apt-get upgrade --yes && \
    apt-get install --yes --no-install-recommends \
    # - apt-get upgrade is run to patch known vulnerabilities in apt-get packages as
    #   the ubuntu base image is rebuilt too seldom sometimes (less than once a month)
    # Common useful utilities
    git \
    nano-tiny \
    tzdata \
    unzip \
    vim-tiny \
    # git-over-ssh
    openssh-client \
    # less is needed to run help in R
    # see: https://github.com/jupyter/docker-stacks/issues/1588
    less \
    # # nbconvert dependencies
    # # https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex
    # texlive-xetex \
    # texlive-fonts-recommended \
    # texlive-plain-generic \
    # Enable clipboard on Linux host systems
    xclip \
    # Terminal Customization
    zsh && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Create alternative for nano -> nano-tiny
RUN update-alternatives --install /usr/bin/nano nano /bin/nano-tiny 10

# Switch back to jovyan to avoid accidental container runs as root
USER ${NB_UID}

# Add R mimetype option to specify how the plot returns from R to the browser
# COPY --chown=${NB_UID}:${NB_GID} Rprofile.site /opt/conda/lib/R/etc/

# Add RUN statements to install packages as the $NB_USER defined in the base images.

# Add a "USER root" statement followed by RUN statements to install system packages using apt-get,
# change file permissions, etc.

# If you do switch to root, always be sure to add a "USER $NB_USER" command at the end of the
# file to ensure the image runs as a unprivileged user by default.

## Fix up permissions
USER root
RUN fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Custom CSS
RUN mkdir -p "/home/${NB_USER}/.jupyter/custom/"
COPY custom/custom.css  "/home/${NB_USER}/.jupyter/custom/custom.css"


## Oh My ZSH
# set the zsh theme
USER $NB_USER
ENV ZSH_THEME robbyrussell
# run the installation script
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

## Pip and Python Packages
RUN pip install --upgrade pip

# ## Jupyterlab
# RUN pip install jupyterlab "ipywidgets>=7.5"
# RUN jupyter nbextension enable --py widgetsnbextension

# # Extensions for jupyterlab
# # Avoid "JavaScript heap out of memory" errors during extension installation
# # (OS X/Linux)
# RUN export NODE_OPTIONS=--max-old-space-size=4096

# # Jupyter widgets extension
# RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager

# Unset NODE_OPTIONS environment variable
# (OS X/Linux)
RUN unset NODE_OPTIONS


# set default shell
ENV SHELL=/usr/bin/zsh

###
# ensure image runs as unpriveleged user by default.
###
USER ${NB_UID}
