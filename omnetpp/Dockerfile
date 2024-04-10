#Define your ubuntu version
FROM ubuntu:20.04

MAINTAINER aleami3301@gmail.com

RUN apt-get update && apt-get upgrade -y
RUN apt install python2 -y
RUN update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
RUN apt-get install -y wget && apt-get install -y nano

#basic libraries installation
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get install build-essential clang lld gdb bison flex perl python3 python3-pip qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools libqt5opengl5-dev libxml2-dev zlib1g-dev doxygen graphviz libwebkit2gtk-4.0-37 xdg-utils -y
RUN python3 -m pip install --user --upgrade numpy pandas matplotlib scipy seaborn posix_ipc
RUN apt-get install openscenegraph-plugin-osgearth libosgearth-dev -y
RUN apt-get install mpi-default-dev -y

#basic python libraries instalation
#RUN pip install networkx==3.1

WORKDIR /workspace
#Define omnetpp version. Make sure it exists.
RUN wget https://github.com/omnetpp/omnetpp/releases/download/omnetpp-6.0.2/omnetpp-6.0.2-linux-x86_64.tgz && tar xvfz omnetpp-6.0.2-linux-x86_64.tgz
RUN rm omnetpp-6.0.2-linux-x86_64.tgz
WORKDIR /workspace/omnetpp-6.0.2

ENV PATH $PATH:/workspace/omnetpp-6.0.2/bin/
ENV __omnetpp_root_dir=/workspace/omnetpp/omnetpp-6.0.2/
ENV PYTHONPATH=/workspace/omnetpp/omnetpp-6.0.2/python/
ENV OMNETPP_RELEASE=omnetpp-6.0.2
RUN mkdir /usr/share/desktop-directories/
RUN /bin/bash -c "source setenv; ./configure WITH_QTENV=no WITH_OSG=no WITH_OSGEARTH=no"
RUN make

#Define inet and simu5g version. Make sure it exists.
WORKDIR /workspace/simu5g
RUN wget https://github.com/inet-framework/inet/releases/download/v4.5.0/inet-4.5.0-src.tgz
RUN tar xvfz inet-4.5.0-src.tgz
RUN rm inet-4.5.0-src.tgz
RUN wget https://github.com/Unipisa/Simu5G/archive/refs/tags/v1.2.2.tar.gz
RUN tar xvfz v1.2.2.tar.gz
RUN mv Simu5G* simu5g
RUN rm v1.2.2.tar.gz

#Define the files to be removed if you want
#WORKDIR /workspace/simu5g/simu5g
#RUN rm -r ./src/stack/phy/ChannelModel/LteRealisticChannelModel.cc

#Define the files to be copied if you want
#WORKDIR /workspace/simu5g
#COPY ./LteRealisticChannelModel.cc ./simu5g/src/stack/phy/ChannelModel/

#Make inet4.5 and simu5g
WORKDIR /workspace/simu5g/inet4.5
RUN /bin/bash -c "source setenv; make makefiles"
RUN make

WORKDIR /workspace/simu5g/simu5g
#RUN ["chmod", "+x", "setenv"]
RUN /bin/sh -c "source setenv; make makefiles"
RUN make
