FROM maven:3.9.9-amazoncorretto-21-debian-bookworm AS build

# Copy the project files into the container
COPY . /app

# Set the working directory inside the container
WORKDIR /app

# Build the Spring Boot application
RUN mvn clean package -DskipTests

# Use an openjdk image to run the application
FROM openjdk:21-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the JAR file from the build stage to the container
COPY --from=build /app/target/*.jar /app/app.jar

COPY src/main/resources/*.properties /app/

# Expose the application port
EXPOSE 8761

# Set the entry point to run the JAR with the specified profiles
ENTRYPOINT ["java", "-jar", "/app/app.jar"]