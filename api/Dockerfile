FROM php:7.1-fpm

LABEL maintainer="Marek Miernik <vincent.composieux@gmail.com>"

ENV ALLOW_OVERRIDE **False**
ENV TERM xterm

# Add repository
RUN apt-get autoclean && apt-get update
RUN apt-get install --no-install-recommends -y software-properties-common python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get update

# Install base packages
RUN apt-get install -y git curl nano wget make

# Install php
RUN apt-get install --no-install-recommends -y \
    php7.1 php7.1-cli php7.1-mysql php7.1-fpm \
    php7.1-curl php7.1-intl php7.1-dom php7.1-mbstring php7.1-zip \
    php7.1-xml php7.1-dev php-pear php7.1-bcmath php7.1-mcrypt php7.1-sqlite \
    php7.1-tokenizer

# Symfony installer
RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
RUN chmod a+x /usr/local/bin/symfony