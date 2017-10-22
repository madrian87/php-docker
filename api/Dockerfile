FROM php:7.1-fpm

LABEL maintainer="Marek Miernik <miernikmarek@gmail.com>"

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

RUN mkdir -p /var/log/php
RUN sed -ie 's/;error_log = syslog/error_log = \/var\/log\/php\/error.log/g' /etc/php/7.1/fpm/php.ini
RUN sed -ie 's/memory_limit = 128M/memory_limit = 1024M/g' /etc/php/7.1/fpm/php.ini

RUN sed -ie 's/listen = \/run\/php\/php7.1-fpm.sock/listen = 0.0.0.0:9000/g' /etc/php/7.1/fpm/pool.d/www.conf
RUN service php7.1-fpm reload

# Symfony installer
RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
RUN chmod a+x /usr/local/bin/symfony

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH $PATH:/usr/share/nginx/html/app/vendor/bin

# Phing
RUN wget http://www.phing.info/get/phing-latest.phar
RUN mv phing-latest.phar /usr/local/bin/phing
RUN chmod +x /usr/local/bin/phing

# Running fpm service
RUN service php7.1-fpm start

CMD ["php-fpm7.1", "-F"]
EXPOSE 9000