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
`docker run --name some-nginx -p 8080:80 -v /home/user/TP1:/usr/share/nginx/html:ro -d nginx`



