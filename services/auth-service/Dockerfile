FROM maven:3.10-eclipse-temurin-21-alpine AS build

WORKDIR /usr/src/auth-service/
COPY . .

RUN mvn dependency:go-offline
RUN mvn clean package -DskipTests

FROM eclipse-temurin:25
WORKDIR /usr/src/auth-service/

COPY --from=build /usr/src/auth-service/target/auth-service-1.0.0.jar ./auth-service.jar

EXPOSE 8081
ENTRYPOINT ["java", "-jar" , "auth-service.jar"]
