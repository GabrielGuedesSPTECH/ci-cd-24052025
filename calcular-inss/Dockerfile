FROM maven:3-amazoncorretto-21 as builder
LABEL authors="Guedes"

WORKDIR /build

COPY . .

RUN mvn clean package -DskipTests -DcheckStyle.skip=true

FROM eclipse-temurin:21-jdk-alpine

WORKDIR /app

COPY --from=builder /build/target/*.jar /app/app.jar

ENV JAVA_OPTS=""
ENV SPRING_PROFILES_ACTIVE=default

EXPOSE 8080

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar \
    --spring.profiles.active=${SPRING_PROFILES_ACTIVE}"]
