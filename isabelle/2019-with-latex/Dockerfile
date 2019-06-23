# used internally for CI

FROM ubuntu:latest

ADD 01_nodoc /etc/dpkg/dpkg.cfg.d/01_nodoc

RUN apt-get update \
    &&  DEBIAN_FRONTEND=noninteractive apt-get install -y \
        curl \
        lib32stdc++6 \
        libgomp1 \
        texlive-full \
        biber \
        curl \
        gnuplot \
        make \
    && apt-get --purge -y remove tex.\*-doc$ \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# add included latexmk version
ADD latexmk.pl /usr/bin/latexmk
RUN chmod +x /usr/bin/latexmk


# add isabelle user
RUN useradd -m isabelle && (echo isabelle:isabelle | chpasswd)
USER isabelle


# install Isabelle
WORKDIR /home/isabelle
RUN curl --silent --fail https://isabelle.in.tum.de/dist/Isabelle2019_linux.tar.gz > Isabelle.tar.gz && \
    tar xzf Isabelle.tar.gz && \
    mv Isabelle2019 Isabelle && \
    rm -rf Isabelle.tar.gz Isabelle/contrib/jdk/x86-linux && \
    rm -f Isabelle/doc/*.pdf && \
    sed -i -e 's@ISABELLE_HOME_USER=.*@ISABELLE_HOME_USER="$USER_HOME/.isabelle"@g' Isabelle/etc/settings
ENV PATH="/home/isabelle/Isabelle/bin:${PATH}"


# set up the logic 
ARG DEF_LOGIC="HOLCF"
RUN sed -i -e 's@ISABELLE_LOGIC=.*@'"ISABELLE_LOGIC=$DEF_LOGIC"'@g' Isabelle/etc/settings && \
    isabelle build -s -b -j 4 -v HOLCF
