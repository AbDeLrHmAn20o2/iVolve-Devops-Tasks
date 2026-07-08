From maven:3.9.16-eclipse-temurin-17-alpine AS build
WORKDIR /app
COPY . .
RUN mvn clean package


FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*jar app.jar
EXPOSE 8080
CMD ["java","-jar","app.jar"]
