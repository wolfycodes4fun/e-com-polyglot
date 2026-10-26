FROM golang:1.27.3-alpine3.24 AS builder

WORKDIR /usr/src/catalog-service/

COPY . .
RUN go mod tidy

RUN go build -o /app/catalog-service .

FROM alpine:3.24.2

WORKDIR /usr/src/catalog-service/

RUN apk add --no-cache ca-certificates

# Create non-privileged user to run service
RUN addgroup -S gouser \
    && adduser -S -D -G gouser -u 10005 gouser

COPY --from=builder --chown=gouser:gouser /app/catalog-service .

USER gouser

EXPOSE 8082
ENTRYPOINT ["/usr/src/catalog-service/catalog-service"]
