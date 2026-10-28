FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder

WORKDIR /usr/src/payment-service/

COPY payment-service.csproj .
RUN dotnet restore payment-service.csproj

COPY . .
RUN dotnet publish payment-service.csproj \
    --configuration Release \
    --runtime linux-x64 \
    --self-contained true \
    --output /app/publish

FROM ubuntu/dotnet-aspnet:8.0-24.04_stable

WORKDIR /usr/src/payment-service

COPY --from=builder --chown=app:app  /app/publish .

USER app

EXPOSE 8085
ENTRYPOINT ["./payment-service"]
