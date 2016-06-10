FROM ubuntu:16.04
MAINTAINER Pierre Bellec <pierre.bellec@criugm.qc.ca>

# Update repository list
RUN apt-get update
RUN apt-get dist-upgrade -y

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

# Clone or copy the minc tools was done before runnig the dockerfile
WORKDIR /tmp
RUN git clone --recursive https://github.com/BIC-MNI/minc-toolkit
RUN mkdir build 
WORKDIR build
#DEFAULT setting for the compilation
RUN cmake ../minc-toolkit -DCMAKE_INSTALL_PREFIX:PATH=/opt/minc \
                  -DCMAKE_BUILD_TYPE:STRING=Release \
                  -DUSE_SYSTEM_ZLIB:BOOL=ON
# build the minc tools
RUN make -j 7 && make test
RUN make install
# put the source in the bashrc and profile
#
RUN echo "source /opt/minc/minc-toolkit-config.sh" >> /etc/profile
RUN echo "source /opt/minc/minc-toolkit-config.sh" >> /etc/bash.bashrc
# Command for build 
# docker build -t="simexp/minc-toolkit:1.9.2_ubuntu_16.04" .
# Command for running
# docker run -i -t --rm --name minc-toolkit -v $HOME:$HOME --user $UID:$GID simexp/minc-toolkit:1.9.2 /bin/bash -c "export HOME=$HOME; cd $HOME; source /opt/minc/minc-toolkit-config.sh; exec bash"
