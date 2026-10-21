FROM golang:1.27.3-alpine3.24 AS build

WORKDIR /go/src/

COPY go.mod go.sum ./
RUN go mod download

COPY main.go .
RUN go build -o /go/src/catalog-service .

FROM alpine:3.24.2

WORKDIR /app/
RUN apk add --no-cache ca-certificates
COPY --from=build /go/src/catalog-service catalog-service

EXPOSE 8082
ENTRYPOINT ["/app/catalog-service"]