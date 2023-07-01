# Makefile

export SHARELATEX_BASE_TAG := sharelatex/sharelatex-base
export SHARELATEX_TAG := sharelatex/sharelatex

export SHARELATEX_BASE_TAG_PUSHED := registry.gitlab.com/overleaf-open/overleaf/sharelatex-base:latest
export SHARELATEX_TAG_PUSHED := registry.gitlab.com/overleaf-open/overleaf/sharelatex:latest

export SHARELATEX_BASE_CACHE := $(shell echo $(SHARELATEX_BASE_TAG) | sed -E 's/(.+):.+/\1:latest/')
export MONOREPO_REVISION := $(shell git rev-parse HEAD)
MONOREPO_ROOT := ../

all: build-base build-community push-finish

build-base:
	cp .dockerignore $(MONOREPO_ROOT)
	docker pull $(SHARELATEX_BASE_CACHE) || echo "nothing cached yet"
	docker buildx build --platform linux/amd64,linux/arm64 -f Dockerfile-base --pull --cache-from $(SHARELATEX_BASE_CACHE) -t $(SHARELATEX_BASE_TAG) $(MONOREPO_ROOT)
	docker tag sharelatex/sharelatex-base:latest $(SHARELATEX_BASE_TAG_PUSHED)
	docker push $(SHARELATEX_BASE_TAG_PUSHED)

build-community:
	cp .dockerignore $(MONOREPO_ROOT)
	docker buildx build --platform linux/amd64,linux/arm64 --build-arg SHARELATEX_BASE_TAG --build-arg MONOREPO_REVISION -f Dockerfile -t $(SHARELATEX_TAG) $(MONOREPO_ROOT)
	docker tag sharelatex/sharelatex:latest $(SHARELATEX_TAG_PUSHED)
	docker push $(SHARELATEX_TAG_PUSHED)

push-finish:
	echo "push image finish!"

.PHONY: all build-base build-community push-finish
