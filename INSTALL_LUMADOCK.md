
# 🗺️ Installation Carto-Laser sur Lumadock

## 1. Copier le dossier
Copiez ce dossier `Carto-workshop` sur votre VPS, par exemple dans `/opt/lumadock/carto-laser` ou simplement `./carto-laser` à côté de votre `docker-compose.yml`.

## 2. Modifier docker-compose.yml
Ajoutez ce bloc de service à votre fichier `docker-compose.yml` existant (sous `services:`):

```yaml
  # Carto Laser - Générateur de cartes vectorielles OSM
  carto-laser:
    build:
      context: ./carto-laser  # Ajustez le chemin vers le dossier
      dockerfile: Dockerfile
    container_name: vulca-carto-laser
    restart: unless-stopped
    ports:
      - "8090:80"
    networks:
      - vulca-network
```

## 3. Déployer
Lancez la commande :
```bash
docker-compose up -d --build carto-laser
```

## 4. Accès
L'outil sera disponible sur : `http://votre-ip-vps:8090`
