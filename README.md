# TP 3.1 & TP 3.2 – Spring Cloud Config & Actuator

## Description

Ce projet met en œuvre la **centralisation de la configuration** des microservices avec **Spring Cloud Config** et le **monitoring** ainsi que le **rechargement dynamique** de la configuration avec **Spring Boot Actuator**.
La configuration est externalisée dans un **repository GitHub** et consommée dynamiquement par un microservice Produits.

## Architecture

Le système est composé de :

1. **Config Server**

   * Serveur centralisé de configuration
   * Lit les fichiers depuis GitHub
   * Port : 9101

2. **Microservice Produits**

   * API REST
   * Consomme la configuration externe
   * Actuator activé
   * Port : 9001

## Fonctionnalités

* Centralisation des fichiers de configuration
* Chargement dynamique des propriétés au démarrage
* Limitation du nombre de produits via une propriété externalisée
* Monitoring du microservice
* Rafraîchissement de la configuration sans redémarrage
* Vérification de l’état de santé du service

## Endpoints principaux

### Config Server

* `GET /microservice-produits/default`

### Microservice Produits

* `GET /Produits` : liste des produits

### Actuator

* `GET /actuator`
* `GET /actuator/health`
* `POST /actuator/refresh`

## Configuration

* Les propriétés sont stockées dans un repository GitHub
* Exemple :

```properties
mes-configs.limitDeProduits=3
```

* Le microservice utilise `bootstrap.properties` pour se connecter au Config Server

## Exécution

### Démarrer le Config Server

```bash
cd config-server
mvn spring-boot:run
```

### Démarrer le microservice Produits

```bash
cd microservice-produits
mvn spring-boot:run
```

## Tests

1. Vérifier la configuration :

   ```
   http://localhost:9101/microservice-produits/default
   ```
2. Vérifier les produits :

   ```
   http://localhost:9001/Produits
   ```
3. Tester Actuator :

   ```
   http://localhost:9001/actuator
   http://localhost:9001/actuator/health
   ```
4. Rafraîchir la configuration :

   ```bash
   curl -X POST http://localhost:9001/actuator/refresh
   ```

## Screen

<img width="763" height="713" alt="Capture d&#39;écran 2025-12-14 171006" src="https://github.com/user-attachments/assets/9807616f-f380-43af-91d9-de6fc3654eb8" />
<img width="908" height="386" alt="Capture d&#39;écran 2025-12-14 171114" src="https://github.com/user-attachments/assets/aaae4c1a-e969-43f3-987b-d5151045052a" />

![1](https://github.com/user-attachments/assets/ea81e220-702a-4e79-b77a-bafa0fb12cc0)
![2](https://github.com/user-attachments/assets/7f8775b0-6ccf-4777-9e36-fe47ba291ed8)
![3](https://github.com/user-attachments/assets/252b3bc5-fd33-41e7-84f2-6afad329e88b)
![5](https://github.com/user-attachments/assets/110ee900-8e82-4f99-9889-c5081dc2362c)
![6](https://github.com/user-attachments/assets/41461195-12a1-4d72-950c-c5491b1da8cc)
![7](https://github.com/user-attachments/assets/8acba1d4-533f-42cf-8b25-7aed99f3b164)
![8](https://github.com/user-attachments/assets/2b7b542c-925d-4b87-9280-2dc51ae561c5)
![9](https://github.com/user-attachments/assets/353de63a-30ca-49cb-b120-e1c04a508185)

## Objectifs pédagogiques

* Comprendre la configuration centralisée
* Découpler le code et la configuration
* Superviser un microservice
* Recharger la configuration à chaud
* Utiliser Spring Cloud dans une architecture microservices

---

**MOHAMMED EL KHAYATI & MOUAD MOUDID --5IIR11**
