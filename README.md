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



### Résolution de l'exercice 

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
![Capture d'écran 2024-12-08 152621](https://github.com/user-attachments/assets/5450b994-d1db-4f85-bc79-781ed69dec47)


#### Ouverture du port 1022  
![Capture d'écran 2024-12-08 153123](https://github.com/user-attachments/assets/389f814d-7d2b-464c-9f66-7425c1fac238)
![Capture d'écran 2024-12-08 153143](https://github.com/user-attachments/assets/34d83fe3-9aef-4285-9ab5-efed1b3887e6)

#### Mon serveur pourra pinguer, mais ne pas être pingué
![Capture d'écran 2024-12-08 153905](https://github.com/user-attachments/assets/10e93920-e0a8-4730-a34e-4b34d76eff7b)
![Capture d'écran 2024-12-08 154024](https://github.com/user-attachments/assets/8eec3a30-ec84-41c7-98ce-91b37516274d)

#### je souhaite également mettre en place un peu de sécurité en comptant les paquets TCP de types NULL ou XMAS, cela dénote un comportement anormal. Nous allons également les bloquer
![Capture d'écran 2024-12-08 161915](https://github.com/user-attachments/assets/e7b13f75-19c3-40de-823d-4896350f422f)
![Capture d'écran 2024-12-08 155915](https://github.com/user-attachments/assets/d33d065b-599d-47dc-86ae-426b5b8e5370)




#### Tout ce qui n'est pas explicitement autorisé sera refusé
A la fn on peut finir les chaines avec un "drop" pour rejeter tout le reste  

