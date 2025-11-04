<table align="center">
  <tr>
    <td align="center" width="50%">
      <a href="https://github.com/Sam-Tech-Lab-Git" target="_blank">
        <img src="https://raw.githubusercontent.com/Sam-Dz-Devops/Images/main/Sam-Tech-Site-Web.png" 
             alt="Sam Tech Lab Logo" width="300"/>
      </a>
    </td>
    <td align="center" width="50%">
      <a href="https://hub.docker.com/r/samtechrepo/jammy" target="_blank">
        <img src="https://upload.wikimedia.org/wikipedia/commons/7/76/Ubuntu-logo-2022.svg?sanitize=true" 
             alt="Ubuntu Logo" width="180"/>
      </a>
    </td>
  </tr>
</table>

<p align="center">
  <a href="https://hub.docker.com/r/samtechrepo/jammy" target="_blank">
    <img src="https://img.shields.io/docker/pulls/samtechrepo/jammy.svg?style=for-the-badge&logo=docker&logoColor=white" alt="Docker Pulls"/>
  </a>
  <a href="https://hub.docker.com/r/samtechrepo/jammy" target="_blank">
    <img src="https://img.shields.io/docker/stars/samtechrepo/jammy.svg?style=for-the-badge&logo=docker&logoColor=white" alt="Docker Stars"/>
  </a>
  <a href="https://github.com/Sam-Tech-Lab-Git" target="_blank">
    <img src="https://img.shields.io/static/v1?label=SamTechLab&message=GitHub&color=94398d&labelColor=555555&style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/>
  </a>
  <a href="https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/LICENSE" target="_blank">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="License: MIT"/>
  </a>
  <a href="https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/actions/workflows/build-amd64.yml" target="_blank">
      <img src="https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/actions/workflows/build-amd64.yml/badge.svg" alt="Build amd64 — Monthly"/>
  </a>
  <a href="https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/actions/workflows/build-arm64.yml" target="_blank">
      <img src="https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/actions/workflows/build-arm64.yml/badge.svg" alt="Build arm64 — Monthly"/>
  </a>
  <a href="https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/actions/workflows/build-multiarch.yml" target="_blank">
      <img src="https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/actions/workflows/build-multiarch.yml/badge.svg" alt="Build multiarch — Monthly"/>
  </a>
</p>

---

## Overview

This image provides a **clean, stable, and minimal Ubuntu base** to build production-ready Docker containers.  
It is built **from scratch** using the **official Ubuntu OCI rootfs**, ensuring **authenticity**, **lightness**, and **reproducibility**.

> **Automatic monthly updates**:  
> The image is rebuilt every month with the latest Ubuntu updates and security patches.

Designed to be **secure, fast, and multi-purpose**, it includes advanced APT optimizations, a non-root user, and system hardening for maximum reliability.

---

## Key Features

- ✅ **“FROM scratch” image** — minimal size with optimized multi-stage builds  
- ✅ **Based on the official Ubuntu OCI rootfs**  
- ✅ **APT & dpkg optimization** — no recommended packages, clean cache  
- ✅ **Automatic service blocking** (`systemd`, `upstart`)  
- ✅ **Non-root user (`appuser`)** for safer container execution  
- ✅ **Full cleanup** of `/tmp`, `/var/log`, `/var/lib/apt/lists`  
- ✅ **Locale & timezone configured** (`en_US.UTF-8`, `UTC`)
- ✅ **System hardening**:
  - Root account locked  
  - Unnecessary SUID/SGID bits removed  
  - Default `umask 027`  
- ✅ **PUID/PGID variables** for easy permission mapping  
- ✅ **Automated monthly rebuilds**  
- ✅ **Regular security patches**

---

## Included Packages

| Category | Packages |
|-----------|-----------|
| System base | `bash`, `cron`, `curl`, `gnupg`, `jq`, `netcat-openbsd`, `tzdata` |
| System tools | `systemd-standalone-sysusers`, `apt-utils`, `locales` |

