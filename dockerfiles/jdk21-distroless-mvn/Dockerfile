FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app
ARG SERVICE_NAME
ARG ENV_FILE

COPY ../services/${SERVICE_NAME}/pom.xml .
RUN --mount=type=cache,target=/root/.m2 mvn dependency:go-offline -B

COPY ../services/${SERVICE_NAME}/src ./src
COPY ../services/${SERVICE_NAME}/${ENV_FILE} ./${ENV_FILE}

RUN --mount=type=cache,target=/root/.m2 mvn clean package -DskipTests

FROM gcr.io/distroless/java21-debian12
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
COPY --from=build /app/${ENV_FILE} ${ENV_FILE}
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