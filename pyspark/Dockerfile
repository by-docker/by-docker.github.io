FROM continuumio/miniconda

RUN apt-get upgrade -y && apt-get update && DEBIAN_FRONTEND=noninteractive \
    apt-get -y install default-jre-headless && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN conda install -y pypandoc pyspark jupyter

CMD ['/bin/bash']
