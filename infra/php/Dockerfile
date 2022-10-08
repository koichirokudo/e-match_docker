FROM golang:1.15 AS builder

RUN go get -d -v github.com/mailhog/mhsendmail \
&& cd /go/src/github.com/mailhog/mhsendmail/ \
&& GOOS=linux GOARCH=arm64 go build -o mhsendmail .

FROM php:7.4-fpm
COPY --from=builder /go/src/github.com/mailhog/mhsendmail/mhsendmail /usr/local/bin/
ENV TZ Asia/Tokyo

RUN apt-get update -qq; \
    apt-get install -y libicu-dev; \
    apt-get install --no-install-recommends -y libpq-dev libonig-dev libxml2-dev git zip unzip; \
    apt-get install --no-install-recommends -y zlib1g-dev libfreetype6-dev libpng-dev libjpeg62-turbo-dev libwebp-dev libxpm-dev; \
    aptget clean; \
    rm -rf /var/cache/apt; \
    npm install npm@latest -g; \
    docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp --with-xpm; \
    docker-php-ext-install intl pdo mbstring pgsql pdo_pgsql;

RUN chmod +x /usr/local/bin/mhsendmail; \
    addgroup nginx; \
    adduser --system --no-create-home --disabled-login --ingroup nginx nginx; \
    mkdir /var/run/php-fpm;

COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer
COPY ./zzz-docker.conf /usr/local/etc/php-fpm.d/zzz-docker.conf
COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /var/www