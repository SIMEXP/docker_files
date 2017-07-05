FROM simexp/minc-toolkit:1.9.15
MAINTAINER P-O Quirion <poq@criugm.qc.ca>

# Update repository list
RUN apt update

RUN apt-get install -y \
  gcc \
  g++ \
  gfortran \
  make 

RUN apt-get install -y \
  libpcre3-dev

RUN apt-get install  -y \
  libcurl4-gnutls-dev\
  epstool\
  libfftw3-dev\
  transfig\
  libfltk1.3-dev\
  libfontconfig1-dev\
  libfreetype6-dev\
  libgl2ps-dev\
  libglpk-dev\
  libreadline-dev\
  gnuplot-x11\
  libgraphicsmagick++1-dev\
  libhdf5-serial-dev\
  openjdk-8-jdk\
  libsndfile1-dev\
  llvm-dev\
  lpr\
  libgl1-mesa-dev\
  libosmesa6-dev\
  pstoedit\
  portaudio19-dev\
  libqhull-dev\
  libqscintilla2-dev\
  libsuitesparse-dev\
  texlive\
  texinfo\
  libxft-dev\
  zlib1g-dev

RUN apt-get install -y \
  libqt4-dev \
  libqtcore4 \
  libqtwebkit4 \
  libqt4-network \
  libqtgui4 \
  libqt4-opengl-dev   


# Install octave
RUN apt-get install -y \
  autoconf\
  automake\
  bison \
  flex \  
  gperf \
  gzip \
  icoutils\
  librsvg2-bin \
  libtool \  
  perl \
  rsync \
  tar

# get octave in the container
# compile openblas with 64 bit option for fortran array indexes 
ADD OpenBLAS-0.2.19 /tmp/OpenBLAS-0.2.19
WORKDIR /tmp/OpenBLAS-0.2.19
RUN make -j 7
RUN make install
ENV LD_LIBRARY_PATH="/opt/all64/lib:${LD_LIBRARY_PATH}"

Add opt64.conf /etc/ld.so.conf.d/opt64.conf
RUN ln -s /opt/all64/lib/libopenblas.so /usr/lib/libopenblas.so


ADD qrupdate-1.1.2 /tmp/qrupdate-1.1.2
WORKDIR /tmp/qrupdate-1.1.2
RUN make solib
RUN make install

ADD SuiteSparse /tmp/SuiteSparse
WORKDIR /tmp/SuiteSparse
RUN make CFLAGS='-DLONGBLAS=long' CXXFLAGS='-DLONGBLAS=long'
RUN cp -r ./lib/*  /opt/all64/lib/.

ADD ARPACK /tmp/ARPACK
WORKDIR /tmp/ARPACK
RUN make -j 8
RUN make install


ADD octave-4.2.1 /tmp/octave-4.2.1
# compile octave with 64 bit option for fortran array indexes 
WORKDIR /tmp/octave-4.2.1
RUN ./configure LD_LIBRARY_PATH=/opt/all64/lib CPPFLAGS=-I/opt/all64/include LDFLAGS=-L/opt/all64/lib \
  JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 \
  --with-hdf5-includedir=/usr/include/hdf5/serial --with-hdf5-libdir=/usr/lib/x86_64-linux-gnu/hdf5/serial \
   --enable-64 F77_INTEGER_8_FLAG='-fdefault-integer-8'
RUN make -j 7
RUN cp -r /opt/all64/lib/*  /usr/lib/.
#RUN make check 
RUN make install


# Fetch Octave forge packages

ADD octave_package /tmp/octave_package

WORKDIR /tmp/octave_package
# Install Octave forge packages
RUN octave --eval "more off; \
                   pkg install -auto -global -verbose \
                   control-3.0.0.tar.gz \
                   general-2.0.0.tar.gz \
                   signal-1.3.2.tar.gz \
                   image-2.6.1.tar.gz \
                   io-2.4.7.tar.gz \
                   statistics-1.3.0.tar.gz"


# Build octave configure file
RUN echo 'cellfun (@(x) pkg ("load", x.name), pkg ("list"));' >> /etc/octave.conf
RUN echo more off >> /etc/octave.conf
RUN echo save_default_options\(\'-7\'\)\; >> /etc/octave.conf
RUN echo graphics_toolkit gnuplot >> /etc/octave.conf
ENV OCTAVE_VERSION_INITFILE /etc/octave.conf
RUN rm -r /tmp/ARPACK /tmp/SuiteSparse /tmp/OpenBLAS-0.2.19 /tmp/qrupdate-1.1.2 /tmp/octave-4.2.1 /tmp/octave_package


# Command for build
# docker build --no-cache -t="simexp/octave:4.2.1_ubuntu_16" .
# docker build -t="simexp/octave:4.2.1_ubuntu_16" .
