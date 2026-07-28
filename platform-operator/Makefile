SRC=$(wildcard *.go)
LATEST_VERSION=$(shell tail -1 versions.txt)
IMAGE=gcr.io/cloudark-kubeplus/platform-operator

.PHONY: all
all: .image-built

.image-built: artifacts/deployment/platform-operator
ifdef KUBEPLUS_BUILD_VERSIONED
	docker build -t $(IMAGE):$(LATEST_VERSION) ./artifacts/deployment
	docker push $(IMAGE):$(LATEST_VERSION)
else
	docker build -t $(IMAGE):latest ./artifacts/deployment
endif
	@touch $@

artifacts/deployment/platform-operator: $(SRC)
	CGO_ENABLED=0 GOOS=linux go build -o $@