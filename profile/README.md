<div align="center">

![Motasu](../Motasu%20logo%201.png)

![Status](https://img.shields.io/badge/Status-In%20Development-yellow?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Web%20%7C%20Mobile-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

## 🏁 Your SimRacing Social Network

> **Gather here to find new communities, meet friends, and compare your SimRacing achievements.**
> **Every car and track is your playground—show the world your pace!**

**Motasu** is a cross-platform social network designed specifically for the virtual racing community. Whether you are hot-lapping on the Nordschleife, drifting in Tsukuba, or competing in high-stakes GT3 leagues, Motasu connects your telemetry, your setups, and your passion with the world.

---

### 🚀 Project Overview

The goal of Motasu is to bridge the gap between different simulators (iRacing, ACC, rFactor 2) by providing a unified social hub.

**Key Features (Planned):**
* **📰 Activity Feed:** Just like your morning run, post your latest race results, new personal bests (PB), and track days. Follow your friends' progression in real-time.
* **📊 Unified Driver Profile:** Aggregate your stats from multiple simulators into one pro-looking card. Show off your safety ratings, win ratios, and favorite cars.
* **🎨 Livery Showcase:** A dedicated space to display your best car designs and artistic creations to the community.
* **🤝 Communities & Leagues:** Join groups, follow specific racing leagues, and stay updated on upcoming events.

### 🏗 Architecture

Motasu relies on a modern, decoupled architecture to ensure scalability and performance across devices.

* **Frontend (Mobile/Web):** A responsive client consuming the API.
* **Backend (API):** A robust RESTful API handling logic, data persistence, and telemetry ingestion.



### 👤 Author

**Corentin "Koroh" Richard**
* *Role:* Lead Developer & Architect
* *Github:* [@Koroh63]((https://github.com/Koroh63))
* *Contact:* koroh6@gmail.com

---

## 🎓 Contexte Académique : Réalisations Techniques & Sécurité

*Cette section détaille les implémentations réalisées dans le cadre du projet, couvrant les aspects de développement applicatif, d'architecture réseau et de sécurité.*

### 🌍 Accès & Environnements de Déploiement

L'application est déployée de manière automatisée sur une Machine Virtuelle (VM) et est accessible publiquement via des connexions sécurisées (HTTPS / Let's Encrypt) gérées par un reverse proxy **NGINX**.
* **Production :** [https://motasu.corentinkorohrichard.fr](https://motasu.corentinkorohrichard.fr)
* **Développement :** Environnement de staging isolé (`motasu-dev`).
* **Local :** L'ensemble de l'écosystème peut être instancié en local en lançant simultanément les fichiers `docker-compose.yaml` présents dans les dépôts de l'API et du client Web.

### 👥 Fonctionnalités Utilisateurs (Client Web Angular)
L'interface utilisateur a été conçue pour être fluide et réactive (SPA), en communiquant avec l'API GraphQL :
* **Authentification & Profil :** Création de compte sécurisée, connexion, et gestion de la suppression du compte.
* **Réseau Social :** Création de nouvelles publications dans le flux d'actualité, possibilité de supprimer ses propres posts, et consultation des profils détaillés des auteurs.
* **Expérience Utilisateur (UX) :** Implémentation d'un basculement dynamique entre le Mode Sombre et le Mode Clair.
* **Sécurité Frontend :** Mise en place de Guards de navigation vérifiant la validité locale et serveur des jetons de connexion (JWT) à chaque démarrage.

### ⚙️ Architecture Technique & CI/CD
L'infrastructure s'appuie sur une philosophie de conteneurisation et d'intégration continue :
* **Pipeline CI/CD :** Chaque nouvelle *Release* déclenche des workflows GitHub Actions automatisés. Ces pipelines construisent les images Docker optimisées, les poussent sur le registre, et ordonnent le déploiement sur la VM (dans les dossiers DEV ou PROD selon la branche).
* **Frontend Web :** Utilisation d'Angular avec un build Docker *Multi-stage*. L'application est compilée puis servie par un conteneur NGINX ultra-léger garantissant d'excellentes performances.
* **Backend API :** Serveur Node.js exploitant **Apollo Server (GraphQL)** pour des requêtes de données précises, connecté à une base de données **PostgreSQL** via l'ORM **Prisma**.

### 🔒 Sécurité & Standards (ANSSI)
La sécurité des données et des échanges a été pensée "Secure by Design", en s'inspirant des recommandations de l'ANSSI :
* **Chiffrement en Transit :** Toutes les communications Client-Serveur sont chiffrées de bout en bout via TLS (Certificats Let's Encrypt).
* **Stockage des Mots de Passe :** Les mots de passe ne sont jamais stockés en clair. Ils sont hachés de manière unilatérale via l'algorithme robuste `bcrypt` (intégrant un *salt* généré dynamiquement pour contrer les attaques par dictionnaire et tables arc-en-ciel).
* **Gestion de Session (JWT) :** L'authentification repose sur des JSON Web Tokens (stateless). La validation s'effectue en deux temps : vérification de l'expiration locale côté client, suivie d'une vérification stricte côté serveur (Query GraphQL `me`) pour prévenir l'accès par des comptes suspendus ou supprimés.

<br>
<br>

<div align="center">

Last updated: January 2026
<br>
Licensed under the <strong>GNU Affero General Public License v3.0</strong>

</div>
