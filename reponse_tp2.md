2.
La commande nano n’est pas reconnue, car le paquet nano n’est pas installé.

7.
Cette fois, nano s’ouvre bien car on a créé une image de ubuntu contenant nano grâce au Dockerfile.

10.
Nous avons reconstruit l’image et écrasé l’ancienne version. Le répertoire de travail par défaut du container est /app.

11.
On constate que le répertoire courant est directement /app.

13.
On a ajouté une commande par défaut au Dockerfile. Si durant l'appel de l'image, aucune commande précise n'est exécutée.

14.
Sans préciser de commande, la commande par défaut est nano index.html. Le container démarre donc dans nano avec ce fichier.

17.
docker run -it -v "$(pwd)":/app --rm ubuntu:24.04-withnano
Le répertoire local (contenant index.html) est monté dans /app, la commande nano index.html ouvre donc bien le fichier créé sur l’hôte mais accessible depuis le container.

24.
Le fichier test.txt créé dans le container apparaît aussi sur l’hôte. On le voit bien avec la commande ls. Le fichier contient bien le contenu fourni

26.
En reconstruisant l’image, on a donne la commande d'entrée prioritaire (donc nano) et un paramètre par defaut si aucun n'est précisé (index.html)
Par défaut l’image lancera toujours nano, et elle ouvrira index.html si on ne précise pas un autre ficheir

27.
Quand on lance un container avec cette image, on tombe directement dans nano avec le fichier index.html qui est présent dans le répertoire monté depuis l’hôte

28.
docker run -it -v "$(pwd)":/app nano:latest test.txt
Si on lance le container en ajoutant test.txt à la commande, alors c’est ce fichier qui s’ouvre dans nano. Le paramètre par défaut (index.html) est remplacé par ce qu’on indique au lancement