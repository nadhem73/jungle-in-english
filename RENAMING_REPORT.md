# 📋 Rapport de Renommage: EnglishFlow → Jungle in English

## ✅ Fichiers Déjà Mis à Jour

- ✅ `README.md` - Toutes les occurrences remplacées

## 📝 Fichiers Nécessitant des Modifications

### 1. Configuration Globale

#### `.env.example`
- Ligne 1: Titre du fichier
- Ligne 61: `IMAGE_PREFIX=your-org/englishflow` → `IMAGE_PREFIX=your-org/jungle`

#### `sonar-project.properties`
- Ligne 1: Commentaire
- Ligne 5: `sonar.projectName=EnglishFlow - Jungle in English` → `sonar.projectName=Jungle in English`

#### `Makefile`
- Ligne 4: `@echo "EnglishFlow - Available commands:"` → `@echo "Jungle in English - Available commands:"`
- Ligne 115: `sonar.projectKey=englishflow-backend` → `sonar.projectKey=jungle-backend`

### 2. Scripts Python

#### `generate-coverage-report.py`
- Ligne 3: Commentaire de description
- Ligne 101: Titre du rapport
- Ligne 129: Titre HTML
- Ligne 274: Titre de la page
- Ligne 354: Footer
- Ligne 366: Print statement

### 3. Backend - WebRTC Signaling (Node.js)

#### `backend/webrtc-signaling/package.json`
- Ligne 2: `"name": "englishflow-signaling"` → `"name": "jungle-signaling"`
- Ligne 4: Description

#### `backend/webrtc-signaling/server.js`
- Ligne 262: Message de console

### 4. Backend - Sponsors Service

#### `backend/sponsors-service/.env.example`
- Ligne 6: `DB_URL=jdbc:postgresql://localhost:5432/englishflow_sponsors_db` → `jungle_sponsors_db`
- Ligne 18: `MAIL_FROM=noreply@englishflow.com` → `noreply@jungleinenglish.com`

#### `backend/sponsors-service/src/main/resources/application.yml`
- Ligne 6: URL de base de données
- Ligne 44: Secret JWT (commentaire)
- Ligne 50: Clé de service interne (commentaire)
- Ligne 136: Package de logging `com.englishflow.sponsors` → `com.jungle.sponsors`

#### Fichiers de test Java dans `backend/sponsors-service/src/test/java/`
- `com/englishflow/sponsors/` → `com/jungle/sponsors/`
  - `service/EmailServiceTest.java`
  - `service/WebSocketNotificationServiceTest.java`
  - `service/SponsorServiceTest.java`
  - `security/InternalServiceAuthenticationFilterTest.java`

### 5. DevOps Scripts

#### `devops/scripts/check-services.sh`
- Ligne 12: `BASE_URL="https://englishflow.com"` → `BASE_URL="https://jungleinenglish.com"`
- Ligne 14: `BASE_URL="https://staging.englishflow.com"` → `BASE_URL="https://staging.jungleinenglish.com"`
- Ligne 17: Message d'écho

#### `devops/scripts/docker-build-all.sh`
- Ligne 68: Messages de tags Docker

### 6. Frontend

#### `frontend/Dockerfile`
- Ligne 28: `COPY --from=builder /app/dist/englishflow-pi/browser` → `/app/dist/jungle-pi/browser`

#### `frontend/karma.conf.js`
- Ligne 28: `dir: require('path').join(__dirname, './coverage/englishflow-pi')` → `'./coverage/jungle-pi'`

## 🔍 Fichiers Supplémentaires à Vérifier

Les fichiers suivants peuvent également contenir des références à "englishflow" :

### Backend Services (à vérifier individuellement)
- `backend/auth-service/`
- `backend/courses-service/`
- `backend/club-service/`
- `backend/community-service/`
- `backend/learning-service/`
- `backend/messaging-service/`
- `backend/event-service/`
- `backend/exam-service/`
- `backend/gamification-service/`
- `backend/payment-service/`
- `backend/complaints-service/`
- `backend/api-gateway/`
- `backend/eureka-server/`
- `backend/config-server/`

