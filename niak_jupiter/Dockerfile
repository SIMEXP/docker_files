FROM simexp/niak_dependency:1.1
MAINTAINER Pierre-Olivier Quirion <poq@criugm.qc.ca>

# install niak
RUN  cd /home/ &&  wget -qO- -O tmp.zip  https://github.com/SIMEXP/niak/archive/dev-0.14.0.zip && unzip tmp.zip && rm tmp.zip
RUN  mv /home/niak-dev-0.14.0 /home/niak

RUN echo save_default_options\(\'-7\'\)\; >> /etc/octave.conf
RUN echo graphics_toolkit gnuplot >> /etc/octave.conf


# pip installation
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python3 get-pip.py
# jupyter install
RUN pip3 install notebook
# octave_kernel install
RUN pip3 install octave_kernel
RUN python3 -m octave_kernel.install
RUN pip3 install ipywidgets
# start jupyter then head to the adress http://localhost:8888/
RUN mkdir /home/niak/tutorial
WORKDIR /home/niak/tutorial

ADD execute_jup execute_jup
EXPOSE 8080

ENTRYPOINT ["/bin/bash", "-il", "execute_jup"]

#ENTRYPOINT ["jupyter", "notebook", "--no-browser"]

#CMD ["--port", "8080", "--ip=*"]


# Command for build
# docker build -t="simexp/jupyter_niak" .

