# Utiliser l'image officielle Python
FROM python:3.9-slim

# Définir le dossier de travail
WORKDIR /app

# Copier uniquement les fichiers nécessaires
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copier le code source et les tests (avec le bon chemin)
COPY ../etl_process.py /app/etl_process.py
COPY test_etl.py upload_s3.py /app/

# Exécuter les tests Pytest au démarrage
CMD ["pytest", "test_etl.py", "--junitxml=results.xml"]
