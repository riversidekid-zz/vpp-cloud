TAG ?= latest # Tag images with :$(TAG)
VERSION_FILE=version
GENERATE_LOG_FILE=../vpplink/binapi/vppapi/generate.log
ALSO_LATEST ?= n # If 'y' also tag images with :latest

.PHONY: build
build:
	go build -o ./watcher .

.PHONY: image
image: build
	@echo "Image tag                   : $(TAG)"                         > $(VERSION_FILE)
	@echo "VPP-dataplane version       : $(shell git log -1 --oneline)" >> $(VERSION_FILE)
	@cat $(GENERATE_LOG_FILE)                                           >> $(VERSION_FILE)
	docker build --pull -t calicovpp/multinet-monitor:$(TAG) .
	@if [ "${ALSO_LATEST}" = "y" ]; then \
		docker tag calicovpp/agent:$(TAG) calicovpp/agent:latest; \
	fi

.PHONY: dev
dev: image
