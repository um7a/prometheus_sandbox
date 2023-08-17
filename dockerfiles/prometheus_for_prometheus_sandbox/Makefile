IMAGE_NAME := local/prometheus_for_prometheus_sandbox
TAG := 0.0.1
CONTAINER_NAME := $(shell echo test_run_${IMAGE_NAME}_${TAG} | sed -e s/\\//_/g)

ContainerExists = "$(shell docker ps | grep ${CONTAINER_NAME})"

.PHONY: help
help:
	@echo ""
	@echo "  TARGETS"
	@echo "    build  ... Build docker image ${IMAGE_NAME}"
	@echo "    clean  ... Clean docker image ${IMAGE_NAME}"
	@echo "    run    ... Run docker container using image ${IMAGE_NAME}"
	@echo "    attach ... Attach on docker container using image ${IMAGE_NAME}"
	@echo "    stop   ... Stop docker container which was created by run target"
	@echo ""

.PHONY: build
build: Dockerfile
	docker build --rm -t ${IMAGE_NAME}:${TAG} .

.PHONY: clean
clean: stop
	docker rmi ${IMAGE_NAME}:${TAG}

.PHONY: run
run: stop
	@echo "Start test container."
	docker run \
	-itd \
	--rm \
	--name ${CONTAINER_NAME} \
	-v $(shell pwd)/files/home/prometheus:/home/prometheus \
	-p 9090:9090 \
	${IMAGE_NAME}:${TAG}
	@echo "Now you can access web ui from localhost:9090."

.PHONY: attach
attach:
	# Execute bash
	docker exec \
	-it \
	${CONTAINER_NAME} \
	/bin/bash

.PHONY: stop
stop:
ifneq (${ContainerExists}, "")
	@echo "!!! Container exists. Delete. !!!"
	docker stop \
	${CONTAINER_NAME}
else
	@echo "Container does not exist."
endif
