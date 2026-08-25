FROM maven:3.5-jdk-8 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn package -DskipTests

FROM eclipse-temurin:8-jre-jammy
WORKDIR /app
COPY --from=build /app/target/userFront-0.0.1-SNAPSHOT.jar app.jar
ENV DB_URL=jdbc:mysql://mysql:3306/onlinebanking?useSSL=false&allowPublicKeyRetrieval=true
ENV DB_USER=root
ENV DB_PASSWORD=changeme
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]
