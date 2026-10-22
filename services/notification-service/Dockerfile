FROM ruby:3.4-slim-bookworm AS builder

WORKDIR /usr/src/notification-service

RUN apt-get update \
    && apt-get install -y \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*
    
COPY Gemfile Gemfile.lock ./
RUN gem install bundler -v 4.0.20 \
    && bundle _4.0.20_ install

COPY app.rb .

FROM ruby:3.4-slim-bookworm

WORKDIR /usr/src/notification-service/

RUN apt-get update \
    && apt-get install -y libpq5 \
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /usr/local/bundle /usr/local/bundle
COPY --from=builder /usr/src/notification-service/app.rb .

EXPOSE 8086
ENTRYPOINT ["bundle", "exec", "ruby", "app.rb"]
