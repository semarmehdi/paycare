# Guide de Configuration Jenkins et Pipeline CI/CD

## 📌 Introduction

Ce projet implémente un pipeline CI/CD dans Jenkins pour exécuter un processus ETL en conteneur Docker. Le pipeline inclut des tests unitaires et envoie les résultats sur AWS S3.

## 📂 Structure du projet

```
├── Jenkinsfile               # Pipeline Jenkins
├── Dockerfile                # Conteneurisation du projet
├── etl_process.py            # Script ETL principal
├── test_etl.py               # Tests unitaires pour l'ETL
├── upload_s3.py              # Script d'upload des résultats sur S3
├── requirements.txt          # Dépendances Python
└── data/
    ├── input_data.csv        # Fichier d'entrée pour l'ETL
    ├── output_data.csv       # Résultat du processus ETL
```

---

## 🚀 Étapes de configuration

### 1️⃣ Configuration de Jenkins

Assurez-vous que Jenkins est bien installé et fonctionne.

### 2️⃣ Ajout des Variables d'Environnement

Les variables AWS pour l'upload sur S3 doivent être ajoutées à Jenkins.

1. **Aller dans Jenkins** → **Manage Jenkins** → **Manage Credentials**
2. Sélectionnez **(global)** → **Add Credentials**
3. Ajoutez les clés AWS en tant que **Secret Text**:
   - **AWS_ACCESS_KEY_ID**
   - **AWS_SECRET_ACCESS_KEY**

Ou ajoutez-les directement dans Jenkins :

1. **Aller dans Jenkins** → **Manage Jenkins** → **Configure System**
2. Ajoutez sous **Global Properties** → **Environment Variables** :
   - `AWS_ACCESS_KEY_ID = VOTRE_CLE`
   - `AWS_SECRET_ACCESS_KEY = VOTRE_CLE_SECRET`

### 3️⃣ Configuration du Job Jenkins

1. **Créer un nouveau job Jenkins** → **Pipeline**
2. **Sélectionner Pipeline Script from SCM**
3. **Ajouter le repository GitHub** contenant le `Jenkinsfile`
4. **Sauvegarder et exécuter**

---

## 🏗️ Fonctionnement du Pipeline

### 🛠️ Étapes du Pipeline :

1. **Clone du repository** : Récupère le code depuis GitHub.
2. **Exécution des tests** :
   - Lance les tests dans un conteneur Docker.
   - Enregistre les résultats en XML.
   - Envoie les résultats sur S3.
3. **Build de l'ETL** :
   - Construit l'image Docker pour l'ETL.
4. **Exécution de l'ETL** :
   - Monte les fichiers CSV et exécute le traitement.
   - Sauvegarde le résultat dans `data/output_data.csv`.

---

Ce pipeline CI/CD garantit l'intégration et le déploiement automatisé du processus ETL en utilisant Jenkins et Docker.

🔥 N'hésitez pas à adapter les configurations en fonction de votre environnement !
