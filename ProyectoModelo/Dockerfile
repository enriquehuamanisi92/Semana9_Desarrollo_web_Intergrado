FROM maven:3.9.9-eclipse-temurin-21 AS build
WORKDIR /app

# 1. Copiar solo el pom.xml y descargar las dependencias primero
COPY pom.xml .
RUN mvn dependency:go-offline -B

# 2. Luego copiar el código y compilar (así no descargas todo de nuevo)
COPY src ./src
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
