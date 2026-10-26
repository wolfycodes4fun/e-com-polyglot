FROM php:8.6-rc-alpine

WORKDIR /usr/src/analytics-service/

# Install and enable required PHP extensions
RUN apk add --no-cache libpq curl \
    && apk add --no-cache --virtual .build-deps $PHPIZE_DEPS postgresql-dev curl-dev \
    && docker-php-ext-install -j$(nproc) pdo_pgsql curl \
    && apk del .build-deps

# Add non-priveleged user
RUN addgroup -S phpuser \
    && adduser -S -D -G phpuser -u 10005 phpuser

COPY --chown=phpuser:phpuser ./router.php ./

USER phpuser

EXPOSE 8087
CMD ["php", "-S", "0.0.0.0:8087", "router.php"]
