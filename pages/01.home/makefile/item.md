---
title: Makefile
---

## Makefile 

## Run shell commands
```makefile
DOCKER_GID=$(shell getent group docker | cut -d: -f3)
```
## echo

Prefixing with `@` does not print out the command itself

```makefile
	@echo "Spinning up the cluster"
	kind create cluster --config kind.yaml
```

## User defined function
```makefile
define get_conf
$(shell yq -r .$(1) conf.yml)
endef
NAME:=$(call get_conf,name)
```

## Concat variables
```makefile
BUILDARGS=--build-arg uid=$(UID) --build-arg gid=$(GID)
BUILDARGS:=$(BUILDARGS) --build-arg docker_gid=$(DOCKER_GID)
BUILDARGS:=$(BUILDARGS) --build-arg name=$(NAME)
```

## IF
```makefile
ifeq ($(MOUNT_AWS_FOLDER), true)
MOUNT:=${MOUNT} -v $$HOME/.aws/:/home/${NAME}/.aws
endif
```

```makefile
	@if [ "$(TARGET)" == "" ]; then echo "Missing target variable - run make targets for possible values"; exit 1; fi
```

## Help message
```makefile
.PHONY: help

help: ## This help.
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)

.DEFAULT_GOAL := help
```
This allows something like the following where everything after `##` is printed as help message
```makefile
build: ## Build the container
	@echo 'Building image'
	docker build $(BUILDARGS) -t $(NAME) .
```