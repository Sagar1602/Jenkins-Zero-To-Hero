# Use Java 17 runtime (adjust to 11 only if your app needs it)
FROM eclipse-temurin:17-jre-alpine

WORKDIR /opt/app

# Copies the fat jar built by Maven. The wildcard handles versioned filenames.
# If you DO have a fixed name (e.g., spring-boot-web.jar), replace the wildcard accordingly.
COPY target/*.jar app.jar

# Optional but nice-to-have:
EXPOSE 8080
HEALTHCHECK --interval=30s --timeout=3s --start-period=30s --retries=3 \
  CMD wget -qO- http://localhost:8080/actuator/health | grep -q '"status":"UP"' || exit 1

# Run as non-root
RUN adduser -D appuser
USER appuser

# Start
ENTRYPOINT ["java","-jar","/opt/app/app.jar"]
