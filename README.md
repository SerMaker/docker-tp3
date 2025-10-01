# TP Docker 3

Mettre en place une architecture web basée sur **NGINX**, **PHP-FPM** et **MariaDB** :  
- Étape 1 → NGINX + PHP-FPM  
- Étape 2 → Ajout de MariaDB  
- Étape 3 → Conversion en Docker Compose  

## Structure
```
docker-tp3/
├── etape1/
├── etape2/
├── etape3/
```
## Etape 1 : NGINX + PHP
docker network create tp3-web
docker run -d --name SCRIPT --network tp3-web -v ${pwd}/etape1:/app php:8.2-fpm
docker run -d --name HHTP --network tp3-web -p 8080:80 -v ${pwd}/etape1:/app -v ${pwd}/etape1/nginx/default.conf:/etc/nginx/conf.d/default.conf nginx:latest
docker ps
