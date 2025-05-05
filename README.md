# **Softy Pinko - Docker, Nginx & Load Balancer**

Ce projet met en place une infrastructure Docker composée d’un front-end, d’un back-end API et d’un proxy Nginx. L’objectif est d’assurer une communication efficace entre ces services et d’ajouter un Load Balancer pour gérer la montée en charge des requêtes API.

## 📌 **Étapes réalisées**

### **1️⃣ Création et configuration du proxy Nginx**

-   Ajout du dossier `proxy/` contenant un `Dockerfile` et une configuration Nginx (`proxy.conf`).
-   Paramétrage du proxy pour rediriger les requêtes :
-   `/` → Front-end (`http://front-end:9000`).
-   `/api` → Back-end (`http://back-end:5252`).
-   Modification du `docker-compose.yml` pour intégrer le proxy.

### **2️⃣ Mise en place du projet Docker**

-   Création des services `front-end`, `back-end` et `proxy` dans `docker-compose.yml`.
-   Suppression des ports exposés directement pour les back-ends, tout passe par le proxy.
-   Construction et démarrage des conteneurs avec :
-   bash

docker-compose up --build -d

### **3️⃣ Mise en place du Load Balancer**

-   Création d’un dossier `task6/` en copiant `task5/`.
-   Ajout de **plusieurs instances du back-end** (`back-end-1` et `back-end-2`).
-   Modification de `proxy.conf` pour équilibrer les requêtes API :
-   nginx

upstream back-end {
    server back-end-1:5252;
    server back-end-2:5252;
}

-   Lancement des conteneurs avec le scaling :
-   bash

docker-compose up --scale back-end=2

### **4️⃣ Tests et validation**

-   Vérification du bon fonctionnement des conteneurs avec :
-   bash

docker ps

-   Test manuel des API servers pour s’assurer qu’ils répondent bien :
-   bash

curl -X GET http://back-end-1:5252/api/hello
curl -X GET http://back-end-2:5252/api/hello

-   Vérification du Load Balancer avec :
-   bash

bash -c 'for i in {1..10}; do curl -X GET http://localhost/api/hello; done'

-   ✅ **Les requêtes doivent alterner entre** `back-end-1` **et** `back-end-2`**.**