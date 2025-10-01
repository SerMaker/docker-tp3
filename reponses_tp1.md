
**Question 4 :**
Commande : docker image ls

Constat :
- L�image nginx:latest correspond � la version 1.29 (m�me IMAGE ID 41f689c20910 ).
- Donc quand on fait docker pull nginx sans version, Docker t�l�charge l�image la plus r�cente (1.29).
- On a bien trois images disponibles : nginx:1.20, nginx:1.29 et nginx:latest.


**Question 7 :**
Commande : docker image rm nginx:1.20

Constat :
- Docker renvoie une erreur.
- L�image nginx:1.20 ne peut pas �tre supprim�e car elle est utilis�e par un container en cours d�ex�cution (e1b67dc6006c).


**Question 8 :**
Commande : docker container rm e1b67dc6006c

Constat :
- Docker renvoie une erreur car on ne peut pas supprimer un container qui est encore en cours d�ex�cution.
- Message d�erreur typique : 'cannot remove a running container'.
- Pour le supprimer, il faut d�abord l�arr�ter avec docker container stop.


**Question 8 :**
Commande : docker container rm e1b67dc6006c

Constat :
- Docker renvoie une erreur car on ne peut pas supprimer un container qui est encore en cours d�ex�cution.
- Message d�erreur typique : 'cannot remove a running container'.
- Pour le supprimer, il faut d�abord l�arr�ter avec docker container stop.


**Question 9 :**
Commande : docker container stop e1b67dc6006c

Constat :
- Le container s�arr�te correctement.
- Apr�s l�arr�t, il reste pr�sent dans la liste des containers (docker ps -a), mais n�est plus en cours d�ex�cution.


**Question 10 :**
Commande : docker container rm e1b67dc6006c

Constat :
- Cette fois, la suppression fonctionne car le container est arr�t�.
- Le container dispara�t de la liste (docker ps -a).


**Question 11 :**
Commande : docker image rm nginx:1.20

Constat :
- Comme le container a �t� supprim�, l�image peut maintenant �tre supprim�e sans erreur.
- L�image dispara�t de la liste (docker image ls).


**Question 13 :**
Commande : docker container run -d --name http nginx:1.29

Constat :
- Docker renvoie une erreur : 'Conflict. The container name '/http' is already in use'.
- On ne peut pas cr�er deux containers avec le m�me nom.
- Solution : soit supprimer l�ancien container http, soit lancer le nouveau avec un autre nom (ex: http3).


**Question 17 :**
Commande : docker container run -d --name http2 -p 8081:80 nginx:1.29

Constat :
- Docker renvoie une erreur : 'port is already allocated'.
- On ne peut pas publier deux containers sur le m�me port h�te.
- Solution : utiliser un autre port (ex. -p 8082:80).


**Question 21 :**
Commande : navigateur ? http://localhost:8081

Constat :
- Aucun effet car le container http2 est inactif.
- Le navigateur affiche toujours la page de http.


**Question 22 :**
Commande : docker container unpause http2

Constat :
- Comme le container n��tait pas en pause (il n�a jamais d�marr� correctement), la commande �choue.


**Question 25 :**
Commande : navigateur ? http://localhost:8082

Constat :
- La page par d�faut de Nginx s�affiche, car le r�pertoire html est vide.


**Question 27 :**
Commande : navigateur ? http://localhost:8082

Constat :
- Le contenu du fichier index.html local s�affiche � la place de la page par d�faut.


**Question 30 :**
Commande : navigateur ? http://localhost:8083

Constat :
- La page par d�faut de Nginx s�affiche car le volume http-src est encore vide.


**Question 32 :**
Commande : navigateur ? http://localhost:8083

Constat :
- La page affiche maintenant le contenu du fichier index.html copi� dans le volume.


**Question 34 :**
Commande : navigateur ? http://localhost:8084

Constat :
- La page affiche le m�me contenu que http4 (volume partag�).


**Question 39 :**
Commande : Modification du fichier config/default.conf

Constat :
- Suppression des lignes 8-11 (ancien bloc location) et remplacement par le proxy vers http5.
- Le fichier de configuration est maintenant pr�t pour le reverse proxy.


**Question 41 :**
La page http://localhost:8085 s'affiche correctement. Le container http6 agit comme proxy et redirige les requêtes vers http7 sans problème.



**Question 45 :**
Commande : docker logs -f sur http5, http6, http7, http8

Constat :
- Les logs montrent le flux des requ�tes HTTP entre les containers.
- On observe les requ�tes entrantes sur http6 et http8, et les redirections vers http7.
- La r�solution des noms de containers dans le r�seau Docker fonctionne correctement.


**Question 46 :**
Commande : navigateur ? http://localhost:8083, 8084, 8085, 8086

Constat :
- http://localhost:8083 (http4) et 8084 (http5) : affichent le contenu du volume partag�.
- http://localhost:8085 (http6) et 8086 (http8) : fonctionnent comme proxy vers http7.
- Tous les containers sont op�rationnels et communiquent correctement.


**Question 50 :**
Apr�s avoir ex�cut� 'nginx -s reload' dans le container http6, la configuration Nginx a �t� recharg�e sans red�marrage. Le proxy continue de fonctionner normalement.

