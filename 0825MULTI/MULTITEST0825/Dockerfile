# Stage 1: Build the application
FROM gradle:7.6-jdk17 AS build
WORKDIR /app

# Copy Gradle build files
COPY build.gradle settings.gradle ./
COPY gradle gradle

# Download dependencies (but don't build the project yet)
RUN gradle dependencies

# Copy the source code
COPY src src

# Build the application
RUN gradle build --no-daemon

# Stage 2: Run the application
FROM openjdk:17-jdk-slim
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/build/libs/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]
EXPOSE 8080
