FROM nvidia/cuda:8.0-devel-ubuntu16.04 as binary_build

RUN apt-get -y update
RUN apt-get -y upgrade

RUN apt-get install -y libopenblas-dev python3-numpy python3-dev python3-pip python3-matplotlib swig wget curl git

WORKDIR /opt

RUN git clone https://github.com/facebookresearch/faiss && cd faiss && git checkout v1.4.0

ENV BLASLDFLAGS /usr/lib/libopenblas.so.0

RUN ln -s /usr/bin/python3 /usr/bin/python

ENV PYTHON_CFLAGS "-I/usr/include/python3.5m/ -I/usr/lib/python3/dist-packages/numpy/core/include"

WORKDIR /opt/faiss

RUN ./configure LIBS=-lgomp && make -j $(nproc) && make py

ENV PYTHONPATH=/opt/faiss/python

RUN cd tests && make

FROM nvidia/cuda:8.0-runtime-ubuntu16.04

LABEL maintainer=binwei.yang@gmail.com

RUN apt-get -y update
RUN apt-get -y upgrade

RUN apt-get install -y libopenblas-dev python3-numpy python3-pip python3-matplotlib swig

ENV BLASLDFLAGS /usr/lib/libopenblas.so.0

RUN ln -s /usr/bin/python3 /usr/bin/python

COPY --from=binary_build /opt/faiss/python/*.py /usr/local/lib/python3.5/dist-packages/
COPY --from=binary_build /opt/faiss/python/faiss /usr/local/lib/python3.5/dist-packages/faiss/
COPY --from=binary_build /opt/faiss/python/*.so /usr/local/lib/python3.5/dist-packages/
