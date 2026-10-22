FROM php:8.6-rc-alpine

WORKDIR /usr/src/analytics-service/
COPY . .

# Install and enable required PHP extensions
RUN apk update && apk add --no-cache \
    postgresql-dev \
    curl-dev

RUN docker-php-ext-install pdo_pgsql curl

EXPOSE 8087
CMD ["php", "-S", "0.0.0.0:8087", "router.php"]
