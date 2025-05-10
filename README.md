# Solution de Scraping pour LinkedIn

## Architecture proposée

1. **Scraping initial**
   - Utilisation de Crawl4AI pour le scraping
   

2. **Format des données**
   ```json
   {
     "id": "linkedin-article-2025-05-11-abc123",
     "url": "https://www.linkedin.com/pulse/.../",
     "title": "Titre de l'article",
     "author": {
       "name": "Nom Prénom",
       "profile_url": "https://linkedin.com/in/..."
     },
     "date": "2025-05-11",
     "content_markdown": "...",
     "content_text": "...",
     "tags": ["IA", "RAG", "LinkedIn"],
     "source": "LinkedIn"
   }
   ```

3. **Stockage**
   - PostgreSQL avec support JSONB pour insertion facile
   - Avantages :
     - Accès direct au contenu texte
     - Création de nœuds relationnels enrichis

4. **LightRAG**
   - Combine :
     - Recherche vectorielle (ChromaDB, LanceDB, Milvus, PGvector)
     - Graphe de connaissances (NetworkX, Neo4J)
   - Avantages :
     - Structure relationnelle
     - Explicabilité des résultats
     - Solution légère et locale

## Installation de PostgreSQL avec Docker

1. **Télécharger Docker Desktop** :
   [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

2. **Lancer le conteneur PostgreSQL** :
   ```bash
   docker run --name fau-postgres \
   -e POSTGRES_PASSWORD=secret \
   -e POSTGRES_USER=admin \
   -e POSTGRES_DB=fau \
   -p 5432:5432 \
   -d postgres:16
   ```

3. **Vérifier le statut** :
   ```bash
   docker ps -f name=fau-postgres
   ```

4. **Activer l'extension PGvector** :
   ```bash
   docker exec -it fau-postgres psql -U admin -d fau -c "CREATE EXTENSION vector;"
   ```

5. **Connexion à la base** :
   ```bash
   psql postgres://admin:secret@localhost:5432/fau
   ```

## Workflow

1. Saisie des URLs dans un fichier .txt
2. Scraping des contenus
3. Conversion au format JSON standardisé
4. Insertion en base PostgreSQL
5. Utilisation dans LightRAG

## Prérequis

- Playwright
- PostgreSQL avec extension PGvector si on retient PGvector
- Python 3.10+

## Ressources Utiles

- [Guide complet d'installation PostgreSQL avec Docker sur MacOS](https://medium.com/@mateus2050/setting-up-postgresql-and-pgadmin-using-docker-on-macos-66cd7d275328)
- [Documentation officielle Docker](https://docs.docker.com/desktop/install/mac-install/)
- [Configuration avancée PGvector](https://github.com/pgvector/pgvector)

lien vers le Freeform pour Mac : https://www.icloud.com/freeform/019vnC8dn5Aw0ctWXjkap3Z7w#FAU
