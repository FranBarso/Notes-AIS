Challenge SA2E09, du 30/10/2025
# Challenge SA2-E09 : Principes ITIL & GLPI

1️⃣ **Installer le GLPI Agent** sur une machine virtuelle (ou plusieurs, si vous voulez aller plus loin).

- L’objectif est que vos machines **remontent correctement leurs informations** dans votre instance GLPI (inventaire matériel, logiciels, etc.).
- Vérifiez que la communication entre l’agent et le serveur GLPI fonctionne bien.

2️⃣ **Tester la gestion des tickets dans GLPI** :

- Créez quelques tickets pour simuler des demandes utilisateurs.
- Testez **le cycle de vie complet d’un ticket** : création, attribution, suivi, clôture.
- Explorez les **fonctionnalités utiles au support** : ajout de commentaires, changement de statut, notifications, etc.

## Partie 1 : GLPI Agent sur MV

Pour l’**installation**, j’ai choisi Windows Installer et installé la version typique :

![[Pasted image 20251030205138.png]]
*Après installation, je peux la voir comme une application même si elle n’ouvre pas

![[Pasted image 20251030205218.png]]
### Remonter correctement les informations :

Selon instructions pour Windows installer, on doit rajouter l’option **« /i / quiet** » dans l’invite de commandes en tant qu’administrateur, et pour cela il faut savoir où on place l’application :
![[Pasted image 20251030205324.png#center]]
![[Pasted image 20251030205347.png]]

Je vois dans les logs de l’agent le **port 62354**

![[Pasted image 20251030205430.png]]

Alors, je l’ai ouvert sur un site web pour **forcer un inventaire** :

![[Pasted image 20251030205509.png#center]]
### Vérification de la communication entre l’agent et le serveur GLPI

![[Pasted image 20251030205544.png]]
## Partie 2 : Tester la gestion des tickets dans GLPI 

### Création d’un ticket
Assistance > + Créer un ticket : Remplir détails
![[Pasted image 20251030205627.png]]

Le ticket peut être **aperçu** sur Assistance > Tickets

![[Pasted image 20251030205711.png]]
### Attribution de ticket

Pour l’**attribution** il n’y a pas de limite :
![[Pasted image 20251030205736.png#center]]
### Suivi de ticket
**Plusieurs options** possibles selon le cas, comme « Ajouter une solution »

![[Pasted image 20251030205839.png]]

Ce qui rendra le ticket en tant que « **Résolu** »

![[Pasted image 20251030205908.png]]

Dans l’idéal, la solution proposée est **acceptée** :

![[Pasted image 20251030205949.png]]

Ce qui rendra le ticket « **Clos** » et ne proposera plus de modification (à sa place il me présente une corbeille pour effacer) :
![[Pasted image 20251030210016.png]]

L’**Historique** du ticket sera toujours là pour nous montrer toute sa trajectoire :

![[Pasted image 20251030210053.png]]



