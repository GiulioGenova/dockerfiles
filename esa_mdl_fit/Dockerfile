FROM laurapoggio/cos8dfsp:v.0.2.6

RUN dnf -y install awscli
RUN Rscript -e 'install.packages("aws.s3",lib=.Library, repos = c("cloudyr" = "http://cloudyr.github.io/drat"))'

RUN Rscript -e 'install.packages(c("rlang", "yardstick", "caret","Metrics","argparser","tidymodels" ),lib=.Library,repos="https://mirrors.evoluso.com/CRAN/")'
RUN Rscript -e 'devtools::install_github("r-barnes/dggridR", lib=.Library, ref="install_github")'
