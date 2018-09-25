FROM ubuntu:16.04

LABEL maintainer=binwei.yang@gmail.com

RUN apt-get -y update
RUN apt-get -y upgrade

RUN apt-get install -y python-setuptools python-pip python-numpy

RUN pip install --upgrade pip

WORKDIR /opt/nmslib

COPY ./requirements.txt .

RUN pip install -r requirements.txt
