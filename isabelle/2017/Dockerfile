FROM debian:9.5-slim

RUN apt-get update && apt-get install -y \
    curl \
    lib32stdc++6 \
    libgomp1 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


# add isabelle user
RUN useradd -m isabelle && (echo isabelle:isabelle | chpasswd)
USER isabelle


# install Isabelle
WORKDIR /home/isabelle
RUN curl --fail --silent https://isabelle.in.tum.de/website-Isabelle2017/dist/Isabelle2017_app.tar.gz > Isabelle.tar.gz && \
    tar xzf Isabelle.tar.gz && \
    mv Isabelle2017 Isabelle && \
    rm -rf Isabelle.tar.gz Isabelle/contrib/jdk/x86-linux && \
    rm -f Isabelle/doc/*.pdf && \
    sed -i -e 's@ISABELLE_HOME_USER=.*@'"ISABELLE_HOME_USER=$HOME/.isabelle"'@g' Isabelle/etc/settings
ENV PATH="/home/isabelle/Isabelle/bin:${PATH}"


# set up the logic 
ARG DEF_LOGIC="HOLCF"
RUN sed -i -e 's@ISABELLE_LOGIC=.*@'"ISABELLE_LOGIC=$DEF_LOGIC"'@g' Isabelle/etc/settings && \
    isabelle build -s -b -j 4 -v HOLCF
