FROM ubuntu:16.04
MAINTAINER P-O Quirion <poq@criugm.qc.ca>

# Update repository list
# Only for 14.04 and older to update cmake
#RUN add-apt-repository ppa:george-edison55/cmake-3.x
#RUN apt-get dist-upgrade -y

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
#  RUN git clone https://github.com/BIC-MNI/minc-toolkit-v2.git
WORKDIR /tmp
#COPY minc-toolkit-v2 /tmp/minc-toolkit-v2
RUN git clone --recursive https://github.com/BIC-MNI/minc-toolkit-v2
RUN mkdir build 
WORKDIR build
#DEFAULT setting for the compilation
RUN cmake ../minc-toolkit-v2 -DCMAKE_INSTALL_PREFIX:PATH=/opt/minc-itk4 \
                  -DCMAKE_BUILD_TYPE:STRING=Release \
                  -DMT_BUILD_ITK_TOOLS:BOOL=ON \
                  -DMT_BUILD_LITE:BOOL=OFF \
                  -DMT_BUILD_ANTS:BOOL=ON \
                  -DMT_BUILD_C3D:BOOL=ON \
                  -DMT_BUILD_ABC:BOOL=ON \
                  -DMT_BUILD_IM:BOOL=OFF \
                  -DMT_BUILD_ELASTIX:BOOL=ON \
                  -DMT_BUILD_SHARED_LIBS:BOOL=ON \
                  -DMT_BUILD_VISUAL_TOOLS:BOOL=ON \
                  -DMT_USE_OPENMP:BOOL=ON \
                  -DCPACK_BINARY_DEB:BOOL=ON \
                  -DCPACK_BINARY_NSIS:BOOL=OFF \
                  -DCPACK_BINARY_RPM:BOOL=OFF \
                  -DCPACK_BINARY_STGZ:BOOL=OFF \
                  -DCPACK_BINARY_TBZ2:BOOL=OFF \
                  -DCPACK_BINARY_TGZ:BOOL=OFF \
                  -DCPACK_BINARY_TZ:BOOL=OFF \
                  -DCPACK_SOURCE_TBZ2:BOOL=OFF \
                  -DCPACK_SOURCE_TGZ:BOOL=OFF \
                  -DCPACK_SOURCE_TZ:BOOL=OFF \
                  -DCPACK_SOURCE_ZIP:BOOL=OFF \
                  -DCPACK_SOURCE_TXZ:BOOL=OFF \
                  -DUSE_SYSTEM_GLUT:BOOL=OFF
# build the minc tools
#RUN cat Makefile
RUN make -j 6 && make test
RUN make install
# put the source in the bashrc and profile
#
RUN echo "source /opt/minc-itk4/minc-toolkit-config.sh" >> /etc/profile
RUN echo "source /opt/minc-itk4/minc-toolkit-config.sh" >> /etc/bash.bashrc

# Command for build 
# docker build -t="simexp/minc-toolkit:1.9.11" .
# Command for running
# docker run -it --rm -v $HOME:$HOME --user $UID:$GID simexp/minc-toolkit:1.9.11 /bin/bash 
