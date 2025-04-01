FROM php:8.3-fpm
ARG TIMEZONE

# Copier la configuration PHP
COPY php.ini /usr/local/etc/php/conf.d/docker-php-config.ini

# Installation des dépendances système et extensions PHP
RUN apt-get update && apt-get install -y \
    gnupg g++ procps openssl git unzip acl \
    zlib1g-dev libzip-dev libfreetype6-dev libpng-dev libjpeg-dev \
    libicu-dev libonig-dev libxslt1-dev libpq-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install zip xsl gd intl opcache exif mbstring pdo pdo_pgsql pgsql \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Définir le fuseau horaire
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
    && echo "[PHP]\ndate.timezone = \"${TIMEZONE}\"" > /usr/local/etc/php/conf.d/tzone.ini \
    && date

# Installer Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Installer Symfony CLI proprement
RUN curl -sS https://get.symfony.com/cli/installer | bash \
    && mv /root/.symfony*/bin/symfony /usr/local/bin/symfony \
    && rm -rf /root/.symfony*

# Définir un alias Symfony
RUN echo 'alias sf="php bin/console"' >> ~/.bashrc

# Définir le dossier de travail
WORKDIR /var/www/html
