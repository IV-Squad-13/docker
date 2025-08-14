FROM gradle:jdk-21-and-22-alpine AS build
ARG SERVICE_NAME
WORKDIR /app
COPY services/${SERVICE_NAME}/ . 
RUN gradle clean build -x test

FROM gcr.io/distroless/java21-debian12
COPY --from=build /app/build/libs/*.jar app.jar
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