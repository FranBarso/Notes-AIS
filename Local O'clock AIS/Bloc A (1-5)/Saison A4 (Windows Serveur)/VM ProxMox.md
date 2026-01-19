Cours du 19/11/2025
# Installation de WS sur ProxMox

## Créer la VM :
![[Pasted image 20251203140001.png]]
**Général** : Nommer la VM (9002 pour moi)
![[Pasted image 20251203140045.png]]
**OS** : choisir l’image ISO, l’OS et sa version
![[Pasted image 20251203140125.png]]
**Système** : choisir local pour stockage
![[Pasted image 20251203140158.png]]
**Disques** : Bus SATA, taille selon besoin
![[Pasted image 20251203140251.png]]
**Processeur** : 2 cœurs + Si jamais, on a besoin de créer de la virtualisation (VM dans VM) choisir Type « Host »
![[Pasted image 20251203140722.png]]
**Mémoire** : Selon besoin
![[Pasted image 20251203140748.png]]
**Réseau** : attention où on se connecte (dans ce cas au pont **vmbr2**) + désactiver le **pare-feu** (pour ne pas se rajouter des sources potentielles de problèmes, car on a déjà un pare-feu activé dans WS) + **Intel E1000** comme modèle de base (carte classique)
![[Pasted image 20251203140830.png]]
Puis l’installation de l’OS en question.

Mdp de pratique : **rocknroll(25 !)**
