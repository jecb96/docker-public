## Dockerfile for LaTeX (CI Usage)
FROM ubuntu:17.10
SHELL ["/bin/bash", "-c"]

ADD 01_nodoc /etc/dpkg/dpkg.cfg.d/01_nodoc

# packages
RUN apt-get update && apt-get install  -y  \
    texlive-full \
	biber \
	curl \
	gnuplot \
	make \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
  
  
# add included latexmk version
ADD latexmk.pl /usr/bin/latexmk
RUN chmod +x /usr/bin/latexmk
