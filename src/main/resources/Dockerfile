# Step 1: Use a Maven image to build the app
FROM maven:3.9.6-eclipse-temurin-17 AS builder

# Set working directory inside the container
WORKDIR /app

# Copy all files into container
COPY . .

# Build the project and skip tests
RUN mvn clean package -DskipTests

# Step 2: Use a minimal JDK image to run the app
FROM eclipse-temurin:17-jdk-alpine

# Set working directory for runtime
WORKDIR /app

# Copy JAR file from builder image
COPY --from=builder /app/target/*.jar app.jar

# Expose the port (optional for documentation)
EXPOSE 8080

# Dynamic port support for platforms like Render
ENV PORT=8080

# Run the Spring Boot app
CMD ["java", "-jar", "app.jar"]
