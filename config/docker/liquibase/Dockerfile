FROM maven:3.3.9-jdk-8 AS build
COPY . /usr/src/app
RUN mvn -f /usr/src/app/liquibase/pom.xml clean package

FROM openjdk:8-jre-alpine

ENV APPLICATION_USER databaseuser
RUN adduser -D -g '' $APPLICATION_USER

RUN mkdir /app
RUN chown -R $APPLICATION_USER /app

USER $APPLICATION_USER

COPY --from=build /usr/src/app/liquibase/target/liquibase.jar /app/liquibase.jar

WORKDIR /app
CMD java -jar /app/liquibase.jar