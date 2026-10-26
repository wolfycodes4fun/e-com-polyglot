FROM maven:3.10-eclipse-temurin-21-alpine AS builder

WORKDIR /usr/src/auth-service/

COPY pom.xml .
RUN mvn dependency:go-offline

COPY src ./src
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre-alpine

WORKDIR /usr/src/auth-service/

# Create non-privileged user to run application
RUN addgroup -S javauser \
    && adduser -S -D -G javauser -u 10005 javauser

COPY --from=builder --chown=javauser:javauser \
    /usr/src/auth-service/target/auth-service-1.0.0.jar ./auth-service.jar

USER javauser

EXPOSE 8081
ENTRYPOINT ["java", "-jar" , "auth-service.jar"]
