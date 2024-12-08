# NFtables
---
Toute la config de Netfilter par nftables, passe par une commande : nft. Toujours en tant que root.  

* Création d'une table :  
`nft add table ip mon_filtreIPv4`  
`add table` qui décrit l'action que nous voulons faire. `ip` précise la famille de table, ici IPv4.

* Lister les tables
`nft list tables` pour avoit toutes les tables. il faut bien mettre un "s" à tables. On peut également trier les les tables d'affichage.  
![Capture d'écran 2024-12-08 114856](https://github.com/user-attachments/assets/52849a42-e4d3-4a27-a013-b06ab58ca30a)


