SRC=$(wildcard *.go)
LATEST_VERSION=$(shell tail -1 versions.txt)

.PHONY: all
all: .image-built

.image-built: crd-hook
ifdef KUBEPLUS_BUILD_VERSIONED
	docker build -t gcr.io/cloudark-kubeplus/pac-mutating-admission-webhook:$(LATEST_VERSION) .
	docker push gcr.io/cloudark-kubeplus/pac-mutating-admission-webhook:$(LATEST_VERSION)
else
	docker build -t gcr.io/cloudark-kubeplus/pac-mutating-admission-webhook:latest .
endif
	@touch $@

crd-hook: $(SRC)
	CGO_ENABLED=0 GOOS=linux go build -o $@