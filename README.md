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
| [ubuntu1804-ansible-desktop](ubuntu1804-ansible-desktop)  |  [iancleary/ubuntu1804-ansible-desktop](https://hub.docker.com/repository/docker/iancleary/ubuntu1804-ansible-desktop) | Dockerfile for [iancleary/ansible-desktop](https://github.com/iancleary/ansible-desktop) CI Testing|
| [ubuntu2004-ansible-desktop](ubuntu2004-ansible-desktop)  |  [iancleary/ubuntu2004-ansible-desktop](https://hub.docker.com/repository/docker/iancleary/ubuntu2004-ansible-desktop) | Dockerfile for [iancleary/ansible-desktop](https://github.com/iancleary/ansible-desktop) CI Testing|

## Attributions

The Basic Idea

This is a template module collecting many utilities I have liked from other projects, to serve as a personal reference.

- [https://github.com/dawidd6/docker](https://github.com/dawidd6/docker) for the GitHub Action and Repo Structure
- [https://github.com/jessfraz/dockerfiles](https://github.com/jessfraz/dockerfiles) as a reference for bindings for various applications
