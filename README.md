# jupyterlab docker image

<p align="center">
    <em>Jupyterlab Docker Image with my personal preferences (perhaps with yours too)</em>
</p>

<p align="center">
<a href="https://github.com/iancleary/jupyterlab/actions/workflows/publish.yml" target="_blank">
    <img src="https://github.com/iancleary/jupyterlab/actions/workflows/publish.yml/badge.svg" alt="Publish">
</a>
</p>

Images are built and pushed to DockerHub and GitHub container registery automatically on releases.

## Custom Preferences in Jupyterlab

I installed ohmyzsh, along with powerlevel10k, and the MesloLGS NF fonts.

### Jupyterlab Settings Preferences

<https://stackoverflow.com/a/70485739>

Using overrides.json is the current recommended approach:

<https://jupyterlab.readthedocs.io/en/stable/user/directories.html#overridesjson>

In short: check the application directory with jupyter lab path and place a file named overrides.json containing

```json
{
    "@jupyterlab/apputils-extension:themes": {
        "theme": "JupyterLab Dark"
    },
    "@jupyterlab/terminal-extension": {
        "fontFamily": "MesloLGS NF"
    }
}
```

into {application directory}/settings/ (e.g. /opt/conda/share/jupyter/lab/settings/ for the official jupyter docker containers)

So if you want to have the base image from jupyter with dark theme, the Dockerfile would be something like:

```Dockerfile
FROM jupyter/base-notebook

COPY overrides.json /opt/conda/share/jupyter/lab/settings/
```
