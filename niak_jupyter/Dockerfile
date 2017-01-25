FROM niak/beta
MAINTAINER Pierre-Olivier Quirion <poq@criugm.qc.ca>

# install niak
#RUN  cd /home/ &&  wget -qO- -O tmp.zip  https://github.com/SIMEXP/niak/archive/dev-0.14.0.zip && unzip tmp.zip && rm tmp.zip
#RUN  mv /home/niak-dev-0.14.0 /home/niak

RUN echo save_default_options\(\'-7\'\)\; >> /etc/octave.conf
RUN echo graphics_toolkit gnuplot >> /etc/octave.conf


# pip installation
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
# jupyter install
RUN pip install notebook
# octave_kernel install
RUN pip install octave_kernel
RUN python -m octave_kernel.install
RUN pip install ipywidgets
# start jupyter then head to the adress http://localhost:8888/
RUN mkdir -p /jupyter_tutorial
WORKDIR /juyter_sandbox

ADD niak_jupyter /usr/local/bin/niak_jupyter
ADD psom_gb_vars_local.jupyter /usr/local/lib/psom_gb_vars_local.jupyter
RUN chmod 777 /usr/local/bin/niak_jupyter
EXPOSE 80 

#ENTRYPOINT ["/bin/bash", "-il", "execute_jup"]

#ENTRYPOINT ["jupyter", "notebook", "--no-browser"]

#CMD ["--port", "80", "--ip=*"]


# Command for build
# docker build -t="simexp/niak_jupyter" .

