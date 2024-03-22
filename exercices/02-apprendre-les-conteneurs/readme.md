# TP conteneur

## Partie 1

- En utilisant votre machine Windows, lancez le service Docker, s’il n’est pas lancé.
- Lancement de Docker Desktop

- Créer une image Docker sur votre machine du jeu 2048 (voir screen jeux_2048).

```sh
docker search docker-2048
docker pull alexwhen/docker-2048
```

- Vérifier que l’image est bien présente sur votre machine.

```sh
docker images
```

- Lancer ce jeu sur un port disponible au travers d’un conteneur que vous allez appeler «jeu-votre-nom ».

```sh
docker run -d --name jeu-votre-nom -p 8080:80 alexwhen/docker-2048
```

- Vérifier que le conteneur est bien lancé avec la commande adaptée.

```sh
docker ps
```

- Créer un second conteneur qui va lancer le même jeu mais avec un nom différent «jeu2-votre-nom ».

```sh
docker run -d --name jeu2-votre-nom -p 8081:80 alexwhen/docker-2048
```

- Les 2 jeux sont fonctionnels en même temps sur votre machine, effectuez la commande pour vérifier la présence des conteneurs.

```sh
docker ps
```

- Ouvrez les 2 jeux sur votre navigateur.

```
http://localhost:8081/
http://localhost:8080/
```

- Stopper les 2 conteneurs et assurez-vous que ces 2 conteneurs sont arrêtés.

```sh
docker stop jeu-votre-nom
docker stop jeu2-votre-nom
docker ps
```

- Relancez le conteneur «jeu2-votre-nom » et aller vérifier dans votre navigateur s’il fonctionne bien. Effectuez la commande pour voir s’il a bien été relancé. Puis stopper le.

```sh
docker start jeu2-votre-nom
http://localhost:8081/
docker ps
docker stop jeu2-votre-nom
```

- Supprimez l’image du jeu 2048 et les conteneurs associés.

```sh
docker rm jeu-votre-nom
docker rm jeu2-votre-nom
docker rmi alexwhen/docker-2048
```

- Vérifiez que les suppressions ont bien été faite.

```sh
docker images
docker ps -a
```

## Partie 2

- Récupérer une image docker nginx.

```sh
docker search nginx
docker pull nginx
```

- Créer un conteneur en vous basant sur cette image en lui attribuant le nom suivant : « nginx-web».

```sh
docker run -d --name nginx-web -p 8082:80 nginx
```

- Assurez-vous que l’image est bien présente et que le conteneur est bien lancé.

```sh
docker ps
docker images
```

- Ce serveur nginx web (nginx-web) devra être lancé sur un port disponible.

```
 -p 8082:80
```

- Vérifier que le serveur est bien lancé au travers du navigateur.

```
http://localhost:8082/
```

- Une page web avec «Welcome to nignx » devrait s'afficher (voir nginx.png).

```
http://localhost:8082/
```

- Effectuer la commande vous permettant de rentrer à l’intérieur de votre serveur nginx.

```sh
docker exec -it nginx-web /bin/sh
```

- Une fois à l’intérieur, aller modifier la page html par défaut de votre serveur nginx en changeant le titre de la page en :  
  Welcome «votre prenom ».

```sh
cd /usr/share/nginx/html
apt update
apt upgrade
apt install nano
nano index.html
```

- Relancez votre serveur et assurez-vous que le changement à bien été pris en compte, en relançant votre navigateur.

```sh
docker stop nginx-web
docker start nginx-web
```

- Refaite la même opération mais en utilisant le serveur web apache et donc il faudra créer un autre conteneur.

```sh
docker search apache
docker pull httpd
```

```sh
docker run -d --name apache-web -p 8083:80 httpd
```

```sh
docker exec -it apache-web /bin/sh
```

```sh
cd /usr/local/apache2/htdocs
apt update
apt upgrade
apt install nano
nano index.html
```

- Il faut supprimer le contenu complet de l'index.html et y mettre : "Je suis heureux et je m'appelle votre prenom".

```sh
echo "Je suis heureux et je m'appelle votre prenom" > index.html
```

- Le changement doit apparaître dans votre navigateur.

```
http://localhost:8083/
```

## Partie 3

- Répétez 3 fois la même opération que pour le début de la partie 2, il faudra juste appelez vos conteneurs :

- « nginx-web3 ».

```sh
docker run -d --name nginx-web3 -p 8084:80 nginx
```

- « nginx-web4 ».

```sh
docker run -d --name nginx-web4 -p 8085:80 nginx
```

- « nginx-web5 ».

```sh
docker run -d --name nginx-web5 -p 8086:80 nginx
```

- Il faudra faire en sorte que les pages html présente dans les fichiers ci-dessous s’affiche dans chacun des navigateurs en lien avec vos conteneurs :

- html5up-editorial-m2i.zip pour nginx-web3

```sh
docker cp chemin/de/mon/fichier/html5up-editorial-m2i.zip nginx-web3:/usr/share/nginx/html
cd /usr/share/nginx/html
apt update
apt upgrade
unzip html5up-editorial-m2i.zip -d ./
cd html5up-editorial-m2i
mv ./* ../
```

- html5up-massively.zip pour nginx-web4

```sh
docker cp chemin/de/mon/fichier/html5up-massively.zip nginx-web3:/usr/share/nginx/html
cd /usr/share/nginx/html
apt upgrade
apt update
unzip html5up-massively.zip -d ./
```

- html5up-paradigm-shift.zip pour nginx-web5

```sh
docker cp chemin/de/mon/fichier/html5up-paradigm-shift.zip nginx-web3:/usr/share/nginx/html
cd /usr/share/nginx/html
apt upgrade
apt update
unzip html5up-paradigm-shift.zip -d ./
```

- Stopper, ensuite, ces différents conteneurs.

```sh
docker stop nginx-web3
docker stop nginx-web4
docker stop nginx-web5
```
