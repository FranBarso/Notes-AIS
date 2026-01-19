Et si on découvrait **Packet Tracer** par la pratique ? 💪

Vous allez devoir ajouter dans un projet Packet Tracer tous les “end devices” (ordinateurs fixes, portables, copieurs, serveurs, etc.) ainsi que les premiers appareils d’interconnexion d’une entreprise fictive, dont le réseau et le parc informatique sont décrits ci-dessous.

Pour l’instant, on oublie le WiFi : on considère que tous les postes sont connectés en filaire.

Pour toutes les adresses IP, on utilise le **masque de sous-réseau 255.0.0.0** soit /8 en notation _classless/CIDR_.

Voici la liste des end devices avec leurs adresses IP (on appelle ça un **plan d’adressage** !) :

1. **Paris (site principal) :
- *Accueil :
- 2 PC fixes, adresses IP en 10.1.1.X (X étant le numéro du poste, de 1 à 2)
- un copieur, adresse IP 10.1.123.1

- *Compta :
- 3 PC fixes, adresses IP en 10.1.2.X (X étant le numéro du poste, de 1 à 3)
- un copieur, adresse IP 10.1.123.2

- *Direction :
- 2 PC portables, adresses IP en 10.1.3.X (X étant le numéro du poste, de 1 à 2)
- une imprimante, adresse IP 10.1.123.3

- *Salle 4 / open-space N°1 :
- 8 PC fixes, adresses IP en 10.10.4.X (X étant le numéro du poste, de 1 à 8)
- un copieur, adresse IP 10.10.123.4
- un switch dédié (utilisez un Cisco 2960 !)

- *Salle 5 / open-space N°2 :
- 12 PC fixes, adresses IP en 10.10.5.X (X étant le numéro du poste, de 1 à 12)
- un switch dédié

- *Service Informatique :
- 1 PC fixe et 2 PC portables, adresses IP en 10.1.42.X (idem pour le X)
- un switch dédié

- *Salle serveur :
- 1 switch pour les PC de l’Accueil, la Compta et la Direction
- 1 switch “cœur de réseau”, sur lequel tous les autres sont connectés !

1. **Lyon :
- *Accueil :
- 2 PC fixes, adresses IP en 10.2.1.X (X étant le numéro du poste, de 1 à 2)
- un copieur, adresse IP 10.2.123.1
- un switch partagé avec la salle 2

- *Salle serveur :
- 1 switch “cœur de réseau”, sur lequel tous les autres sont connectés !

- *Salle 2 / open-space :
- 12 PC fixes, adresses IP en 10.20.2.X (X étant le numéro du poste, de 1 à 12)
- une imprimante, adresse IP 10.20.123.2
- un switch partagé avec l’accueil

Pour l’instant, même si les sites sont géographiquement éloignés, reliez les deux switchs “cœur du réseau” entre eux.

**Bonus :** Vérifiez avec la commande ping si les postes peuvent bien communiquer. Vous l’avez normalement vue en saison 2, mais cherchez sur Internet comment utiliser cette commande si nécessaire (votre formateur n’a peut-être pas eu le temps d’en reparler, la journée était suffisamment chargée 😅) !
## Solution :

### Réseau logique :
Les deux parcs informatiques de l’entreprise fictive partagent le même réseau et toutes les machines peuvent pinguer entre eux.
![[Pasted image 20251104092142.png]]
### Communication entre machines :
Je voudrais tester la communication entre une machine de Paris et une autre de Lyon. Pour pouvoir le faire, il faut rentrer sur la configuration d’une machine -> Desktop et noter son **Adresse IP :** je prends la première machine de l’accueil de Paris (**10.1.1.1**) et la deuxième machine de la Salle 2/ Open space de Lyon (**10.20.2.2**) :
#### Première PC de Paris :
![[Pasted image 20251104092240.png]]
#### Deuxième PC de Lyon :
Même procédure
![[Pasted image 20251104092312.png]]
Ensuite je peux les pinguer (je reviens à la configuration d’une des machines -> **Desktop** -> **Command Prompt**)
![[Pasted image 20251104092404.png]]
Et je peux **pinguer** les deux machines (dans ce cas la deuxième PC de Lyon avec la première PC de Paris) et je constate qu’elles sont bien pinguées :
![[Pasted image 20251104092445.png#center]]
#### Regarder le ping sur simulation :
Il faut tout d’abord filtrer l’événement que je veux regarder (**Ping** : Protocol **ICMP**, ou Internet Control Messaging Protocol), alors je nettoie tous les événements par défaut (**Show All/None**), puis j’**édite les filtres** pour choisir l’**ICMP** :
![[Pasted image 20251104092520.png]]
Et je peux regarder la **trajectoire** du processus de Ping :
![[Pasted image 20251104092546.png#center]]
Jusqu’à ce que le Ping arrive à son **destinataire** :
![[Pasted image 20251104092618.png]]
# Correction 
![[Pasted image 20251104092916.png]]
## Observation:
Pour chaque salle, il faut mettre l'adresse IP base pour ne pas avoir à regarder les notes à chaque fois
### L'imprimante et sa configuration IP

**Note:** Toutes les imprimantes ont le même code Administrateur (soit 1111 ou 1234 ou 0000)
### Astuces pour Pinguer
Avant de pinguer, nous pouvons regarder l'adresse IP de la machine par le **commande prompt** avec la commande **ipconfig** :
![[Pasted image 20251104094844.png]]
On peut aussi Pinguer avec l'**adresse de Broadcast** dans ce cas c'est 10.255.255.255


