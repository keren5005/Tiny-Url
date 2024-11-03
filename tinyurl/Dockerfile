# Use OpenJDK 11 as the base image
FROM openjdk:11

# Set the working directory
WORKDIR /usr/src/app

# Copy the JAR file into the container
COPY target/tinyurl-0.0.1-SNAPSHOT.jar /usr/src/app/chatbot.jar

# Copy the application.properties file into a specific configuration path
COPY src/main/resources/application.properties /opt/conf/application.properties

# Run the application with the custom configuration path
CMD ["java", "-jar", "/usr/src/app/chatbot.jar", "--spring.config.location=file:/opt/conf/application.properties"]
