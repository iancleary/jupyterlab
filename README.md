# Dockerfiles

<p align="center">
    <em>Dockerfiles to build images useful to me (and maybe others)</em>
</p>

<p align="center">
<a href="https://github.com/iancleary/dockerfiles/actions?query=workflow%3APublish" target="_blank">
    <img src="https://github.com/iancleary/dockerfiles/workflows/Publish/badge.svg" alt="Publish">
</a>
</p>

Images are built and pushed to DockerHub automatically on push to master branch.

Feel free to grab anything you want.

| Directory   |      Image      |  Description |
|----------|:-------------:|:------:|
| [notebook](notebook)  |  [iancleary/notebook](https://hub.docker.com/repository/docker/iancleary/notebook) | Jupyter Notebook with ZSH and Custom CSS |

## Calendar Versioning

This project adheres to [Calendar Versioning](https://calver.org/), YYYY.MINOR.MICRO.

## Attributions

The Basic Idea

This is a template module collecting many utilities I have liked from other projects, to serve as a personal reference.

- [https://github.com/dawidd6/docker](https://github.com/dawidd6/docker) for the GitHub Action and Repo Structure
- [https://github.com/jessfraz/dockerfiles](https://github.com/jessfraz/dockerfiles) as a reference for bindings for various applications

## Custom Preferences in Jupyterlab


### Jupyterlab Settings Preferences

<https://stackoverflow.com/a/70485739>

Using overrides.json is the current recommended approach:

<https://jupyterlab.readthedocs.io/en/stable/user/directories.html#overridesjson>

In short: check the application directory with jupyter lab path and place a file named overrides.json containing

```json
{
    "@jupyterlab/apputils-extension:themes": {
        "theme": "JupyterLab Dark"
    }
}
```

into <application directory>/settings/ (e.g. /opt/conda/share/jupyter/lab/settings/ for the official jupyter docker containers)

So if you want to have the base image from jupyter with dark theme, the Dockerfile would be

```Dockerfile
FROM jupyter/base-notebook

COPY overrides.json /opt/conda/share/jupyter/lab/settings/
```
