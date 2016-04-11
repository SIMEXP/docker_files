FROM simexp/niak_dependency
MAINTAINER Pierre Bellec <pierre.bellec@criugm.qc.ca>

# Install NIAK
RUN cd /home/ && wget https://github.com/SIMEXP/niak/archive/v0.13.4.zip && unzip v0.13.4.zip && rm v0.13.4.zip
RUN mv /home/niak-0.13.4 /home/niak

# Build octave configure file
RUN echo addpath\(genpath\(\"/home/niak/\"\)\)\; >> /etc/octave.conf

# Command for build
# docker build -t="simexp/niak:0.13.0" .

# Command to run bash (don't start octave)
# docker run -i -t --rm --name niakbash -v $HOME:$HOME --user $UID:$GID simexp/niak:0.13.0 /bin/bash -c "export HOME=$HOME; export USER=$USER; cd $HOME; source /opt/minc-itk4/minc-toolkit-config.sh; exec bash"

# Command to run octave as command line
# docker run -i -t --rm --name niakcli -v $HOME:$HOME --user $UID:$GID simexp/niak:0.13.0 /bin/bash -c "export HOME=$HOME; export USER=$USER; cd $HOME; source /opt/minc-itk4/minc-toolkit-config.sh; octave"

# Command to run octave as GUI
# docker run -i -t --rm --name niakgui  -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY -v $HOME:$HOME --user $UID:$GID simexp/niak:0.13.0 /bin/bash -c "export HOME=$HOME; export USER=$USER; cd $HOME; source /opt/minc-itk4/minc-toolkit-config.sh; octave --force-gui"
