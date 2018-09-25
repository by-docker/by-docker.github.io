# Use:
#
# `make container` will build a container
# `make save` will save the container as a tar ball

IMAGE_NAME ?=nmslib
DOCKER_FILE ?=Dockerfile
JUPYTER_IMAGE_NAME ?=nmslib-jupyter
JUPYTER_DOCKER_FILE ?=Dockerfile.jupyter
JUPYTER_PORT ?=8080

file := 'VERSION'
VERSION := $(shell cat ${file})

container:
	docker build --pull	-t $(IMAGE_NAME) -f ${DOCKER_FILE} .
	docker tag $(IMAGE_NAME) $(IMAGE_NAME):$(VERSION)

save: container
	docker save -o $(IMAGE_NAME).tar $(IMAGE_NAME)

jupyter:
	docker build --build-arg NMSLIB_VERSION=$(VERSION) -t $(JUPYTER_IMAGE_NAME) -f ${JUPYTER_DOCKER_FILE} .
	docker tag $(JUPYTER_IMAGE_NAME) $(JUPYTER_IMAGE_NAME):$(VERSION)

run_notebooks:
	docker run --rm -p $(JUPYTER_PORT):8888 -v $(NMSLIB_DIR):/opt/nmslib $(JUPYTER_IMAGE_NAME):$(VERSION) jupyter notebook --notebook-dir=/opt/nmslib/python_bindings/notebooks --ip 0.0.0.0 --no-browser --allow-root
