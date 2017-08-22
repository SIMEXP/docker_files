FROM ubuntu:16.04
MAINTAINER P-O Quirion <poq@criugm.qc.ca>

# Install dependencies available through apt-get
RUN apt-get update && apt-get install -y \
  bc \
  bison \
  bzr \
  cmake \
  flex \
  freeglut3-dev \
  g++ \
  git \
  imagemagick \
  libc6 \
  libexpat1 \
  libgl1 \
  libgl1-mesa-dev \
  libglapi-mesa \
  libgsl-dev \
  libjpeg62 \
  libstdc++6 \
  libtiff5 \
  libtalloc-dev \
  libuuid1 \
  libx11-6 \
  libxau6 \
  libxcb1 \
  libxdmcp6 \
  libxext6 \
  libxi-dev \
  libxmu-dev \
  make \
  mesa-utils-extra \
  patch \
  perl \
  software-properties-common \
  xorg-dev \
  wget \
  zip \
  zlib1g-dev

WORKDIR /tmp
COPY minc-toolkit-1.9.15-20170308-Ubuntu_16.04-x86_64.deb /tmp/minc-toolkit-1.9.15-20170308-Ubuntu_16.04-x86_64.deb
RUN dpkg -i minc-toolkit-1.9.15-20170308-Ubuntu_16.04-x86_64.deb
RUN rm /tmp/minc-toolkit-1.9.15-20170308-Ubuntu_16.04-x86_64.deb

# minc-toolkit configuration parameters for 1.9.15-20170308
ENV MINC_TOOLKIT /opt/minc/1.9.15
ENV MINC_TOOLKIT_VERSION "1.9.15-20170308"
ENV PATH /opt/minc/1.9.15/bin:/opt/minc/1.9.15/pipeline:${PATH}
ENV PERL5LIB /opt/minc/1.9.15/perl:/opt/minc/1.9.15/pipeline:${PERL5LIB}
ENV LD_LIBRARY_PATH /opt/minc/1.9.15/lib:/opt/minc/1.9.15/lib/InsightToolkit:${LD_LIBRARY_PATH}
ENV MNI_DATAPATH /opt/minc/1.9.15/share
ENV MINC_FORCE_V2 1
ENV MINC_COMPRESS 4
ENV VOLUME_CACHE_THRESHOLD -1
ENV MANPATH /opt/minc/1.9.15/man:${MANPATH}


 
#
#ADD beast-library-1.1 /opt/minc-itk4/share/beast-library-1.1
#ADD icbm152_model_09c /opt/minc-itk4/share/icbm152_model_09c
#RUN rm -r /opt/minc-itk4/pipeline 
#ADD pipeline /opt/minc-itk4/pipeline
# Command for build 
# docker build -t="simexp/minc-toolkit:1.9.15" .
# Command for running
# docker run -it --rm -v $HOME:$HOME --user $UID:$GID simexp/minc-toolkit:1.9.11 /bin/bash 
