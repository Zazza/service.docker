FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -yq --no-install-recommends \
    software-properties-common \
    apt-utils \
    build-essential \
    curl \
    git \
    # Install tools
    openssl \
    cron \
    nano \
    graphicsmagick \
    imagemagick \
    ghostscript \
    iputils-ping \
    locales \
    gnupg2 \
    g++ \
    ca-certificates
    
RUN curl -s "https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh" | bash    

RUN LC_ALL=en_US.UTF-8 apt-add-repository -y ppa:ondrej/php \
    && apt-get clean -y \
    && apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install --no-install-recommends -yq \
    php7.3-cli \
    php7.3-json \
    php7.3-curl \
    php7.3-fpm \
    php7.3-gd \
    php7.3-ldap \
    php7.3-mbstring \
    php7.3-soap \
    php7.3-xml \
    php7.3-zip \
    php7.3-dev \
    php7.3-intl \
    php7.3-amqp \
    php7.3-bcmath \
    php7.3-gmp \
    php7.3-mysqli \
    php-imagick \
    php-xdebug \
    
    php7.3-phalcon \
    
    composer \


    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install composer
#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY ./config/cgi/php.ini /etc/php/7.3/cgi/php.ini
COPY ./config/fpm/php.ini /etc/php/7.3/fpm/php.ini
COPY ./config/fpm/php-fpm.conf /etc/php/7.3/fpm/php-fpm.conf
COPY ./config/fpm/pool.d/www.conf /etc/php/7.3/fpm/pool.d/www.conf
COPY ./config/fpm/mods-available/xdebug.ini /etc/php/7.3/mods-available/xdebug.ini

COPY start.sh start.sh
RUN chmod +x start.sh
CMD ["./start.sh"]