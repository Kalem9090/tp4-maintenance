# --- Étape 1 : On construit l'application (Build) ---
# On utilise une image avec Maven et Java 17 pour compiler [cite: 24]
FROM maven:3.8.7-jdk-17 AS build

# On se place dans un dossier de travail
WORKDIR /app

# On copie le fichier de configuration Maven (pom.xml) et le code source
COPY pom.xml .
COPY src ./src

# On lance la compilation (en sautant les tests pour gagner du temps) [cite: 31]
RUN mvn clean package -DskipTests

# --- Étape 2 : On prépare l'image finale (Run) ---
# On repart d'une image très légère juste pour exécuter Java [cite: 27]
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# On récupère seulement le fichier .jar qu'on a fabriqué à l'étape 1
COPY --from=build /app/target/*.jar app.jar

# On dit que l'application écoute sur le port 8080 [cite: 55]
EXPOSE 8080

# La commande pour démarrer l'app quand le conteneur se lance
ENTRYPOINT ["java", "-jar", "app.jar"]