FROM laurapoggio/cos8dfsp:v.0.2.6.1

RUN wget https://github.com/jgm/pandoc/releases/download/2.19.2/pandoc-2.19.2-linux-amd64.tar.gz
RUN tar xvzf pandoc-2.19.2-linux-amd64.tar.gz --strip-components 1 -C /usr/
RUN rm -f pandoc-2.19.2-linux-amd64.tar.gz

# See http://bugs.python.org/issue19846
ENV LANG C.UTF-8
ENV QUARTO_VERSION=1.0.38

RUN  yum install -y pandoc

RUN mkdir -p /opt/quarto/${QUARTO_VERSION}

RUN curl -o quarto.tar.gz -L \
    "https://github.com/quarto-dev/quarto-cli/releases/download/v${QUARTO_VERSION}/quarto-${QUARTO_VERSION}-linux-amd64.tar.gz"

RUN tar -zxvf quarto.tar.gz \
    -C "/opt/quarto/${QUARTO_VERSION}" \
    --strip-components=1

RUN rm quarto.tar.gz

RUN ln -s /opt/quarto/${QUARTO_VERSION}/bin/quarto /usr/local/bin/quarto

RUN Rscript -e "install.packages(c('quarto'),lib=.Library,repos='https://mirrors.evoluso.com/CRAN/')"
RUN Rscript -e "install.packages(c('rmarkdown'),lib=.Library,repos='https://mirrors.evoluso.com/CRAN/')"