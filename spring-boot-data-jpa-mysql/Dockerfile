# utilisation de l'image maven pour la construction
FROM maven AS build

# Définitir la répertoire de travaille
WORKDIR /app/myapp

# Copie du code source dans l'image de construction
COPY . .

# Construction du projet avec Maven
RUN mvn clean package -DskipTests

# Image pour executer le code java
FROM openjdk:17-alpine

# Definir la répertoire de travaille
WORKDIR /app

EXPOSE 8080

# Mise q jour des packages pour résoudre les vulnérabilités
RUN apk add --no-cache -l openssl zlib apk-tools libtasn1 busybox libretls


# Copie du fichier JAR généré depuis l'étape de construction
COPY --from=build /app/myapp/target/spring-boot-data-jpa*.jar app.jar

# Commande à exécuter lors du démarrage du conteneur
ENTRYPOINT ["java","-jar","app.jar"]