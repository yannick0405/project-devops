
Ce projet démontre le déploiement complet de l’application PayMyBuddy à l’aide de Docker, Docker Compose et d’un registre privé Docker.
L’objectif est de moderniser le déploiement, automatiser les environnements et améliorer la qualité des livraisons.

***

## Objectifs du projet

***
Déployer l’application **PayMyBuddy** avec Docker en respectant les bonnes pratiques DevOps :

-   utilisation des variables d’environnement
    
-   mise en place d’un **registre Docker privé**
    
-   documentation des commandes d’exécution et de test
    

----------

## 🐳 Technologies utilisées

-   Docker
    
-   Docker Compose
    
-   Java (Spring Boot)
    
-   MySQL
    
-   Docker Registry privé


## Gestion des variables d’environnement

Les variables sensibles sont stockées dans un fichier `.env`.

### `.env` (non versionné)

`MYSQL_ROOT_PASSWORD=rootpass
MYSQL_DATABASE=paymybuddy
MYSQL_USER=payuser
MYSQL_PASSWORD=paypass

SPRING_DATASOURCE_USERNAME=payuser
SPRING_DATASOURCE_PASSWORD=paypass` 

Un fichier `.env.example` est fourni pour référence.

----------

## 📦 Registre Docker privé

Un registre Docker privé est déployé avec une interface graphique.

### Lancement du registre

`docker compose -f docker-compose-registry.yml up -d` 

### Vérification du registre

`curl http://localhost:5000/v2/` 


Résultat attendu :

`{}` 

----------

## 🏷️ Build et push des images

### Build

`docker build -t paymybuddy-backend .
docker build -t paymybuddy-db .` 

### Tag

`docker tag paymybuddy-backend localhost:5000/paymybuddy-backend
docker tag paymybuddy-db localhost:5000/paymybuddy-db` 

### Push vers le registre privé

`docker push localhost:5000/paymybuddy-backend
docker push localhost:5000/paymybuddy-db` 

### Vérification des images

`curl http://localhost:5000/v2/_catalog` 



## 🚀 Lancement de l’application

`docker compose down -v
docker compose up` 

Services lancés :

-   MySQL (`paymybuddy-db`)
    
-   Backend Java (`paymybuddy-backend`)
    

----------

## 🖥️ Interface du registre

L’interface graphique du registre est fournie via **Docker Registry UI**.

⚠️ Dans un environnement distant (DockerLabs), l’interface peut ne pas être accessible via le navigateur.  
La présence des images est alors vérifiée via l’API du registre (`curl`).

----------

## ✅ Conclusion

Le projet respecte les consignes :

-   variables d’environnement via `.env`
    
-   registre Docker privé avec interface
    
-   images Docker centralisées
    
-   documentation claire des étapes
    

----------
