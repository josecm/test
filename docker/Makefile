## 
 # Bao, a Lightweight Static Partitioning Hypervisor 
 #
 # Copyright (c) Bao Project (www.bao-project.org), 2019-
 #
 # Authors:
 #      Jose Martins <jose.martins@bao-project.org>
 #
 # Bao is free software; you can redistribute it and/or modify it under the
 # terms of the GNU General Public License version 2 as published by the Free
 # Software Foundation, with a special exception exempting guest code from such
 # license. See the COPYING file in the top-level directory for details. 
 #
##

root_dir?=$(realpath ../..)

DOCKER?=$(shell which docker)
docker_repo:=josecm/test
docker_tag:=latest
docker_image:=$(docker_repo):$(docker_tag)

override MAKEFLAGS:=$(addprefix -,$(MAKEFLAGS)) --no-print-directory

all .DEFAULT:
	@echo "Launching docker container..."
	-@$(DOCKER) run --rm -it -u bao -v $(root_dir):$(root_dir) -w $(root_dir) \
		$(docker_image) $(MAKE) $(MAKEFLAGS) $(MAKEOVERRIDES) $@
	@echo "Leaving and destroying docker container..."

build:
	@echo "Launching docker container..."
	@$(DOCKER) build -t $(docker_image) .

push: build
	@echo "Pushing container image to $(docker_repo)"
	@$(DOCKER) push $(docker_image)

.PHONY: all build push
