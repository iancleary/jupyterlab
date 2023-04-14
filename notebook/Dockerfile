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
    # font for powerline10k
    fontconfig \
    # Terminal Customization
    zsh && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Create alternative for nano -> nano-tiny
RUN update-alternatives --install /usr/bin/nano nano /bin/nano-tiny 10

# Switch back to jovyan to avoid accidental container runs as root
USER ${NB_UID}


## Fix up permissions
USER root
RUN fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Custom CSS, Themes, Fonts
RUN mkdir -p "/home/${NB_USER}/.jupyter/custom/"
COPY custom/custom.css  "/home/${NB_USER}/.jupyter/custom/custom.css"


## Oh My ZSH and Powerlevel10k
## See https://github.com/iancleary/ansible-role-ohmyzsh
USER $NB_USER
# run the installation script
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true && \
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.oh-my-zsh/custom/themes/powerlevel10k && \
    git clone --depth=1 https://github.com/zdharma-continuum/fast-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/fast-syntax-highlighting && \
    git clone --depth=1 https://github.com/zsh-users/zsh-autosuggestions.git ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions && \
    mkdir -p ~/.local/share/fonts/ && \
    cd ~/.local/share/fonts/ && \
    wget -O 'MesloLGS NF Regular.ttf' https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf && \
    wget -O 'MesloLGS NF Bold.ttf' https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf && \
    wget -O 'MesloLGS NF Italic.ttf' https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf && \
    wget -O 'MesloLGS NF Bold Italic.ttf' https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf && \
    fc-cache -f -v

COPY custom/.zshrc custom/.zshrc_aliases custom/.p10k.zsh /home/${NB_USER}/
COPY custom/overrides.json /opt/conda/share/jupyter/lab/settings/

USER root

RUN fix-permissions "/home/${NB_USER}/.local/share/fonts" && \
    fix-permissions "/home/${NB_USER}/.zshrc" && \
    fix-permissions "/home/${NB_USER}/.zshrc_aliases" && \
    fix-permissions "/home/${NB_USER}/.p10k.zsh" && \
    fix-permissions "/opt/conda/share/jupyter/lab/settings/overrides.json" && \
    mkdir -p "/home/${NB_USER}/.jupyter/lab/user-settings/" && \
    fix-permissions "/home/${NB_USER}/.jupyter/lab/user-settings/" && \
    mkdir -p "/home/${NB_USER}/.jupyter/lab/workspaces/" && \
    fix-permissions "/home/${NB_USER}/.jupyter/lab/workspaces/"

USER ${NB_UID}

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
# RUN unset NODE_OPTIONS


# set default shell
ENV SHELL=/usr/bin/zsh

###
# ensure image runs as unpriveleged user by default.
###
USER ${NB_UID}
