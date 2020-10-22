FROM tensorflow/tensorflow:2.3.1-gpu-jupyter

# following instructions here https://github.com/cdr/code-server/blob/v3.5.0/doc/install.md
RUN curl -fsSL https://code-server.dev/install.sh | sh

RUN pip install pandas

RUN pip install psycopg2

RUN pip install SQLAlchemy

EXPOSE 8080

#USER coder

#WORKDIR /home/coder


ENTRYPOINT ["/usr/bin/entrypoint.sh" "--bind-addr" "0.0.0.0:8080" "."]