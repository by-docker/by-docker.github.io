# Use:
#
# `make container` will build a container
# `make save` will save the container as a tar ball

IMAGE_NAME ?=pyspark-jupyter
DOCKER_FILE ?=Dockerfile
JUPYTER_PORT ?=8080

file := 'VERSION'
VERSION := $(shell cat ${file})

container:
	docker build --pull -t $(IMAGE_NAME) -f ${DOCKER_FILE} .
	docker tag $(IMAGE_NAME) $(IMAGE_NAME):$(VERSION)

save: container
	docker save -o $(IMAGE_NAME).tar $(IMAGE_NAME)

run_notebooks: container
	docker run --rm -p $(JUPYTER_PORT):8888 -v $(NOTEBOOKS_DIR):/notebooks $(IMAGE_NAME):$(VERSION) jupyter notebook --notebook-dir=/notebooks --ip 0.0.0.0 --no-browser --allow-root