---

## Environment Variables

| Variable | Default value | Description |
|-----------|----------------|--------------|
| `PUID` | `999` | Non-root user ID |
| `PGID` | `999` | Non-root group ID |
| `HOME` | `/config` | Home directory |
| `LANG` | `en_US.UTF-8` | Default locale |
| `TZ` | `UTC` | Timezone |
| `DEBIAN_FRONTEND` | `noninteractive` | Disables interactive APT prompts |

---

## Base Specifications

| Field | Value |
|--------|--------|
| OS | Ubuntu |
| Architectures | amd64, arm64 |
| Source | Ubuntu OCI RootFS |
| Maintainer | Sam Tech Lab |
| License | MIT |
| Update frequency | Monthly (automated) |

---

## Dockerfile Sources

- **Dockerfile amd64**: [GitHub – Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/Dockerfile-amd64](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/Dockerfile-amd64)
- **Dockerfile arm64**: [GitHub – Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/Dockerfile-arm64](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/Dockerfile-arm64)
- **Dockerfile multiarch** : [GitHub – Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/Dockerfile-arm64](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/Dockerfile-multi-arch)

---

## Usage Examples

### 1. Run an interactive container

```bash
docker run -it --rm ghcr.io/sam-tech-lab-git/jammy:latest /bin/bash
```

### 2. Simple Dockerfile

```dockerfile
FROM ghcr.io/sam-tech-lab-git/jammy:latest

RUN apt update && apt install -y nginx

CMD ["nginx", "-g", "daemon off;"]
```

This Dockerfile creates a custom image based on ghcr.io/sam-tech-lab-git/jammy:latest with NGINX preinstalled.

You can then build and test it locally:

```bash
docker build -t my-nginx .

docker run -d -p 8080:80 my-nginx
```

### 3. Example with Docker Compose
Create a file named docker-compose.yml:

```yaml
services:
  web:
    image: ghcr.io/sam-tech-lab-git/jammy:latest
    container_name: nginx-web
    restart: unless-stopped
    ports:
      - "8080:80"
    volumes:
      - ./html:/var/www/html
    environment:
      TZ: "Europe/Paris"
      PUID: 1000
      PGID: 1000
    command: >
      bash -c "
      apt update &&
      apt install -y nginx &&
      nginx -g 'daemon off;'
      "
```

Then start the container :

```bash
docker compose up -d
```

This automatically pulls the optimized Ubuntu image from Sam Tech Lab, installs NGINX, and launches the web server at http://localhost:8080.

To stop the container :

```bash
docker compose down
```

---

## Présentation

Cette image fournit une **base Ubuntu propre, stable et minimaliste** pour construire des conteneurs Docker de production.  
Elle est construite **from scratch** à partir du **rootfs officiel Ubuntu OCI**, garantissant **authenticité**, **légèreté** et **reproductibilité**.

> **Mises à jour automatiques mensuelles** :  
> L’image est reconstruite chaque mois avec les dernières mises à jour et correctifs de sécurité Ubuntu officiels.

Conçue pour être sécurisée, rapide et multi-usage, elle inclut des optimisations APT avancées, un utilisateur non-root et un durcissement du système pour une compatibilité maximale.

---

## Points forts

- ✅ **Image ”FROM scratch”** : taille minimale, multi-étapes optimisées  
- ✅ **Basée sur le rootfs officiel Ubuntu OCI**  
- ✅ **Optimisation APT & dpkg** : aucun paquet recommandé, cache propre  
- ✅ **Blocage des services automatiques** (`systemd`, `upstart`)  
- ✅ **Utilisateur non-root (`appuser`)** pour une exécution plus sûre  
- ✅ **Nettoyage complet** : `/tmp`, `/var/log`, `/var/lib/apt/lists`  
- ✅ **Locale & fuseau horaire configurés** (`en_US.UTF-8`, `UTC`) 
- ✅ **Durcissement système** :
  - Compte `root` verrouillé  
  - Suppression des bits SUID/SGID inutiles  
  - `umask 027` par défaut  
