FROM maven:3.9-eclipse-temurin-21-alpine AS build
WORKDIR /app
ARG SERVICE_NAME
COPY ../services/${SERVICE_NAME}/pom.xml .
RUN mvn dependency:go-offline -B

COPY ../services/${SERVICE_NAME}/src ./src
RUN mvn clean install -B

COPY ../services/${SERVICE_NAME}/.env.properties ./.env.properties
RUN mvn clean package -DskipTests

FROM gcr.io/distroless/java21-debian12
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
COPY --from=build /app/.env.properties .env.properties
ENV SERVER_PORT=${PORT}
EXPOSE ${PORT}
ENTRYPOINT ["java", "-jar", "app.jar"]

# Execute na raiz do projeto
# docker build -f docker/dockerfiles/jdk21-distroless-mvn/Dockerfile --build-arg SERVICE_NAME=api-monolito --build-arg PORT=13000 -t api-monolito .

# Estrutura suposta
# Raiz/
# ├── docker/
# │   └── dockerfiles/
# │       └── jdk21-distroless-mvn/
# │       |   └── Dockerfile
# │       └── jdk21-distroless-gradle/
# │           └── Dockerfile
# └── services/
#     └── jdk21-service/
#         └── src/
#         └── pom.xml
#         └── .env.properties