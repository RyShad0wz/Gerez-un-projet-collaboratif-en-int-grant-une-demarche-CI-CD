FROM maven:3.6.3-jdk-11 AS build
WORKDIR /workspace
COPY pom.xml .
COPY src /workspace/src
RUN mvn -B -f pom.xml clean package -DskipTests
FROM eclipse-temurin:11-jdk-jammy
COPY --from=build /workspace/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
