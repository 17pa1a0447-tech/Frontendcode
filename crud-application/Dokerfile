# build stage
FROM maven:3.9.0-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn -B -DskipTests package

# run stage
FROM eclipse-temurin:17-jdk-jammy
ARG JAR=/app/target/*.jar
COPY --from=build /app/target/*.jar /app/app.jar
EXPOSE 8080
# Accept spring.data.mongodb.uri from ENV
ENTRYPOINT ["sh","-c","java -Djava.security.egd=file:/dev/./urandom -jar /app/app.jar"]
