VPC Peering Inter-Régions sur AWS
Mise en place d'une connexion réseau privée entre deux VPC AWS situés dans deux régions différentes, avec validation de la connectivité de bout en bout.
Auteure : Fawzia Aboubakar — Mastère Expert Informatique & SI, EPSI Lyon
Module : Réseaux & Cloud Computing
Date : Juin 2026
---
Contexte
Travail réalisé en binôme : chaque étudiant administre son propre VPC, dans une région AWS différente. L'objectif est d'établir une connexion privée (VPC Peering) entre les deux VPC, puis de valider la connectivité par un test réseau réel.
Paramètre	Mon VPC (Paris)	VPC du binôme (Londres)
Région	eu-west-3	eu-west-2
CIDR	10.0.0.0/16	20.0.0.0/16
Sous-réseau public	10.0.1.0/24	20.0.1.0/24
Serveur web	Apache HTTPD :80	Apache HTTPD :80
Stack technique
AWS VPC · VPC Peering inter-régions · Security Groups · Tables de routage · EC2 (Amazon Linux 2023) · Apache HTTPD · curl / ping
Ce qui a été réalisé
Création du VPC, du sous-réseau public, de l'Internet Gateway et de la table de routage
Déploiement d'un serveur web Apache sur EC2
Création de la connexion de peering avec le VPC du binôme
Configuration du routage croisé entre les deux VPC
Ouverture des Security Groups pour autoriser HTTP/ICMP depuis le CIDR distant
Validation de la connectivité par curl dans les deux sens
Résultat de validation
```
$ curl http://20.0.1.169
<title>It works! Apache httpd</title>
<p>It works!</p>
```
Le trafic transite par le réseau privé AWS, sans passer par Internet.
Compétences développées
Conception d'un VPC AWS · compréhension du routage et du caractère non transitif du peering · configuration de Security Groups · diagnostic réseau méthodique · coordination technique en binôme sur des ressources cloud partagées
---
Rapport complet : `Rapport_TP_VPC_Peering_Fawzia.pdf`
Contact : LinkedIn — aboubakararike22@gmail.com
