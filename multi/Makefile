# Makefile

# export SHARELATEX_BASE_TAG := sharelatex/sharelatex-base
export SHARELATEX_BASE_TAG := registry.gitlab.com/overleaf-open/overleaf/sharelatex-base:latest
# export SHARELATEX_TAG := sharelatex/sharelatex
export SHARELATEX_TAG := registry.gitlab.com/overleaf-open/overleaf/sharelatex:latest

export SHARELATEX_BASE_CACHE := $(shell echo $(SHARELATEX_BASE_TAG) | sed -E 's/(.+):.+/\1:latest/')
export MONOREPO_REVISION := $(shell git rev-parse HEAD)
MONOREPO_ROOT := ../

all: build-base build-community push-image

build-base:
	cp .dockerignore $(MONOREPO_ROOT)
	docker pull $(SHARELATEX_BASE_CACHE) || echo "nothing cached yet"
	docker buildx build --platform linux/amd64,linux/arm64 -f Dockerfile-base --pull --cache-from $(SHARELATEX_BASE_CACHE) -t $(SHARELATEX_BASE_TAG) $(MONOREPO_ROOT)


build-community:
	cp .dockerignore $(MONOREPO_ROOT)
	docker buildx build --platform linux/amd64,linux/arm64 --build-arg SHARELATEX_BASE_TAG --build-arg MONOREPO_REVISION -f Dockerfile -t $(SHARELATEX_TAG) $(MONOREPO_ROOT)


push-image:
	echo "start push image"
	docker push $(SHARELATEX_BASE_TAG)
	docker push $(SHARELATEX_TAG)

.PHONY: all build-base build-community push-image
