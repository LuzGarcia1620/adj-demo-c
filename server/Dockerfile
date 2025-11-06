FROM maven:3.9.5-eclipse-temurin-21
WORKDIR /app
COPY . .
#mvn clean package -DskipTests = target/server-0.0.1-SNAPSHOT.jar
#el cp target/*.jar app.jar es para renombrar el archivo jar generado a un nombre mas simple
RUN mvn clean package -DskipTests &&  cp target/*.jar app.jar
EXPOSE 8080
#el ENTRYPOINT es para definir el comando que se ejecutara al iniciar el contenedor
ENTRYPOINT ["java","-jar","app.jar"]
