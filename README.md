# TP1 - Docker


## Installation de Docker


## Installation de l'image d'Nginx


## Configuration et mise en ligne d'une page index.html

Récupération de l'image sur le docker Hub :
`docker pull nginx`

Vérification de l'existance des images docker en local
`docker images`

Index.html :
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Docker</title>
</head>
<body>
    <h1>TP1 - From Ynov to Docker</h1>
</body>
</html>
```

Initialisation d'un conteneur et création d'un volume :
`docker run --name some-nginx -p 8080:80 -v /home/user/TP1:/usr/share/nginx/html -d nginx`

Suppression du conteneur existant : 
`docker stop some-nginx`
`docket rm some-nginx`

Utilisation de la commande cp :
`docker run --name some-nginx-with-cp -v /host/path/nginx.conf:/etc/nginx/nginx.conf:ro -d nginx`
`docker run --name tmp-nginx-container -d nginx`
`docker cp tmp-nginx-container:/etc/nginx/nginx.conf /host/path/nginx.conf`
`docker rm -f tmp-nginx-container`

## Builder une image

Création d'un Dockerfile :
`touch DockerFile`

```
FROM nginx
ADD index.html /usr/share/nginx/html
```

Build de l'image : `docker build -t some-nginx`


Exécution de l'image : `docker run --name some-nginx-container -d some-nginx`

Observations :
- Optimisation et centralisations des commandes pour la construction d'image
- Rapidité pour le Dockerfile

## Question 7 TP

### Création du fichier docker-compose.yml

`$ touch docker-compose.yml`

Ce fichier utilisera l'image *praqma/network-multitool* et va créer 3 services : **web**, **app** et **db**.
Ce fichier créera également 2 réseaux distincs : 1 pour le **frontend** et 1 pour le **backend**

On obtient le fichier suivant :
```yml
version: "3"

services:
    web:
        image: praqma/network-multitool:latest
        ports:
        - 8080:80
        networks:
            - frontend

    app:
        image: praqma/network-multitool:latest
        networks:
            - backend
      
    db:
        image: praqma/network-multitool:latest
        ports: 
        - 3306:3306
        networks:
        - backend
        environment:
        - MYSQL_ROOT_PASSWORD=root
        - MYSQL_DATABASE=ynov 
        - MYSQL_USER=user 
        - MYSQL_PASSWORD=pwd

networks:
  frontend:
  backend:
```
