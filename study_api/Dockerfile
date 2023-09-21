# START BUILD
FROM maven:3.8.3-jdk-11-slim AS build

RUN mkdir /project

COPY . /project

WORKDIR /project

RUN mvn clean package

# END BUILD

# START RUN
FROM adoptopenjdk/openjdk11:jre-11.0.15_10-alpine

RUN mkdir /app

COPY --from=build /project/target/app.jar /app/app.jar
COPY src/main/resources/application-dev.properties /app/application-dev.properties

WORKDIR /app

EXPOSE 8080

CMD java -jar app.jar