- ✅ **Variables PUID/PGID** pour mapper facilement les permissions  
- ✅ **Mises à jour système automatiques chaque mois**  
- ✅ **Correctifs de sécurité réguliers**

---

## Paquets inclus

| Catégorie | Paquets |
|------------|----------|
| Base système | `bash`, `cron`, `curl`, `gnupg`, `jq`, `netcat-openbsd`, `tzdata` |
| Outils système | `systemd-standalone-sysusers`, `apt-utils`, `locales` |

---

## Variables d’environnement

| Variable | Valeur par défaut | Description |
|-----------|------------------|--------------|
| `PUID` | `999` | Identifiant de l’utilisateur non-root |
| `PGID` | `999` | Identifiant de groupe non-root |
| `HOME` | `/config` | Répertoire personnel |
| `LANG` | `en_US.UTF-8` | Locale par défaut |
| `TZ` | `UTC` | Fuseau horaire |
| `DEBIAN_FRONTEND` | `noninteractive` | Empêche les invites APT interactives |

---

## Spécifications de base

| Champ | Valeur |
|--------|--------|
| Système | Ubuntu |
| Architecture | amd64, arm64 |
| Source | Ubuntu OCI RootFS |
| Mainteneur | Sam Tech Lab |
| Licence | MIT |
| Mise à jour | Mensuelle (automatisée) |

---

## Sources du Dockerfile

- **Dockerfile amd64** : [GitHub – Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/Dockerfile-amd64](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/Dockerfile-amd64)
- **Dockerfile arm64** : [GitHub – Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/Dockerfile-arm64](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/Dockerfile-arm64)
- **Dockerfile multiarch** : [GitHub – Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/Dockerfile-arm64](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/Dockerfile-multi-arch)

---

## Exemple d’utilisation

### 1. Lancer un conteneur interactif

```bash
docker run -it --rm ghcr.io/sam-tech-lab-git/jammy:latest /bin/bash
```

### 2. Dockerfile simple

```dockerfile
FROM ghcr.io/sam-tech-lab-git/jammy:latest

RUN apt update && apt install -y nginx

CMD ["nginx", "-g", "daemon off;"]
```

Ce Dockerfile crée une image personnalisée basée sur ghcr.io/sam-tech-lab-git/jammy:latest, avec NGINX préinstallé.

Vous pouvez ensuite la construire et la tester localement :

```bash
docker build -t my-nginx .

docker run -d -p 8080:80 my-nginx
```

### 3. Exemple avec Docker Compose
Créer un fichier nommé docker-compose.yml :

```yaml
services:
  web:
    image: ghcr.io/sam-tech-lab-git/jammy:latest
    container_name: nginx-web
    restart: unless-stopped
    ports:
      - "8080:80"
    volumes:
      - ./html:/var/www/html
    environment:
      TZ: "Europe/Paris"
      PUID: 1000
      PGID: 1000
    command: >
      bash -c "
      apt update &&
      apt install -y nginx &&
      nginx -g 'daemon off;'
      "
```

Puis lancer le conteneur :

```bash
docker compose up -d
```

Cela télécharge automatiquement l’image Ubuntu optimisée Sam Tech Lab, installe Nginx, et démarre le serveur web sur http://localhost:8080.

Arrêter le conteneur :

```bash
docker compose down
```

---

## License / Licence

This project is distributed under the **MIT** license — see the [LICENSE](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/LICENSE) file for more details.

Ce projet est distribué sous la licence **MIT** — consultez le fichier [LICENSE](https://github.com/Sam-Tech-Lab-Git/Docker-Ubuntu-Jammy/blob/main/LICENSE) pour plus de détails.

---

## Copyright / Droit d’auteur

```text
Copyright (c) 2025 Sam Tech Lab
```
