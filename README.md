# 🌍 Jungle in English - Plateforme d'Apprentissage de l'Anglais

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.0-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Angular](https://img.shields.io/badge/Angular-18.2-red.svg)](https://angular.io/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue.svg)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)

## 📖 Table des Matières

- [À Propos](#-à-propos)
- [Architecture](#-architecture)
- [Technologies](#-technologies)
- [Fonctionnalités](#-fonctionnalités)
- [Prérequis](#-prérequis)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Démarrage](#-démarrage)
- [Documentation API](#-documentation-api)
- [Monitoring](#-monitoring)
- [Tests](#-tests)
- [Structure du Projet](#-structure-du-projet)
- [Contribution](#-contribution)
- [Support](#-support)
- [Licence](#-licence)

## 🎯 À Propos

**Jungle in English** est une plateforme complète d'apprentissage de l'anglais développée avec une architecture microservices moderne. La plateforme offre une expérience d'apprentissage interactive avec des cours, des clubs, des événements, un système de gamification, et bien plus encore.

### Objectifs du Projet

- 🎓 Faciliter l'apprentissage de l'anglais de manière interactive
- 👥 Créer une communauté d'apprenants engagés
- 📊 Suivre les progrès avec un système de gamification
- 🎯 Offrir des cours adaptés à tous les niveaux
- 🤝 Permettre l'interaction entre étudiants et tuteurs

## 🏗️ Architecture

Jungle in English utilise une **architecture microservices** avec les composants suivants :

```
┌─────────────────────────────────────────────────────────────┐
│                      Frontend (Angular)                      │
│                     Port: 4200 / 80                          │
└──────────────────────────┬──────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                   API Gateway (Spring Cloud)                 │
│                        Port: 8080                            │
└──────────────────────────┬──────────────────────────────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
┌───────▼────────┐ ┌──────▼──────┐ ┌────────▼────────┐
│ Eureka Server  │ │   Config    │ │   Microservices │
│   Port: 8761   │ │   Server    │ │   (13 services) │
└────────────────┘ └─────────────┘ └─────────────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
┌───────▼────────┐ ┌──────▼──────┐ ┌────────▼────────┐
│   PostgreSQL   │ │    Redis    │ │   Monitoring    │
│   Port: 5432   │ │  Port: 6379 │ │  (Prometheus,   │
│                │ │             │ │   Grafana, etc) │
└────────────────┘ └─────────────┘ └─────────────────┘
```

### Microservices

| Service | Port | Description | Base de Données |
|---------|------|-------------|-----------------|
| **API Gateway** | 8080 | Point d'entrée unique, routage et sécurité | - |
| **Eureka Server** | 8761 | Service discovery et registration | - |
| **Config Server** | 8888 | Configuration centralisée | - |
| **Auth Service** | 8081 | Authentification, autorisation, gestion utilisateurs | `jungle_identity` |
| **Community Service** | 8082 | Forum, discussions, catégories | `jungle_community` |
| **Learning Service** | 8083 | Parcours d'apprentissage, progression | `jungle_learning_db` |
| **Messaging Service** | 8084 | Chat en temps réel, notifications | `jungle_messaging_db` |
| **Club Service** | 8085 | Gestion des clubs d'apprentissage | `jungle_club_db` |
| **Courses Service** | 8086 | Cours, modules, contenus pédagogiques | `jungle_courses` |
| **Complaints Service** | 8087 | Gestion des réclamations | `jungle_complaints` |
| **Event Service** | 8088 | Événements, calendrier, inscriptions | `jungle_event_db` |
| **Payment Service** | 8089 | Paiements, abonnements | `jungle_payment` |
| **Exam Service** | 8090 | Examens, quiz, évaluations | `jungle_exams` |
| **Gamification Service** | 8091 | Points, badges, classements | `jungle_gamification` |
| **Sponsors Service** | 8092 | Gestion des sponsors et partenaires | `jungle_sponsors_db` |
| **WebRTC Signaling** | 3001 | Signalisation pour visioconférence | - |

## 🛠️ Technologies

### Backend

- **Framework:** Spring Boot 3.2.0
- **Langage:** Java 17
- **Architecture:** Microservices avec Spring Cloud
- **Service Discovery:** Netflix Eureka
- **API Gateway:** Spring Cloud Gateway
- **Sécurité:** Spring Security 6 + JWT
- **Base de données:** PostgreSQL 15
- **Cache:** Redis 7
- **ORM:** Spring Data JPA / Hibernate
- **Documentation API:** Swagger/OpenAPI 3.0
- **Messaging:** WebSocket, STOMP, SockJS
- **Build:** Maven

### Frontend

- **Framework:** Angular 18.2
- **Langage:** TypeScript 5.5
- **UI Components:** Angular Material, Bootstrap 5
- **Styling:** TailwindCSS 3.4
- **Charts:** ApexCharts, Chart.js, AmCharts5
- **Rich Text:** TinyMCE, Quill
- **Calendar:** FullCalendar
- **Maps:** Leaflet
- **Real-time:** Socket.io, STOMP
- **HTTP Client:** RxJS
- **Forms:** Reactive Forms
- **Notifications:** SweetAlert2

### Infrastructure & DevOps

- **Containerisation:** Docker & Docker Compose
- **Monitoring:** Prometheus, Grafana
- **Logging:** Loki, Promtail, Logstash
- **Tracing:** Jaeger
- **Container Monitoring:** cAdvisor
- **Reverse Proxy:** Nginx
- **CI/CD:** Configuration prête pour pipelines
- **Quality:** SonarQube/SonarCloud

## ✨ Fonctionnalités

### 🔐 Authentification & Autorisation
- Inscription et connexion avec JWT
- OAuth2 avec Google
- Gestion des rôles (STUDENT, TUTOR, ACADEMIC_OFFICE_AFFAIR, ADMIN)
- Vérification par email
- Réinitialisation de mot de passe
- Gestion des sessions
- Protection reCAPTCHA
- Rate limiting sur les tentatives de connexion

### 📚 Gestion des Cours
- Création et gestion de cours multi-niveaux
- Modules et chapitres structurés
- Upload de ressources (PDF, vidéos, documents)
- Suivi de progression
- Système de notation
- Certificats de complétion

### 👥 Clubs d'Apprentissage
- Création de clubs par niveau (Beginner, Intermediate, Advanced)
- Gestion des membres et rôles (President, Vice-President, Member)
- Planification de sessions
- Système de tâches
- Workflow d'approbation
- Cache optimisé pour les performances

### 💬 Forum Communautaire
- Catégories et sous-catégories
- Topics et posts avec pagination
- Système de réactions (Like, Helpful, Insightful)
- Recherche full-text
- Topics épinglés et verrouillés
- Modération

### 📅 Événements
- Création et gestion d'événements
- Calendrier interactif
- Inscriptions et participants
- Notifications de rappel
- Intégration Google Calendar

### 💬 Messagerie
- Chat en temps réel (WebSocket)
- Messages privés et groupes
- Notifications push
- Historique des conversations
- Upload de fichiers

### 🎮 Gamification
- Système de points et XP
- Badges et achievements
- Classements (leaderboards)
- Défis et quêtes
- Récompenses

### 💳 Paiements
- Gestion des abonnements
- Paiements sécurisés
- Historique des transactions
- Factures

### 📝 Examens & Quiz
- Création d'examens
- Questions à choix multiples
- Correction automatique
- Statistiques de performance
- Certificats

### 🎥 Visioconférence
- Sessions vidéo WebRTC
- Partage d'écran
- Chat intégré
- Enregistrement de sessions

### 📊 Monitoring & Analytics
- Métriques en temps réel (Prometheus)
- Dashboards Grafana
- Logs centralisés (Loki)
- Tracing distribué (Jaeger)
- Alertes automatiques

## 📋 Prérequis

### Pour le développement local

- **Java:** JDK 17 ou supérieur
- **Node.js:** v18 ou supérieur
- **npm:** v9 ou supérieur
- **Maven:** 3.6 ou supérieur
- **PostgreSQL:** 15 ou supérieur
- **Redis:** 7 ou supérieur (optionnel)
- **Git:** Pour le contrôle de version

### Pour Docker

- **Docker:** 20.10 ou supérieur
- **Docker Compose:** 2.0 ou supérieur

## 🚀 Installation

### 1. Cloner le Repository

```bash
git clone https://github.com/votre-organisation/jungle-in-english.git
cd jungle-in-english
```

### 2. Configuration des Variables d'Environnement

Copier le fichier d'exemple et le configurer :

```bash
cp .env.example .env
```

Éditer `.env` avec vos valeurs :

```env
# JWT Configuration
JWT_SECRET=votre-secret-jwt-minimum-256-bits

# Email Configuration
MAIL_USERNAME=votre-email@gmail.com
MAIL_PASSWORD=votre-mot-de-passe-application

# Google OAuth2
GOOGLE_CLIENT_ID=votre-client-id
GOOGLE_CLIENT_SECRET=votre-client-secret

# reCAPTCHA
RECAPTCHA_SECRET=votre-secret-recaptcha

# Database (si développement local)
DB_PASSWORD=votre-mot-de-passe-postgres
```

### 3. Installation avec Docker (Recommandé)

```bash
# Démarrer tous les services
cd devops/docker
docker-compose up -d

# Vérifier le statut des services
docker-compose ps

# Voir les logs
docker-compose logs -f
```

### 4. Installation Manuelle (Développement)

#### Backend

```bash
# Créer les bases de données PostgreSQL
psql -U postgres -f devops/database/init-databases.sql

# Démarrer Redis (optionnel)
redis-server

# Compiler et démarrer chaque service
cd backend/eureka-server
mvn clean install
mvn spring-boot:run

# Répéter pour chaque service dans l'ordre :
# 1. eureka-server
# 2. config-server
# 3. api-gateway
# 4. auth-service
# 5. autres services...
```

#### Frontend

```bash
cd frontend
npm install
npm start

# L'application sera disponible sur http://localhost:4200
```

## ⚙️ Configuration

### Configuration Backend

Chaque microservice possède son propre fichier `application.properties` ou `application.yml` dans `src/main/resources/`.

Exemple pour Auth Service (`backend/auth-service/src/main/resources/application.properties`) :

```properties
# Server Configuration
server.port=8081

# Database
spring.datasource.url=jdbc:postgresql://localhost:5432/jungle_identity
spring.datasource.username=postgres
spring.datasource.password=${DB_PASSWORD}

# JWT
jwt.secret=${JWT_SECRET}
jwt.expiration=900000

# Eureka
eureka.client.service-url.defaultZone=http://localhost:8761/eureka/
```

### Configuration Frontend

Fichier `frontend/src/environments/environment.ts` :

```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:8080',
  wsUrl: 'ws://localhost:8080/ws',
  recaptchaSiteKey: 'votre-site-key'
};
```

## 🎬 Démarrage

### Avec Docker Compose (Production-like)

```bash
# Démarrer l'infrastructure complète
cd devops/docker
docker-compose up -d

# Attendre que tous les services soient prêts (environ 2-3 minutes)
docker-compose logs -f | grep "Started"

# Accéder à l'application
# Frontend: http://localhost:4200
# API Gateway: http://localhost:8080
# Eureka Dashboard: http://localhost:8761
# Grafana: http://localhost:3000 (admin/admin)
# Prometheus: http://localhost:9090
# Jaeger: http://localhost:16686
```

### Développement Local

```bash
# Terminal 1 - Eureka Server
cd backend/eureka-server && mvn spring-boot:run

# Terminal 2 - API Gateway
cd backend/api-gateway && mvn spring-boot:run

# Terminal 3 - Auth Service
cd backend/auth-service && mvn spring-boot:run

# Terminal 4 - Autres services selon besoin
cd backend/courses-service && mvn spring-boot:run

# Terminal 5 - Frontend
cd frontend && npm start
```

### Ordre de Démarrage Recommandé

1. **Infrastructure:** PostgreSQL, Redis
2. **Service Discovery:** Eureka Server (8761)
3. **Configuration:** Config Server (8888)
4. **Gateway:** API Gateway (8080)
5. **Services métier:** Auth, Courses, Community, etc.
6. **Frontend:** Angular (4200)

## 📚 Documentation API

### Swagger UI

Chaque microservice expose sa documentation Swagger :

- **Auth Service:** http://localhost:8081/swagger-ui.html
- **Courses Service:** http://localhost:8086/swagger-ui.html
- **Community Service:** http://localhost:8082/swagger-ui.html
- **Club Service:** http://localhost:8085/swagger-ui.html
- **Event Service:** http://localhost:8088/swagger-ui.html
- **Gamification Service:** http://localhost:8091/swagger-ui.html

### OpenAPI JSON

- **Auth Service:** http://localhost:8081/api-docs
- **Courses Service:** http://localhost:8086/api-docs

### Postman Collection

Une collection Postman est disponible pour Auth Service :

```bash
backend/auth-service/postman_collection.json
```

### Documentation Détaillée

- [Auth Service Documentation](backend/auth-service/docs/README.md)
- [Club Service Documentation](backend/club-service/README.md)
- [Community Service Documentation](backend/community-service/README.md)

## 📊 Monitoring

### Prometheus

Accéder aux métriques : http://localhost:9090

Métriques disponibles :
- Latence des requêtes HTTP
- Utilisation mémoire JVM
- Connexions base de données
- Statistiques du cache
- Métriques custom par service

### Grafana

Accéder aux dashboards : http://localhost:3000

**Identifiants par défaut :** admin / admin

Dashboards disponibles :
- Vue d'ensemble de la plateforme
- Métriques par microservice
- Performance base de données
- Utilisation des ressources
- Logs en temps réel

### Jaeger (Distributed Tracing)

Accéder à l'interface : http://localhost:16686

Fonctionnalités :
- Traçage des requêtes inter-services
- Analyse de latence
- Détection de goulots d'étranglement
- Visualisation des dépendances

### Logs

Les logs sont centralisés avec Loki et accessibles via Grafana.

Logs locaux disponibles dans :
```
backend/auth-service/logs/
backend/club-service/logs/
backend/community-service/logs/
```

## 🧪 Tests

### Tests Backend

```bash
# Exécuter tous les tests d'un service
cd backend/auth-service
mvn test

# Tests avec rapport de couverture
mvn test jacoco:report
open target/site/jacoco/index.html

# Tests d'intégration uniquement
mvn verify -P integration-tests
```

### Tests Frontend

```bash
cd frontend

# Tests unitaires
npm test

# Tests avec couverture
npm run test:coverage

# Tests end-to-end
npm run e2e
```

### Objectifs de Couverture

- **Backend:** Minimum 80% de couverture
- **Frontend:** Minimum 70% de couverture

## 📁 Structure du Projet

```
jungle-in-english/
├── backend/                      # Services backend
│   ├── api-gateway/             # API Gateway (Spring Cloud Gateway)
│   ├── eureka-server/           # Service Discovery
│   ├── config-server/           # Configuration centralisée
│   ├── auth-service/            # Authentification & Autorisation
│   ├── courses-service/         # Gestion des cours
│   ├── club-service/            # Gestion des clubs
│   ├── community-service/       # Forum communautaire
│   ├── learning-service/        # Parcours d'apprentissage
│   ├── messaging-service/       # Messagerie temps réel
│   ├── event-service/           # Gestion des événements
│   ├── exam-service/            # Examens et quiz
│   ├── gamification-service/    # Système de gamification
│   ├── payment-service/         # Paiements
│   ├── complaints-service/      # Réclamations
│   ├── sponsors-service/        # Gestion des sponsors
│   └── webrtc-signaling/        # Signalisation WebRTC (Node.js)
│
├── frontend/                     # Application Angular
│   ├── src/
│   │   ├── app/                 # Composants et modules
│   │   ├── assets/              # Ressources statiques
│   │   ├── environments/        # Configuration par environnement
│   │   └── styles/              # Styles globaux
│   ├── angular.json             # Configuration Angular
│   ├── package.json             # Dépendances npm
│   └── tailwind.config.js       # Configuration TailwindCSS
│
├── devops/                       # Configuration DevOps
│   ├── docker/
│   │   ├── docker-compose.yml   # Orchestration des services
│   │   └── docker-compose.prod.yml
│   ├── database/
│   │   └── init-databases.sql   # Scripts d'initialisation DB
│   └── monitoring/
│       ├── prometheus.yml       # Configuration Prometheus
│       ├── grafana/             # Dashboards Grafana
│       ├── loki-config.yml      # Configuration Loki
│       └── promtail-config.yml  # Configuration Promtail
│
├── .sonarqube/                   # Configuration SonarQube
├── .env.example                  # Template variables d'environnement
├── Makefile                      # Commandes utilitaires
├── sonar-project.properties      # Configuration SonarCloud
└── README.md                     # Ce fichier
```

### Structure d'un Microservice Type

```
service-name/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/jungle/service/
│   │   │       ├── config/          # Configuration Spring
│   │   │       ├── controller/      # REST Controllers
│   │   │       ├── dto/             # Data Transfer Objects
│   │   │       ├── entity/          # JPA Entities
│   │   │       ├── exception/       # Custom Exceptions
│   │   │       ├── mapper/          # MapStruct Mappers
│   │   │       ├── repository/      # Spring Data Repositories
│   │   │       ├── service/         # Business Logic
│   │   │       └── ServiceApplication.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── application-docker.properties
│   └── test/                        # Tests unitaires et d'intégration
├── Dockerfile                       # Image Docker
├── pom.xml                          # Dépendances Maven
└── README.md                        # Documentation du service
```

## 🤝 Contribution

Nous accueillons les contributions ! Voici comment participer :

### 1. Fork le Projet

```bash
git clone https://github.com/votre-username/jungle-in-english.git
cd jungle-in-english
```

### 2. Créer une Branche

```bash
git checkout -b feature/ma-nouvelle-fonctionnalite
```

### 3. Développer et Tester

```bash
# Faire vos modifications
# Ajouter des tests
mvn test  # Backend
npm test  # Frontend
```

### 4. Commit et Push

```bash
git add .
git commit -m "feat: ajout de ma nouvelle fonctionnalité"
git push origin feature/ma-nouvelle-fonctionnalite
```

### 5. Créer une Pull Request

Ouvrez une PR sur GitHub avec une description détaillée de vos changements.

### Conventions de Code

#### Backend (Java)
- Suivre les conventions Java standard
- Utiliser Lombok pour réduire le boilerplate
- Documenter les méthodes publiques avec Javadoc
- Écrire des tests unitaires pour toute nouvelle fonctionnalité
- Utiliser les exceptions personnalisées

#### Frontend (Angular/TypeScript)
- Suivre le style guide Angular officiel
- Utiliser TypeScript strict mode
- Composants réutilisables et modulaires
- Services pour la logique métier
- RxJS pour la programmation réactive

### Conventions de Commit

Utiliser [Conventional Commits](https://www.conventionalcommits.org/) :

- `feat:` Nouvelle fonctionnalité
- `fix:` Correction de bug
- `docs:` Documentation
- `style:` Formatage, point-virgules manquants, etc.
- `refactor:` Refactoring de code
- `test:` Ajout de tests
- `chore:` Maintenance

## 📞 Support

### Documentation

- [Guide de Démarrage Rapide](GUIDE_DEMO_COMPLET.md)
- [Documentation Auth Service](backend/auth-service/docs/README.md)
- [Documentation API](http://localhost:8080/swagger-ui.html)

### Problèmes Courants

#### Les services ne démarrent pas

```bash
# Vérifier les logs
docker-compose logs service-name

# Redémarrer un service spécifique
docker-compose restart service-name

# Reconstruire les images
docker-compose build --no-cache
docker-compose up -d
```

#### Erreurs de connexion à la base de données

```bash
# Vérifier que PostgreSQL est démarré
docker-compose ps postgres

# Vérifier les logs PostgreSQL
docker-compose logs postgres

# Recréer la base de données
docker-compose down -v
docker-compose up -d postgres
```

#### Problèmes de cache

```bash
# Vider le cache Redis
docker-compose exec redis redis-cli FLUSHALL

# Redémarrer Redis
docker-compose restart redis
```

### Contact

- **Email:** support@jungleinenglish.com
- **GitHub Issues:** [https://github.com/votre-organisation/jungle-in-english/issues](https://github.com/votre-organisation/jungle-in-english/issues)
- **Documentation:** [Wiki du projet](https://github.com/votre-organisation/jungle-in-english/wiki)

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 🎯 Roadmap

### Version 1.0 (Actuelle)
- ✅ Architecture microservices complète
- ✅ Authentification et autorisation
- ✅ Gestion des cours et clubs
- ✅ Forum communautaire
- ✅ Système de gamification
- ✅ Monitoring et observabilité

### Version 1.1 (En cours)
- ⏳ Tests unitaires et d'intégration (80%+ couverture)
- ⏳ Authentification à deux facteurs (2FA)
- ⏳ Notifications push mobiles
- ⏳ Export de données utilisateur

### Version 2.0 (Planifiée)
- 📋 Application mobile (React Native)
- 📋 Intelligence artificielle pour recommandations
- 📋 Système de tutorat en direct
- 📋 Marketplace de cours
- 📋 Intégration avec plateformes externes

---

## 🙏 Remerciements

Merci à tous les contributeurs qui ont participé à ce projet !

- **Équipe Backend:** Développement des microservices
- **Équipe Frontend:** Interface utilisateur Angular
- **Équipe DevOps:** Infrastructure et monitoring
- **Équipe QA:** Tests et assurance qualité

---

## 📊 Statistiques du Projet

- **Microservices:** 13 services backend + 1 service Node.js
- **Bases de données:** 13 bases PostgreSQL dédiées
- **Endpoints API:** 200+ endpoints REST
- **Composants Angular:** 100+ composants
- **Lignes de code:** 50,000+ lignes (Backend + Frontend)
- **Tests:** 500+ tests unitaires et d'intégration

---

**Développé avec ❤️ par l'équipe Jungle in English**

*Dernière mise à jour: Mai 2026*
