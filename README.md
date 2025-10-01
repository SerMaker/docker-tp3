# TP Docker 3

Mettre en place une architecture web basée sur **NGINX**, **PHP-FPM** et **MariaDB** :  
- Étape 1 → NGINX + PHP-FPM  
- Étape 2 → Ajout de MariaDB  + Affichage test.php
- Étape 3 → Conversion en Docker Compose  

## Structure
```
docker-tp3/
├── etape1/
├── etape2/
├── etape3/
```
## Etape 1 : NGINX + PHP
```
docker network create tp3-web
docker run -d --name SCRIPT --network tp3-web -v ${pwd}/etape1:/app php:8.2-fpm
docker run -d --name HHTP --network tp3-web -p 8080:80 -v ${pwd}/etape1:/app -v ${pwd}/etape1/nginx/default.conf:/etc/nginx/conf.d/default.conf nginx:latest
docker ps
```
Ouvrir http://localhost:8080

## Etape 2 : Ajouter MariaDB + Affichage test.php
```
docker run -d --name DATA --network tp3-web -e MARIADB_ROOT_PASSWORD=password -v ${pwd}/etape2/database.sql:/docker-entrypoint-initdb.d/database.sql mariadb:latest
docker build -t php-mysqli ./etape2/php
docker run -d --name SCRIPT --network tp3-web -v ${pwd}/app:/app php-mysqli
docker run -d --name HTTP --network tp3-web -p 8080:80 -v ${pwd}/app:/app -v ${pwd}/../etape1/nginx/default.conf:/etc/nginx/conf.d/default.conf nginx:latest
```
Ouvrir http://localhost:8080/test.php

## Etape 3 : Convertir en Docker Compose
```
cd etape3
docker-compose up -d
```
Tous les conteneurs sont reliés via le réseau Docker tp3-web, crée précedemment
