FROM simexp/niak_dependency:1.1
MAINTAINER Pierre-Olivier Quirion <poq@criugm.qc.ca>

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
EXPOSE 8080

ENTRYPOINT ["jupyter", "notebook", "--no-browser"]

CMD ["--port", "8080", "--ip=*"]


# Command for build
# docker build -t="simexp/jupyter" .

