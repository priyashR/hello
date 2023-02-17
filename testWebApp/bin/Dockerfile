# download the dependencies
FROM maven:3.5.3-jdk-8 AS mvncache
COPY pom.xml /usr/src/pom.xml
RUN mvn -f /usr/src/pom.xml dependency:resolve

# build and package the artifact 
FROM mvncache AS builder
COPY . /usr/src/
RUN mvn -f /usr/src/pom.xml package

# build the neat container with just what we want
FROM openjdk:8-alpine
COPY --from=builder /usr/src/target/testWebApp-0.0.1-SNAPSHOT.jar /usr/src/testWebApp/test.jar
EXPOSE 9991
WORKDIR /usr/src/testWebApp
CMD ["java", "-jar", "test.jar"]