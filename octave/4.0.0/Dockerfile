FROM simexp/minc-toolkit:1.9.11
MAINTAINER P-O Quirion <poq@criugm.qc.ca>

# Update repository list
RUN apt-get update


# Install octave
RUN apt-get install --force-yes -y \
  bison \
  build-essential \
  cmake \
  cmake-curses-gui \
  flex \  
  g++ \
  graphviz \
  imagemagick \
  liboctave-dev \
  libxi-dev \
  libxi6 \
  libxmu-dev \
  libxmu-headers \
  libxmu6 \  
  unzip \
  xpdf
  
# Fetch Octave forge packages
RUN mkdir /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/control-3.0.0.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/general-2.0.0.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/signal-1.3.2.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/image-2.4.1.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/io-2.4.1.tar.gz -P /home/octave
RUN wget http://sourceforge.net/projects/octave/files/Octave%20Forge%20Packages/Individual%20Package%20Releases/statistics-1.2.4.tar.gz -P /home/octave
WORKDIR /home/octave
# Install Octave forge packages
RUN octave --eval "cd /home/octave; \
                   more off; \
                   pkg install -auto -global -verbose \
                   control-3.0.0.tar.gz \
                   general-2.0.0.tar.gz \
                   signal-1.3.2.tar.gz \
                   image-2.4.1.tar.gz \
                   io-2.4.1.tar.gz \
                   statistics-1.2.4.tar.gz"

# Build octave configure file
RUN echo more off >> /etc/octave.conf
RUN echo save_default_options\(\'-7\'\)\; >> /etc/octave.conf
RUN echo graphics_toolkit gnuplot >> /etc/octave.conf

# Command for build
# docker build --no-cache -t="simexp/octave:4.0.0" .

# Command to run bash (don't start octave)
# docker run -i -t --rm --name octavebash -v $HOME:$HOME --user $UID:$GID simexp/octave:4.0.0 /bin/bash -c "export HOME=$HOME; cd $HOME; source /opt/minc-itk4/minc-toolkit-config.sh; exec bash"

# Command to run octave as command line
# docker run -i -t --rm --name octavecli -v $HOME:$HOME --user $UID:$GID simexp/octave:4.0.0 /bin/bash -c "export HOME=$HOME; cd $HOME; source /opt/minc-itk4/minc-toolkit-config.sh; octave"

# docker run -i -t --rm --name octavegui  -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY -v $HOME:$HOME --user $UID:$GID simexp/octave:4.0.0 /bin/bash -c "export HOME=$HOME; cd $HOME; source /opt/minc-itk4/minc-toolkit-config.sh; octave --force-gui"
