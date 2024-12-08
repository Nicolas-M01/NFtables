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

