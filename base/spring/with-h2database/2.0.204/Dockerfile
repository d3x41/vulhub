FROM maven:3-jdk-8 AS builder

LABEL maintainer="phithon <root@leavesongs.com>"

COPY pom.xml /usr/src/pom.xml
COPY src /usr/src/src

WORKDIR /usr/src

RUN cd /usr/src; \
    mvn -U clean package -Dmaven.test.skip=true

FROM eclipse-temurin:8u302-b08-jre

LABEL maintainer="phithon <root@leavesongs.com>"

COPY --from=builder /usr/src/target/h2-console-demo-0.0.1-SNAPSHOT.jar /h2-console-demo-0.0.1-SNAPSHOT.jar

EXPOSE 8080 5005

CMD ["java", "-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005", "-jar", "/h2-console-demo-0.0.1-SNAPSHOT.jar"]
