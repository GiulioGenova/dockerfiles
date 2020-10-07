FROM tensorflow/tensorflow:2.3.1-gpu-jupyter

ADD 4b03b5f551e3fbdf47ec609712007327828f7530cc3455c43bbcdcaf449a75a9 in / 

CMD ["bash"] 

RUN /bin/sh -c apt-get update  && apt-get install -y     curl     dumb-init     htop     locales     man     nano     git     procps     ssh     sudo     vim     lsb-release   && rm -rf /var/lib/apt/lists/*

RUN /bin/sh -c sed -i "s/# en_US.UTF-8/en_US.UTF-8/" /etc/locale.gen   && locale-gen

ENV LANG=en_US.UTF-8

RUN /bin/sh -c chsh -s /bin/bash

ENV SHELL=/bin/bash

RUN /bin/sh -c adduser --gecos '' --disabled-password coder &&   echo "coder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/nopasswd

RUN /bin/sh -c ARCH="$(dpkg --print-architecture)" &&     curl -fsSL "https://github.com/boxboat/fixuid/releases/download/v0.4.1/fixuid-0.4.1-linux-$ARCH.tar.gz" | tar -C /usr/local/bin -xzf - &&     chown root:root /usr/local/bin/fixuid &&     chmod 4755 /usr/local/bin/fixuid &&     mkdir -p /etc/fixuid &&     printf "user: coder\ngroup: coder\n" > /etc/fixuid/config.yml

COPY 78a849f414017248a4fc8f5a4e941432c80435bb44e3df498495e2143b876a29 in /tmp/ 


COPY f89dace6fac61bcbe2a03cc661a85c1f6e646c6bec10a3f71fd7699b6ba03680 in /usr/bin/entrypoint.sh 

RUN /bin/sh -c dpkg -i /tmp/code-server*$(dpkg --print-architecture).deb && rm /tmp/code-server*.deb


EXPOSE 8080

USER coder

WORKDIR /home/coder


ENTRYPOINT ["/usr/bin/entrypoint.sh" "--bind-addr" "0.0.0.0:8080" "."]