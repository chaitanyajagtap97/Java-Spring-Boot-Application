FROM openjdk:8-jdk-alpine
#Base environment setup, version control
RUN addgroup -S wezvatech && adduser -S wezvatech -G wezvatech && mkdir -p /opt/wezva
#Security, non-root execution, container isolation
WORKDIR /opt/wezva
#Sets the default directory for all subsequent commands.
COPY target/wezva-springboot-docker-0.1.0.jar app.jar
#Copies the built artifact (JAR) from your local system into the container. Containers should always run pre-built artifacts, not raw code.
COPY app.properties app.properties
#Provides the application’s configuration file (set by devs).
COPY bootstrap.sh bootstrap.sh
#Copies the startup script that runs the application.
RUN chown -R wezvatech:wezvatech /opt/wezva && chmod +x bootstrap.sh
#Ensures correct ownership (wezvatech) and execution rights for the startup script. This avoids permission issues during runtime.
USER wezvatech
#Switches the container to run as the non-root user created earlier.
EXPOSE 8080
ENTRYPOINT ["/bin/sh", "bootstrap.sh"]
#Defines the main process for the container (here: bootstrap script → starts Spring Boot app). Without it, the container would start and exit immediately.
