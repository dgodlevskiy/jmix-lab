FROM bellsoft/liberica-openjdk-alpine:17 as builder

ARG jmix_premium_user
ARG jmix_premium_pass

ENV JMIX_PREMIUM_REPO_USER=${jmix_premium_user}
ENV JMIX_PREMIUM_REPO_PASS=${jmix_premium_pass}

WORKDIR /opt/app
COPY ./frontend/themes ./frontend/themes
COPY ./frontend/index.html ./frontend/index.html
COPY ./gradle ./gradle
COPY ./src ./src
COPY gradlew gradlew
COPY build.gradle build.gradle
COPY settings.gradle settings.gradle
RUN chmod +x ./gradlew
RUN ./gradlew -Pvaadin.productionMode=true bootJar

FROM bellsoft/liberica-openjdk-alpine:17
ARG JAR_FILE=build/libs/jmix-lab-0.0.1-SNAPSHOT.jar
COPY --from=builder /opt/app/build/libs/jmix-lab-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
