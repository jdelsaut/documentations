# 📘 Guide des commandes Docker & Docker Compose

## 🐳 Docker

### Gestion des images
```bash
docker build -t nom_image:tag .
docker pull nom_image:tag
docker images        # Lister les images locales
docker rmi image_id  # Supprimer une image
```

### Gestion des conteneurs
```bash
docker run -d --name mon_conteneur nom_image:tag   # Lancer un conteneur en arrière-plan
docker ps                                          # Lister les conteneurs actifs
docker ps -a                                       # Lister tous les conteneurs
docker stop id_conteneur                           # Arrêter un conteneur
docker start id_conteneur                          # Démarrer un conteneur
docker restart id_conteneur                        # Redémarrer un conteneur
docker rm id_conteneur                             # Supprimer un conteneur
```

### Exécution et interaction
```bash
docker exec -it id_conteneur bash   # Ouvrir un shell dans le conteneur
docker logs id_conteneur            # Voir les logs
docker inspect id_conteneur         # Voir les détails
```

### Réseau et volumes
```bash
docker network ls                         # Lister les réseaux
docker network create mon_reseau          # Créer un réseau
docker volume ls                          # Lister les volumes
docker volume create mon_volume           # Créer un volume
```

---

## ⚓ Docker Compose (commande moderne `docker compose`)

### Commandes principales
```bash
docker compose up          # Démarrer les services
docker compose up -d       # Démarrer en arrière-plan
docker compose down        # Arrêter et supprimer les conteneurs
docker compose ps          # Voir les services en cours
docker compose logs        # Afficher les logs
docker compose restart     # Redémarrer les services
```

### Gestion avancée
```bash
docker compose build       # Recompiler les images
docker compose pull        # Télécharger les images définies
docker compose stop        # Arrêter les services (sans les supprimer)
docker compose start       # Relancer des services arrêtés
docker compose exec service_name bash   # Exécuter une commande dans un service
```
### Divers
```bash
docker compose config --services
docker volume prune
docker compose up --build -d
docker compose exec db psql -U postgres -d air-collecte-db
docker compose exec web alembic upgrade head
docker compose logs web
 ```
---

## 🚀 Exemple de `docker-compose.yml`
```yaml
version: "3.9"

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: exemple
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```
