FROM maven:sapmachine 

WORKDIR /app

COPY . .

RUN mvn package 

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "target/demo-0.0.1-SNAPSHOT.jar" ]

