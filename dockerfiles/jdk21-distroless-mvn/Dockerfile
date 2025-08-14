FROM maven:3.9.6-eclipse-temurin-21 AS build
ARG SERVICE_NAME
WORKDIR /app
COPY services/${SERVICE_NAME}/pom.xml .
COPY services/${SERVICE_NAME}/src ./src
RUN mvn clean package -DskipTests

FROM gcr.io/distroless/java21-debian12
COPY --from=build /app/target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]

# Execute na raiz do projeto
# docker build -f docker/{service_folder_name}/Dockerfile -t {service_name} .

# Estrutura suposta
# Raiz/
# ├── docker/
# │   └── dockerfiles/
# │       └── jdk21-distroless/
# │           └── Dockerfile
# └── services/
#     └── jdk21-service/
#         ├── pom.xml
#         └── src/