### Fichiers à vérifier dans chaque service :
- `pom.xml` - groupId, artifactId
- `application.properties` / `application.yml` - URLs, noms de bases de données
- `Dockerfile` - labels, noms
- Packages Java : `com.englishflow.*` → `com.jungle.*`
- Fichiers de test

### Frontend
- `frontend/package.json` - name, description
- `frontend/angular.json` - projectName, outputPath
- `frontend/src/environments/` - URLs d'API
- Fichiers TypeScript avec imports ou références

### DevOps
- `devops/docker/docker-compose.yml` - noms de conteneurs, variables d'environnement
- `devops/docker/docker-compose.prod.yml`
- `devops/database/init-databases.sql` - noms de bases de données
- Fichiers de monitoring dans `devops/monitoring/`

## 🎯 Recommandations

### Option 1: Renommage Manuel Sélectif
Modifier uniquement les fichiers critiques :
- Configuration de base de données
- URLs publiques
- Documentation utilisateur
- Noms de packages principaux

### Option 2: Renommage Complet (Recommandé pour cohérence)
Utiliser un script de recherche et remplacement global :

```bash
# Rechercher toutes les occurrences (exclure node_modules, target, etc.)
find . -type f \
  -not -path "*/node_modules/*" \
  -not -path "*/target/*" \
  -not -path "*/.angular/*" \
  -not -path "*/dist/*" \
  -exec grep -l "englishflow" {} \;

# Remplacer dans tous les fichiers (ATTENTION: faire un backup avant!)
find . -type f \
  -not -path "*/node_modules/*" \
  -not -path "*/target/*" \
  -not -path "*/.angular/*" \
  -not -path "*/dist/*" \
  -exec sed -i 's/englishflow/jungle/g' {} \;

# Pour les majuscules
find . -type f \
  -not -path "*/node_modules/*" \
  -not -path "*/target/*" \
  -exec sed -i 's/EnglishFlow/Jungle in English/g' {} \;
```

### Option 3: Renommage des Packages Java
Pour renommer les packages Java de `com.englishflow` à `com.jungle` :

1. Utiliser l'IDE (IntelliJ IDEA / Eclipse) :
   - Clic droit sur le package → Refactor → Rename
   - Cela mettra à jour automatiquement tous les imports

2. Ou utiliser un script :
```bash
# Renommer les répertoires
find backend -type d -name "englishflow" -exec bash -c 'mv "$0" "${0/englishflow/jungle}"' {} \;

# Mettre à jour les imports dans les fichiers Java
find backend -name "*.java" -exec sed -i 's/com\.englishflow/com.jungle/g' {} \;
```

## ⚠️ Points d'Attention

1. **Bases de données** : Les noms de bases de données doivent correspondre entre :
   - Scripts d'initialisation
   - Configuration des services
   - Docker Compose

2. **URLs** : Vérifier la cohérence des URLs dans :
   - Configuration frontend
   - Configuration backend
   - Scripts de déploiement

3. **Secrets** : Les secrets JWT et clés internes peuvent rester inchangés (ce sont des valeurs, pas des noms)

4. **Tests** : Après le renommage, exécuter tous les tests pour vérifier qu'aucune référence n'a été cassée

5. **Git** : Faire un commit avant le renommage massif pour pouvoir revenir en arrière si nécessaire

## 📊 Statistiques

- **Fichiers identifiés** : ~50+ fichiers
- **Services backend concernés** : 14 services
- **Types de fichiers** : Java, TypeScript, YAML, Properties, Shell, Python, JSON, Markdown
- **Packages Java à renommer** : `com.englishflow.*` → `com.jungle.*`

---

**Date du rapport** : Mai 2026  
**Statut** : README.md mis à jour ✅
