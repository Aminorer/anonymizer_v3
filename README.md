# Anonymiseur Juridique RGPD v3.0

Application web pour l'anonymisation automatique de documents juridiques conformément au RGPD. L'application utilise FastAPI pour le backend et React pour le frontend.

## 🏗️ Architecture

- **Backend** : FastAPI + MongoDB + spaCy (NLP français)
- **Frontend** : React + Tailwind CSS + shadcn/ui
- **Base de données** : MongoDB
- **IA/NLP** : spaCy (fr_core_news_lg) + support Ollama

## 🚀 Installation et Lancement Local

### Prérequis

- Python 3.8+
- Node.js 16+
- MongoDB (local ou distant)
- yarn ou npm

### 1. Configuration de l'environnement

Clonez le projet et naviguez dans le dossier :
```bash
git clone <votre-repo>
cd anonymiseur-juridique-rgpd
```

### 2. Backend (FastAPI)

#### Installation des dépendances Python
```bash
cd backend
pip install -r requirements.txt
```

#### Installation du modèle spaCy français
```bash
python -m spacy download fr_core_news_lg
```

#### Configuration de la base de données
Assurez-vous que MongoDB est en cours d'exécution. Le fichier `.env` est déjà configuré :
```
MONGO_URL="mongodb://localhost:27017"
DB_NAME="test_database"
```

#### Lancement du serveur backend
```bash
cd backend
python server.py
```

Ou avec uvicorn :
```bash
uvicorn server:app --reload --host 0.0.0.0 --port 8000
```

Le backend sera disponible sur : `http://localhost:8000`

### 3. Frontend (React)

#### Installation des dépendances Node.js
```bash
cd frontend
yarn install
# ou
npm install
```

#### Configuration de l'environnement
Le fichier `.env` pointe actuellement vers le serveur de déploiement. Pour le développement local, créez un nouveau fichier `.env.local` :
```bash
cd frontend
echo "REACT_APP_BACKEND_URL=http://localhost:8000" > .env.local
echo "WDS_SOCKET_PORT=3000" >> .env.local
```

#### Lancement du serveur frontend
```bash
cd frontend
yarn start
# ou
npm start
```

Le frontend sera disponible sur : `http://localhost:3000`

## 🧪 Tests

### Test du Backend

Un script de test complet est fourni :
```bash
python backend_test.py
```

Ce script teste tous les endpoints de l'API avec un document juridique français d'exemple.

### Test Manuel

1. **Vérification du backend** : Accédez à `http://localhost:8000/api/` - vous devriez voir le message de bienvenue
2. **Vérification de la santé** : `http://localhost:8000/api/health` - vérifiez que spaCy est disponible
3. **Interface frontend** : `http://localhost:3000` - testez l'upload et le traitement de documents

## 📋 Fonctionnalités

### Modes de traitement

- **Standard** : Expressions régulières pour téléphones, emails, SIRET, etc.
- **Avancé** : Standard + reconnaissance d'entités nommées (personnes, organisations)
- **Ollama** : Support pour modèles IA locaux (en cours de développement)

### Types d'entités détectées

- 📱 **Téléphones** : Formats français (06.12.34.56.78, +33...)
- 📧 **Emails** : Adresses email complètes
- 🏢 **SIRET** : Numéros SIRET avec validation Luhn
- 🆔 **Sécurité Sociale** : Numéros INSEE
- 🏠 **Adresses** : Adresses françaises et codes postaux
- ⚖️ **Références légales** : Numéros RG, dossiers, articles
- 👤 **Personnes** : Noms détectés par IA (mode avancé)
- 🏛️ **Organisations** : Entreprises/institutions (mode avancé)

## 🛠️ Développement

### Structure du projet
```
anonymiseur-juridique-rgpd/
├── backend/
│   ├── server.py          # Serveur FastAPI principal
│   ├── requirements.txt   # Dépendances Python
│   └── .env              # Configuration base de données
├── frontend/
│   ├── src/              # Code source React
│   ├── package.json      # Dépendances Node.js
│   └── .env             # Configuration API
├── backend_test.py       # Tests backend
└── README.md
```

### API Endpoints

- `GET /api/` - Message de bienvenue
- `GET /api/health` - Status système
- `POST /api/process` - Traitement document
- `POST /api/test-ollama` - Test connexion Ollama
- `POST /api/generate-document` - Génération DOCX anonymisé

### Technologies utilisées

#### Backend
- FastAPI : API REST rapide
- spaCy : NLP pour le français
- pymongo/motor : Base de données MongoDB
- python-docx : Génération documents Word
- regex : Patterns d'anonymisation

#### Frontend
- React : Interface utilisateur
- Tailwind CSS : Styles
- shadcn/ui : Composants UI
- axios : Requêtes HTTP

## 🔧 Configuration avancée

### MongoDB personnalisé
Modifiez `backend/.env` :
```
MONGO_URL="mongodb://votre-host:port"
DB_NAME="votre_base"
```

### Support Ollama
Pour utiliser des modèles IA locaux, installez Ollama et configurez l'URL dans l'interface.

## 🐛 Dépannage

### Erreurs courantes

1. **spaCy model not found** : Installez le modèle français
   ```bash
   python -m spacy download fr_core_news_lg
   ```

2. **MongoDB connection failed** : Vérifiez que MongoDB est en cours d'exécution

3. **CORS errors** : Vérifiez que l'URL backend dans `.env.local` est correcte

4. **Port already in use** : Changez les ports dans les commandes de lancement

### Logs

Les logs du backend s'affichent dans le terminal. Pour plus de détails, modifiez le niveau de logging dans `server.py`.

## 📄 Licence

Ce projet est développé pour la conformité RGPD des documents juridiques français.

## 🤝 Contribution

1. Fork le projet
2. Créez une branche feature
3. Commitez vos changes
4. Push vers la branche
5. Ouvrez une Pull Request