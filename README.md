# Application d'Envoi d'E-mails avec Spring Boot (version SendGrid)

Une application Spring Boot simple qui démontre l'envoi d'e-mails en utilisant SendGrid.

## Structure du Projet

```
email-sender-app/
├── src/
│   └── main/
│       ├── java/com/example/emailsender/
│       │   ├── EmailSenderApplication.java
│       │   └── EmailController.java
│       └── resources/
│           ├── application.properties
│           └── static/
│               └── index.html
└── pom.xml
```

## Prérequis

- Java 17 ou supérieur
- Maven
- Un compte SendGrid et une clé API

## Configuration de SendGrid

Pour utiliser SendGrid, vous devez générer une clé API :

1. Inscrivez-vous pour un compte SendGrid : https://sendgrid.com/ . Inutile de créer un domaine, vous pouvez utiliser votre email de l'univ-jfc.fr comme expéditeur.
2. Connectez-vous et allez dans **Settings** > **API Keys**.
3. Cliquez sur **Create API Key**.
4. Donnez-lui un nom et sélectionnez **Full Access** ou **Restricted Access** (suffisant pour envoyer des mails).
5. Copiez la clé API générée immédiatement (elle ne sera plus affichée).

> [!NOTE]
> Il est également nécessaire de vérifier une "Sender Identity" (Identité d'Expéditeur) dans SendGrid (Settings > Sender Authentication) pour éviter que vos e-mails ne soient marqués comme spam. Utilisez votre email de l'univ-jfc.fr comme expéditeur.

## Configuration

Examinez la configuration dans le fichier `src/main/resources/application.properties` :

```properties
sendgrid.api-key=${SENDGRID_API_KEY}
sendgrid.from-email=${SENDGRID_FROM_EMAIL}
```

- `sendgrid.api-key` : Configuré pour utiliser la variable d'environnement `SENDGRID_API_KEY`.
- `sendgrid.from-email` : Configuré pour utiliser la variable d'environnement `SENDGRID_FROM_EMAIL`. L'adresse e-mail doit être validée dans votre compte SendGrid.

## Lancement de l'Application

1. Accédez au répertoire du projet :
   ```bash
   cd email-sender-app
   ```

2. Lancez l'application :

### Linux / macOS (Bash/Zsh)
```bash
SENDGRID_API_KEY=votre-cle-api-sendgrid SENDGRID_FROM_EMAIL=votre-email@exemple.com mvn spring-boot:run
```

### Windows 11 (PowerShell)
```powershell
$env:SENDGRID_API_KEY="votre-cle-api-sendgrid"; $env:SENDGRID_FROM_EMAIL="votre-email@exemple.com"; mvn spring-boot:run
```

### Windows (Invite de commandes)
```cmd
set SENDGRID_API_KEY=votre-cle-api-sendgrid && set SENDGRID_FROM_EMAIL=votre-email@exemple.com && mvn spring-boot:run
```

Remplacez `votre-cle-api-sendgrid` par votre véritable clé API SendGrid.

3. Ouvrez votre navigateur et allez sur :
   ```
   http://localhost:8080
   ```

## Utilisation

1. Remplissez le formulaire avec :
   - **To Email** : Adresse e-mail du destinataire
   - **Subject** : Objet de l'e-mail
   - **Message** : Corps du message

2. Cliquez sur "Send Email" (Envoyer l'e-mail)

3. Un message de succès ou d'erreur s'affichera après la tentative d'envoi.

## Caractéristiques

- Interface utilisateur simple et propre avec un dégradé en arrière-plan
- Validation du formulaire
- Affichage des messages de succès/erreur
- Utilise le SDK Java de SendGrid
- Configuré via des variables d'environnement pour plus de sécurité

## Déploiement sur Render

Cette application est prête à être déployée sur [Render](https://render.com) en utilisant Docker.

1. Créez un nouveau **Web Service** sur Render.
2. Connectez votre dépôt GitHub.
3. Choisissez **Docker** comme environnement d'exécution (Runtime).
4. Configurez les variables d'environnement suivantes dans Render (Settings > Environment) :
   - `SENDGRID_API_KEY` : Votre clé API SendGrid.
   - `SENDGRID_FROM_EMAIL` : Votre adresse e-mail d'expéditeur vérifiée.
5. Render détectera automatiquement le `Dockerfile` et lancera la construction et le déploiement.

## Technologies Utilisées

- Spring Boot 3.2.0
- SendGrid Java SDK 4.10.2
- Spring Boot Starter Web
- Maven
