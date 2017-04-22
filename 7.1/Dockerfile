FROM ubuntu:16.04

ENV ALLOW_OVERRIDE **False**
ENV TERM xterm

# Add repository
RUN apt-get autoclean && apt-get update
RUN apt-get install --no-install-recommends -y software-properties-common python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update