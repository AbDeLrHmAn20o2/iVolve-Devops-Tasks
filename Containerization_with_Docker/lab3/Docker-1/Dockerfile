From maven:3.9.9-eclipse-temurin-17
WORKDIR /app1
COPY . .
RUN mvn package
EXPOSE 8080
CMD ["java","-jar","target/demo-0.0.1-SNAPSHOT.jar"]
