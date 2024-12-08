# NFtables
---
Toute la config de Netfilter par nftables, passe par une commande : nft. Toujours en tant que root.  

### I. Gestion des tables
* Création d'une table :  
`nft add table ip mon_filtreIPv4`  
`add table` qui décrit l'action que nous voulons faire. `ip` précise la famille de table, ici IPv4.

* Lister les tables
`nft list tables` pour avoit toutes les tables. il faut bien mettre un "s" à tables. On peut également trier les les tables d'affichage.  
![Capture d'écran 2024-12-08 114856](https://github.com/user-attachments/assets/52849a42-e4d3-4a27-a013-b06ab58ca30a)

* Supprimer table
Ex : `nft delete table ip6 mon_filtreIPv6`

### II. Gestion des chaines  
* Créer une chaine dans nftables  
![Capture d'écran 2024-12-08 121402](https://github.com/user-attachments/assets/53ffe043-42f6-4711-b985-10bb39aad4ff)

* Lister les chaines  
`nft list table ip mon_filtreIPv4`  
![Capture d'écran 2024-12-08 121521](https://github.com/user-attachments/assets/c78f36c7-4d9f-4fb0-aab2-9a2b434dd4ba)

* Supprimer une chaine
Exemple : `nft delete chain ip filtre2 input`  

### III. Gestion des règles dans nftables
* Créer des règles (ci-dessous, autoristaion d'entrée et sortie des ports 80 et 443 et onbandonne le reste.
![Capture d'écran 2024-12-08 171413](https://github.com/user-attachments/assets/33db2984-6592-4d8d-8b87-a5af031cb53e)


## Résolution de l'exercice  
---

* mon service web est accessible en HTTP, mais aussi en HTTPS;
* mes sites web ont besoin, pour contacter d'autres services web, d'effectuer des requêtes en HTTPS seulement (en tant que client), attention au DNS ;));
* je gère mon service web en SSH sur le port TCP/1022;
* mon serveur mail sera amené à questionner des serveurs NTP externes à et envoyer des mails sur des ports TCP/587;
* je souhaite également mettre en place un peu de sécurité en comptant les paquets TCP de types NULL ou XMAS, cela dénote un comportement anormal. Nous allons également les bloquer;
* tout ce qui n'est pas explicitement autorisé sera refusé;
* mon serveur pourra pinguer, mais ne pas être pingué.

Création de la table :  
`nft add table ip mon_filtreIPv4`  

#### Création de la chaine pour les INPUT et OUTPUT :  

![Capture d'écran 2024-12-08 152528](https://github.com/user-attachments/assets/a74a95fd-c2b5-4f54-b1f7-27f638599b7c)

#### Ajout des accessibiltés HTTP et HTTPS :  
Le site est accessible en HTTP et HTTPS mais ne renvoie qu'en HTTPS  
![Capture d'écran 2024-12-08 152621](https://github.com/user-attachments/assets/8f0a1b2f-bfbb-4de0-8f7d-3d33df36ebf8)


#### Ouverture du port 1022  
On ouvre le port 1022 pour gérer ce serveur (web), donc en input.  
![Capture d'écran 2024-12-08 153123](https://github.com/user-attachments/assets/389f814d-7d2b-464c-9f66-7425c1fac238)
![Capture d'écran 2024-12-08 153143](https://github.com/user-attachments/assets/34d83fe3-9aef-4285-9ab5-efed1b3887e6)

#### Mon serveur pourra pinguer, mais ne pas être pingué  
On accepte les request depuis le serveur, mais pas depuis l'extérieur. On accepte les reply de puis l'extérieur mais pas depuis l'intérieur. Donc on peut pinger mais on ne peut pas être pingé.  
![Capture d'écran 2024-12-08 153905](https://github.com/user-attachments/assets/10e93920-e0a8-4730-a34e-4b34d76eff7b)
![Capture d'écran 2024-12-08 154024](https://github.com/user-attachments/assets/8eec3a30-ec84-41c7-98ce-91b37516274d)

#### Je souhaite également mettre en place un peu de sécurité en comptant les paquets TCP de types NULL ou XMAS, cela dénote un comportement anormal. Nous allons également les bloquer  
![Capture d'écran 2024-12-08 161915](https://github.com/user-attachments/assets/e7b13f75-19c3-40de-823d-4896350f422f)
![Capture d'écran 2024-12-08 155915](https://github.com/user-attachments/assets/d33d065b-599d-47dc-86ae-426b5b8e5370)

#### Mon serveur mail sera amené à questionner des serveurs NTP externes à et envoyer des mails sur des ports TCP/587  
Autoriser les requêtes NTP (UDP port 123)  
![Capture d'écran 2024-12-08 163130](https://github.com/user-attachments/assets/fa7ea739-acb9-4dc9-b604-c2fc3fdb47d5)
Autoriser l'envoi d'e-mails via SMTP sécurisé (TCP port 587)  
![Capture d'écran 2024-12-08 163137](https://github.com/user-attachments/assets/18120edc-869a-414d-ae37-8b6c7e5ee26b)


#### Tout ce qui n'est pas explicitement autorisé sera refusé  
A la fin on finit les chaines avec un "drop" pour rejeter tout le reste. Cette étape se fait en dernier sur le `input` et `output`  

![Capture d'écran 2024-12-08 164048](https://github.com/user-attachments/assets/2e35e567-794d-4ff8-970d-29bccd7b40e0)

![Capture d'écran 2024-12-08 164056](https://github.com/user-attachments/assets/41b3b32d-25dc-4bc9-ab7a-ae7142e2ae74)

 ### :white_check_mark: On devrait obtenir quelque chose comme ça (pas forcément dans le même ordre, sauf les "drop" toujours en dernier (et des handles différents ^^) :  
![Capture d'écran 2024-12-08 164817](https://github.com/user-attachments/assets/99c38b70-2ea9-4d50-a05d-d7750bd1e0a4)
