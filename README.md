# TP 2 : Cloud

## Login

## Instructions
Durant ce TP, nous allons voir les trois types de cloud que nous avons vu durant les cours. Pour ce faire, nous allons déployer l'application PetClinic de trois manières différentes.

Voici à quoi ressemble l'architecture de l'application
![Architecture](https://spring-petclinic.github.io/images/petclinic-microservices-architecture.png "Architecture")

## 1 : Git
### 1.0 : Forker le repo du lab
Forker ce repository dans votre repository personnel.

### 1.1 : Cloner le repository
Clonez le repo nouvellement copié sur votre ordinateur 
> A partir de maintenant, **vous ne travaillerez plus que dans votre copie**. Vous n'avez plus à revenir sur [le projet parent](https://github.com/laurentgrangeau/lab-cloud).
 
### 1.2 : Créer une issue
> ⚠️  **WARNING**: Créez une issue s'intitulant `1.2` ayant pour contenu les commandes que vous avez effectuées pour réaliser le clone de votre repo git.

## 2 : IaaS
Dans un premier temps, nous allons déployer cette architecture sur une machine virtuelle.
> ⚠️  **WARNING**: Attention, toutes les commandes sont à réaliser dans un environnement type bash comme le terminal de MacOS, MINGW ou Git Bash

### 2.0 : Télécharger et installer la CLI d'Azure
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest

### 2.1 : Se connecter à Azure
Pour se connecter, lancer la commande suivante
```bash
az login --service-principal -u http://<login> -p <password> --tenant c8709a2a-70b6-49b5-bdd5-6868b476da85
```
Ou ```<login>``` est votre ID étudiant et le ```<password>``` correspondant.
Ces ```<login>``` et ```<password>``` se trouve dans le fichier ```password.txt```

### 2.2 : Créer une machine virtuelle Azure
Lancer la commande suivante
```bash
az vm create --name vm-<login> --resource-group rg-<login> --admin-username azureuser --generate-ssh-keys --image UbuntuLTS
```
Cette commande va créer une machine virtuelle dans votre environnement cloud dédié

### 2.3 : Se connecter à la machine
Une fois la machine virtuelle créée, se connecter à la machine
```bash
ssh azureuser@<public-ip>
```

### 2.4 : Installer les outils nécessaires
Installer ensuite les outils nécessaires au démarrage de l'application
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.4` ayant pour contenu les commandes que vous avez effectuées

### 2.5 : Cloner le repo Spring PetClinic
Cloner le repo PetClinic https://github.com/spring-projects/spring-petclinic
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.5` ayant pour contenu les commandes que vous avez effectuées

### 2.6 : Lancer Spring PetClinic
Lancer la commande suivante afin de compiler, puis lancer l'application
```bash
cd spring-petclinic
./mvnw package
java -jar target/*.jar
```

### 2.7 : Se connecter à l'application
Maintenant, se connecter à l'application
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.7` expliquant pourquoi il est impossible de se connecter à l'application

### 2.8 Ouvrir le firewall
Executer la commande suivante afin de récupérer le nom de la machine virtuelle
```bash
az vm list --query "[0].name"
```
Ensuite, ouvrir le firewall
```bash
az vm open-port --resource-group <resourcegroup> --name <vm-name> --port <port>
```
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.8` ayant pour contenu les commandes que vous avez effectuées

### 2.9 : Vérifier le bon fonctionnement
Ouvrir le navigateur et aller à l'url suivante afin de voir l'application Petclinic : ```http://<public-ip>:<port>```

### 2.10 : Installer MySQL
Installer ensuite MySQL sur le serveur
> ⚠️  **WARNING**: Créez une issue s'intitulant `2.10` ayant pour contenu les commandes que vous avez effectuées

### 2.11 : Installer les schémas et les données
Dans le repo git, il existe les instructions afin de créer la base de données PetClinic

### 2.12 : Redémarrer l'application
Redémarrer l'application PetClinic avec le bon profil afin que l'application puisse utiliser le serveur MySQL

## 3 : PaaS
Toutes les commandes à jouer sont à faire sur votre poste de travail, et non sur la machine virtuelle

### 3.1 : Cloner le repo
Récupérer le projet PetClinic : https://github.com/spring-projects/spring-petclinic

### 3.2 : Modifier le pom.xml
Modifier le fichier pom.xml afin d'ajouter le plugin Azure
> ⚠️  **WARNING**: Attention à bien modifier les balises ```<resourceGroup />```, ```<appServicePlanName />``` et ```<appName />```
```xml
<plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.8.0</version>
    <configuration>
        <schemaVersion>v2</schemaVersion>
        <resourceGroup>rg-<login></resourceGroup>
        <appServicePlanName>appservice-<login></appServicePlanName>
        <appName>web-<login></appName>
        <region>westeurope</region>
        <runtime>
            <os>linux</os>
            <javaVersion>jre8</javaVersion>
          </runtime>
          <deployment>
            <resources>
              <resource>
                <directory>${project.basedir}/target</directory>
                <includes>
                  <include>*.jar</include>
                </includes>
              </resource>
            </resources>
          </deployment>
          <stopAppDuringDeployment>true</stopAppDuringDeployment>
    </configuration>
</plugin>
```

### 3.3 : Recompilation
Recompiler et déployer le projet PetClinic
```bash
cd spring-petclinic
./mvnw package
./mvnw azure-webapp:deploy
```

Une fois le projet recompilé, il est disponiel à l'adresse suivante : ```https://<app-name>.azurewebsites.net```
### 3.4 : Vérifier que le projet fonctionne
Avez-vous bien accès à la page web de l'application ?

### 3.5 : Troubleshooting
Activer les logs et les traces sur Azure afin de pouvoir débugger
```bash
az webapp log config --name web-<login> --web-server-logging filesystem
```

Une fois les traces activées, vous pouvez voir les logs avec la commande suivante
```bash
az webapp log tail --name web-<login>
```

### 3.6 : La base de données
Comme vu durant le TP IaaS, l'application PetClinic peut-être associée à une base de données MySQL afin de persister les donneés.

Déployer une base de données Azure MySQL
```bash
az mysql create server --resource-group rg-<login> --name mysql-<login> --sku-name GP_Gen5_2 --ssl-enforcement Disabled --admin-user adminmysql --admin-password <your-password>
```

Ouvrir les ports vers l'extérieur
```bash
az mysql server firewall-rule create --resource-group rg-<login> --name mysql-firewall-<login> --server mysql-<login> --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```
### 3.7 : Schéma et base de données
Comme pour le TP IaaS, créer le schéma de base de données, ainsi que les données SQL

### 3.8 : Configuration
Changer la configuration de PetClinic dans le fichier ```spring-petclinic/src/main/resources/application-mysql.properties```

```java
# database init, supports mysql too
database=mysql
spring.datasource.url=${MYSQL_DB:jdbc:mysql://localhost/petclinic}
spring.datasource.username=${MYSQL_USER:petclinic@petclinicdb2}
spring.datasource.password=${MYSQL_PASS:petclinic}
# Uncomment this the first time the app runs
spring.datasource.initialization-mode=always
```
### 3.9 : Configuration de la webapp
```bash
az webapp config appsettings set -n web-<login> --settings SPRING_PROFILES_ACTIVE=mysql MYSQL_DB="jdbc:mysql://<dbname>.mysql.database.azure.com:3306/petclinic?useUnicode=true" MYSQL_USER="petclinicapp@<dbname>" MYSQL_PASS="<password>"
```

### 3.10 : Prise en compte
Redéployer l'application
```bash
./mvnw package
./mvnw azure-webapp:deploy
```

Et redémarrer la
```bash
az webapp restart -n web-<login>
```

Vous pouvez suivre le redémarrage de l'application avec la commande suivante
```bash
az webapp log tail --name web-<login>
```

### 3.11 : Vérification
Vérifier que les changements ont été pris en compte sur l'application
S'amuser à créer quelques vétérinaires

### 3.12 : Réponses
> ⚠️  **WARNING**: Pensez à bien remplir le fichier ```ANSWER.md```, à le commiter et le push dans votre repo

## 4 : Serverless

### 4.1 : Git
Cloner le projet Petclinic : https://github.com/spring-petclinic/spring-petclinic-rest

### 4.2 : Configuration
Modifier la configuration du ```pom.xml```
Ajouter le plugin Azure
```xml
<plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.8.0</version>
    <configuration>
        <schemaVersion>v2</schemaVersion>
        <resourceGroup>rg-<login></resourceGroup>
        <appServicePlanName>appservice-<login></appServicePlanName>
        <appName>rest-<login></appName>
        <region>westeurope</region>
        <runtime>
            <os>linux</os>
            <javaVersion>jre8</javaVersion>
          </runtime>
          <deployment>
            <resources>
              <resource>
                <directory>${project.basedir}/target</directory>
                <includes>
                  <include>*.jar</include>
                </includes>
              </resource>
            </resources>
          </deployment>
          <stopAppDuringDeployment>true</stopAppDuringDeployment>
    </configuration>
</plugin>
```
Et modifier les settings
```xml
        <java.version>1.8</java.version>
        <jacoco.version>0.8.4</jacoco.version>
```

### 4.3 : Déploiement
Compiler et déployer l'application
```bash
./mvnw package
./mvnw azure-webapp:deploy
```

### 4.4 : Vérification
Vérifier que l'application fonctionne. Aller à l'url du déploiement
```http://rest-<login>.azurewebsites.net/petclinic/api/```

### 4.5 : UI
Cloner le projet UI Petclinic : https://github.com/spring-petclinic/spring-petclinic-angular

### 4.6 : Installation des outils
Installer les outils nécessaires sur votre poste de travail
```bash
npm uninstall -g angular-cli @angular/cli
npm cache clean
npm install -g @angular/cli@latest
```
Puis, installer les packages nécessaires
```bash
npm install --save-dev @angular/cli@latest
npm install
```

### 4.7 : Développement
Modifier le code afin de pointer sur l'API précédemment déployée

Changer le fichier ```spring-petclinic-angular/src/environments/environment.prod.ts```
```ts
REST_API_URL: 'http://rest-<login>.azurewebsites.net/petclinic/api/'
```

### 4.8 : Compilation
Compiler ensuite l'application
```bash
ng build --prod --base-href=/ --deploy-url=/
```
### 4.9 : Déploiement
Créer le site web d'hébergement
```bash
az storage account create --name stor<login> --resource-group rg-<login> --kind StorageV2
az storage blob service-properties update --account-name stor<login> --static-website --404-document 404.html --index-document index.html
```
Puis déployer l'appplication dans un storage Azure
```bash
az storage blob upload-batch --source dist/ --destination \$web --account-name stor<login>
```

### 4.10 : Vérification
Vérifier que l'application fonctionne bien et retourne les bonnes données

Récupérer l'url du site avec la commande ```az storage account show --name stor<login> --query primaryEndpoints.web```