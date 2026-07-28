SRC=$(wildcard *.go)
LATEST_VERSION=$(shell tail -1 versions.txt)
IMAGE=gcr.io/cloudark-kubeplus/helm-pod

.PHONY: all
all: .image-built

.image-built: helm-pod
ifdef KUBEPLUS_BUILD_VERSIONED
	docker build -t $(IMAGE):$(LATEST_VERSION) .
	docker push $(IMAGE):$(LATEST_VERSION)
else
	docker build -t $(IMAGE):latest .
endif
	@touch $@

helm-pod: $(SRC)
	CGO_ENABLED=0 GOOS=linux go build -o $@