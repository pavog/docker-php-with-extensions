FROM php:7.4.4-fpm-alpine

RUN set -ex \
  && apk add --no-cache bash build-base wget curl m4 autoconf libtool imagemagick imagemagick-dev zlib zlib-dev libcurl curl-dev libevent libevent-dev libidn libidn-dev \
  && printf "\n" | pecl install raphf propro \
  && docker-php-ext-enable raphf propro \
  && printf "\n" | pecl install pecl_http \
  && echo -e "extension=raphf.so\nextension=propro.so\nextension=http.so" > /usr/local/etc/php/conf.d/docker-php-ext-http.ini \
  && rm -rf /usr/local/etc/php/conf.d/docker-php-ext-raphf.ini \
  && rm -rf /usr/local/etc/php/conf.d/docker-php-ext-propro.ini \
  && printf "\n" | pecl install redis timezonedb imagick mongodb xdebug \
  && docker-php-ext-enable redis timezonedb imagick mongodb xdebug \
  && docker-php-ext-install bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash iconv imap interbase intl json ldap mbstring mcrypt mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline recode reflection session shmop simplexml snmp soap sockets spl standard sysvmsg sysvsem sysvshm tidy tokenizer wddx xml xmlreader xmlrpc xmlwriter xsl zip \
  && cd /tmp \
  && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); exit(1); } echo PHP_EOL;" \
  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && php -r "unlink('composer-setup.php');" \
  && rm -rf /tmp/*

EXPOSE 9000
CMD ["php-fpm"]
