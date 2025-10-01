
**Question 4 :**
Commande : docker image ls

Constat :
- Lï¿½image nginx:latest correspond ï¿½ la version 1.29 (mï¿½me IMAGE ID 41f689c20910 ).
- Donc quand on fait docker pull nginx sans version, Docker tï¿½lï¿½charge lï¿½image la plus rï¿½cente (1.29).
- On a bien trois images disponibles : nginx:1.20, nginx:1.29 et nginx:latest.


**Question 7 :**
Commande : docker image rm nginx:1.20

Constat :
- Docker renvoie une erreur.
- Lï¿½image nginx:1.20 ne peut pas ï¿½tre supprimï¿½e car elle est utilisï¿½e par un container en cours dï¿½exï¿½cution (e1b67dc6006c).


**Question 8 :**
Commande : docker container rm e1b67dc6006c

Constat :
- Docker renvoie une erreur car on ne peut pas supprimer un container qui est encore en cours dï¿½exï¿½cution.
- Message dï¿½erreur typique : 'cannot remove a running container'.
- Pour le supprimer, il faut dï¿½abord lï¿½arrï¿½ter avec docker container stop.


**Question 8 :**
Commande : docker container rm e1b67dc6006c

Constat :
- Docker renvoie une erreur car on ne peut pas supprimer un container qui est encore en cours dï¿½exï¿½cution.
- Message dï¿½erreur typique : 'cannot remove a running container'.
- Pour le supprimer, il faut dï¿½abord lï¿½arrï¿½ter avec docker container stop.


**Question 9 :**
Commande : docker container stop e1b67dc6006c

Constat :
- Le container sï¿½arrï¿½te correctement.
- Aprï¿½s lï¿½arrï¿½t, il reste prï¿½sent dans la liste des containers (docker ps -a), mais nï¿½est plus en cours dï¿½exï¿½cution.


**Question 10 :**
Commande : docker container rm e1b67dc6006c

Constat :
- Cette fois, la suppression fonctionne car le container est arrï¿½tï¿½.
- Le container disparaï¿½t de la liste (docker ps -a).


**Question 11 :**
Commande : docker image rm nginx:1.20

Constat :
- Comme le container a ï¿½tï¿½ supprimï¿½, lï¿½image peut maintenant ï¿½tre supprimï¿½e sans erreur.
- Lï¿½image disparaï¿½t de la liste (docker image ls).


**Question 13 :**
Commande : docker container run -d --name http nginx:1.29

Constat :
- Docker renvoie une erreur : 'Conflict. The container name '/http' is already in use'.
- On ne peut pas crï¿½er deux containers avec le mï¿½me nom.
- Solution : soit supprimer lï¿½ancien container http, soit lancer le nouveau avec un autre nom (ex: http3).


**Question 17 :**
Commande : docker container run -d --name http2 -p 8081:80 nginx:1.29

Constat :
- Docker renvoie une erreur : 'port is already allocated'.
- On ne peut pas publier deux containers sur le mï¿½me port hï¿½te.
- Solution : utiliser un autre port (ex. -p 8082:80).


**Question 21 :**
Commande : navigateur ? http://localhost:8081

Constat :
- Aucun effet car le container http2 est inactif.
- Le navigateur affiche toujours la page de http.


**Question 22 :**
Commande : docker container unpause http2

Constat :
- Comme le container nï¿½ï¿½tait pas en pause (il nï¿½a jamais dï¿½marrï¿½ correctement), la commande ï¿½choue.


**Question 25 :**
Commande : navigateur ? http://localhost:8082

Constat :
- La page par dï¿½faut de Nginx sï¿½affiche, car le rï¿½pertoire html est vide.


**Question 27 :**
Commande : navigateur ? http://localhost:8082

Constat :
- Le contenu du fichier index.html local sï¿½affiche ï¿½ la place de la page par dï¿½faut.


**Question 30 :**
Commande : navigateur ? http://localhost:8083

Constat :
- La page par dï¿½faut de Nginx sï¿½affiche car le volume http-src est encore vide.


**Question 32 :**
Commande : navigateur ? http://localhost:8083

Constat :
- La page affiche maintenant le contenu du fichier index.html copiï¿½ dans le volume.


**Question 34 :**
Commande : navigateur ? http://localhost:8084

Constat :
- La page affiche le mï¿½me contenu que http4 (volume partagï¿½).


**Question 39 :**
Commande : Modification du fichier config/default.conf

Constat :
- Suppression des lignes 8-11 (ancien bloc location) et remplacement par le proxy vers http5.
- Le fichier de configuration est maintenant prï¿½t pour le reverse proxy.


**Question 41 :**
La page http://localhost:8085 s'affiche correctement. Le container http6 agit comme proxy et redirige les requÃªtes vers http7 sans problÃ¨me.



**Question 45 :**
Commande : docker logs -f sur http5, http6, http7, http8

Constat :
- Les logs montrent le flux des requêtes HTTP entre les containers.
- On observe les requêtes entrantes sur http6 et http8, et les redirections vers http7.
- La résolution des noms de containers dans le réseau Docker fonctionne correctement.


**Question 46 :**
Commande : navigateur ? http://localhost:8083, 8084, 8085, 8086

Constat :
- http://localhost:8083 (http4) et 8084 (http5) : affichent le contenu du volume partagé.
- http://localhost:8085 (http6) et 8086 (http8) : fonctionnent comme proxy vers http7.
- Tous les containers sont opérationnels et communiquent correctement.


**Question 50 :**
Après avoir exécuté 'nginx -s reload' dans le container http6, la configuration Nginx a été rechargée sans redémarrage. Le proxy continue de fonctionner normalement.

