VPC Peering Inter-Régions sur AWS
Mise en place d'une connexion réseau privée entre deux VPC AWS situés dans deux régions différentes, avec validation de la connectivité de bout en bout.

---
Objectif du projet
Établir une connexion privée (VPC Peering) entre deux VPC AWS aux CIDR disjoints, situés dans deux régions différentes, en travaillant en binôme — chacun administrant son propre VPC — puis valider la connectivité par un test réseau réel.
Architecture
```
   Région eu-west-3 (Paris)              Région eu-west-2 (Londres)
┌───────────────────────────┐         ┌───────────────────────────┐
│   VPC-Fawzia               │         │   VPC-Binôme              │
│   CIDR : 10.0.0.0/16       │         │   CIDR : 20.0.0.0/16      │
│                            │         │                           │
│   Sous-réseau public       │         │   Sous-réseau public     │
│   10.0.1.0/24              │  VPC    │   20.0.1.0/24            │
│                            │ Peering │                           │
│   EC2                      │◀───────▶│   EC2                    │
│   Apache HTTPD :80         │ pcx-xxx │   Apache HTTPD :80       │
│   10.0.1.149                │         │   20.0.1.169             │
└───────────────────────────┘         └───────────────────────────┘
        trafic privé sur le backbone AWS — aucun passage par Internet
```
Stack technique
Catégorie	Technologies
Réseau cloud	AWS VPC, VPC Peering inter-régions, Internet Gateway
Routage	Tables de routage, routes CIDR distantes
Sécurité	Security Groups (pare-feu stateful), règles HTTP/ICMP
Compute	AWS EC2 (Amazon Linux 2023), Apache HTTPD
Diagnostic réseau	curl, ping, EC2 Instance Connect
Ce qui a été réalisé
Création d'un VPC dédié (10.0.0.0/16) en région Paris (eu-west-3)
Configuration du sous-réseau public, de l'Internet Gateway et de la table de routage
Déploiement d'un serveur web Apache sur EC2
Création de la connexion de peering avec le VPC du binôme (région Londres)
Configuration du routage croisé (route vers le CIDR distant via pcx)
Ouverture des Security Groups pour autoriser HTTP/ICMP depuis le CIDR distant
Validation de la connectivité par curl dans les deux sens
Résultat de validation
```
# Depuis la VM (Fawzia) — test vers le serveur du binôme
$ curl http://20.0.1.169
<title>It works! Apache httpd</title>
<p>It works!</p>
```
Le trafic transite bien par le réseau privé AWS, sans passer par Internet.
Compétences développées
Conception et configuration d'un VPC AWS from scratch
Compréhension du modèle de routage AWS et du caractère non transitif du peering
Configuration de Security Groups comme pare-feu réseau
Diagnostic réseau méthodique (réseau, routage, pare-feu)
Coordination technique en binôme sur des ressources cloud partagées
---
Le rapport complet est disponible dans ce dépôt : `Rapport_TP_VPC_Peering_Fawzia.pdf`
Contact : LinkedIn — aboubakararike22@gmail.com
