## Dockerfile for LaTeX (CI Usage)
FROM ubuntu:latest

# packages
RUN apt-get update && apt-get install  -y  \
    texlive-full \
	biber \
	curl \
	gnuplot \
	make \
	latexmk \
  && rm -rf /var/lib/apt/lists/*