#Define your ubuntu version
FROM ubuntu:20.04

MAINTAINER aleami3301@gmail.com

RUN apt-get update && apt-get upgrade -y
RUN apt install python2 -y
RUN update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
RUN apt-get install -y wget && apt-get install -y nano

#basic libraries installation
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get install g++ python3 python3-setuptools git qt5-default gir1.2-goocanvas-2.0 python3-gi python3-gi-cairo python3-pygraphviz gir1.2-gtk-3.0 ipython3 uncrustify doxygen graphviz imagemagick texlive texlive-extra-utils texlive-latex-extra texlive-font-utils texlive-lang-portuguese dvipng latexmk python3-sphinx dia gsl-bin libgsl-dev libgslcblas0 tcpdump sqlite sqlite3 libsqlite3-dev libxml2 libxml2-dev libboost-all-dev cmake libc6-dev libc6-dev-i386 libclang-6.0-dev llvm-6.0-dev automake python3-pip castxml -y
RUN apt install openmpi-bin openmpi-common openmpi-doc libopenmpi-dev autoconf cvs bzr unrar gdb valgrind -y
RUN pip3 install --user cxxfilt pygccxml
RUN apt-get install libgtk-3-dev vtun lxc uml-utilities -y
RUN mkdir workspace

WORKDIR workspace
RUN wget http://www.nsnam.org/release/ns-allinone-3.34.tar.bz2
RUN tar xjf ns-allinone-3.34.tar.bz2

WORKDIR ns-allinone-3.34/
RUN ./build.py

WORKDIR ns-allinone-3.34/ns-3.34
RUN ./waf -d debug configure
RUN ./waf --enable-tests --enable-examples configure
RUN ./waf
RUN ./test.py


