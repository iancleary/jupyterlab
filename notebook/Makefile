PHONY: help

# build notebook lab test test-env push release

# Docker namespace, image name and version/tag
NS?= iancleary
IMAGE_NAME?= notebook
VERSION?= latest

IMAGE=$(NS)/$(IMAGE_NAME)

VOLUMES=-v $(HOME)/jupyter/:/home/jovyan/jupyter/

# notebook and lab args defaults, override in make.env
GEN_CERT=-e GEN_CERT=yes
PORT=-p 8888:8888
JUPYTER_LAB = -e JUPYTER_ENABLE_LAB=yes

# Shell that make should use
SHELL:=bash

# - to suppress if it doesn't exist
-include make.env

help:
# http://marmelab.com/blog/2016/02/29/auto-documented-makefile.html
# adds anything that has a double # comment to the phony help list
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ".:*?## "}; {printf "\033[36m%-25s\033[0m %s\n", $$1, $$2}'

build: DARGS?=
build: ## Make the latest build of the image
	docker build $(DARGS) --rm --force-rm -t $(NS)/$(IMAGE_NAME):$(VERSION) .

notebook: ARGS?=
notebook: DARGS?=$(PORT) $(GEN_CERT) $(VOLUMES) $(IMAGE)
notebook: ## Run a container from a tagged image and start in the regular notebook view
	docker run -it --rm $(DARGS) $(REPO) $(ARGS)

lab: ARGS?=
lab: DARGS?=$(PORT) $(JUPYTER_LAB) $(GEN_CERT) $(VOLUMES) $(IMAGE)
lab: ## Run a container from a tagged image and start in JupyterLab view
	docker run -it --rm $(DARGS) $(REPO) $(ARGS)

ephemeral: ARGS?=
ephemeral: DARGS?=$(PORT) $(JUPYTER_LAB) $(GEN_CERT) $(IMAGE)
ephemeral: ## Run a container from a tagged image and start in JupyterLab view, without volumes
	docker run -it --rm $(DARGS) $(REPO) $(ARGS)

.DEFAULT_GOAL := help
