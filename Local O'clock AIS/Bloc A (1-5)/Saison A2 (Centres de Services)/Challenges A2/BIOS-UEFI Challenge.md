# Challenge SA2-E06 : [[BIOS, UEFI...]]

- Accédez au BIOS de votre ordinateur, et explorez les différentes pages, sections et réglages proposés !

- ⚠️ Ne modifiez rien, vous risqueriez d’empêcher votre ordinateur de démarrer.
- Prenez des photos des pages ou des réglages que vous ne comprenez/connaissez pas.
- Pour ceux qui sont sur Mac, pas de BIOS dispo ! Vous pouvez explorer ce [simulateur en ligne](https://l.oclock.io/andromede-technicien-support-it-854ada6c557d64d4c9d71322d397f5bf) . ou [celui-ci](https://l.oclock.io/andromede-technicien-support-it-2d06d5739f2508d8eec5b6db68bc43d4) ou [encore lui](https://l.oclock.io/andromede-technicien-support-it-dcfb4ea81259b23bbf3a6e14b722ee4b)

- Sauvegardez les données d’une clé USB, puis tentez de :

- convertir sa table de partitions de MBR à GPT (ou l’inverse) à l’aide de l’utilitaire DiskPart (depuis une VM Windows, si vous êtes sous MacOS)
- créer plusieurs partitions sur cette clé et tester de les formater avec différents systèmes de fichiers : NTFS, FAT32 et ExFAT
- testez la compatibilité avec les différents systèmes d’exploitation (en connectant la clé USB sur des VMs VirtualBox)

💡 Vous devrez potentiellement réussir à connecter une clé USB sur une VM VirtualBox. À vous de trouver comment faire !

## Partie 1 : Accès au BIOS de mon ordinateur

### Méthode classique

**F2** dès que le logo apparaît

### Méthode via Windows (si le démarrage rapide bloque l’accès)

**Paramètres** > **Mise à jour et sécurité** > **Récupération**

Sous « Démarrage avancé » : **Redémarrer maintenant**

Une fois dans le menu bleu, choisir **Dépannage** > **Options avancées** > **Paramètres du firmware UEFI** > **Redémarrer**

J’ai toujours pensé que j’avais un BIOS, mais avec cette exercice je me suis rendu compte que c’est un UEFI, selon le Boot Mode ci-dessous (désolé pour la qualité des images) :

![[Pasted image 20251031134556.png]]

Tout ce que je ne comprends pas se trouve sur :

1.1.           Main :

Network Boot

F12 Boot Menu

Wake on LAN

USB/TBT wake from S4 Support

Function key behavior

Wake on USB while lid closed

D2D Recovery

Keyboard backlight timeout

Fast Boot

![[Pasted image 20251031134631.png]]

### 1.2.           Security (tout ce qui est password)

Set Supervisor Password

Change Supervisor Password

Set User Password

Change User Password

Password on Boot

Secure Boot Mode

Erase all Secure Boot Setting

Select an UEFI file as trusted for executing

Restore Secure Boot to Factory Default

TPM type

Current TPM (TCM) State

Change TPM (TCM) State

Clear TPM (TCM)

![[Pasted image 20251031134707.png]]

## Partie 2 : Modifications sur la clé USB

### 2.1. Formatage de la clé USB :

Par défaut, elle est déjà en système de fichier Fat32, comme nous pouvons le constater dans « Gestion des disques » :

![[Pasted image 20251031135154.png]]

Si je la formate (encore) en Fat32, rien ne change :

![[Pasted image 20251031135117.png]]

J’essaie de voir ses volumes (pour savoir son type de partitions -MBR ou GPT-) mais tout est blanc :

![[Pasted image 20251031135308.png#center]]

Alors, je me rends sur « **Diskpart** » pour regarder plus loin : Ma clé USB (Disque 3) n’est pas partitionnée en **GPT** (absence d’étoile en fin de ligne de sa description) :

![[Pasted image 20251031135446.png#center]]

Donc je fais la conversion de **MBR** à **GPT** :

![[Pasted image 20251031135524.png#center]]

La conversion à GPT a fait disparaître la clé USB de la liste de disques :

![[Pasted image 20251031135559.png]]

Alors, je refais la conversion de GPT à MBR sur diskpart, pour pouvoir procéder à **formater** le système de fichier en **NTFS** et constater le résultat sur la liste de disques :

![[Pasted image 20251031135635.png#center]]

Pour que la clé apparaisse

![[Pasted image 20251031140752.png]]

### 2.2. Création de plusieurs partitions :

**Note** : après la conversion à GPT, la clé USB n’apparaissait plus dans mon gestionnaire des disques car je n’avais pas appliqué le « diskpart » en tant qu’**administrateur de l’invite de commandes** (**cmd**). Alors j’ai refait la procédure en rajoutant les commandes « diskpart » de partition et formatage en Fat32 : **create partition primary** > **format fs=fat32 quick** > **assign** > **exit**

Une fois la clé USB récupérée, j’ai « **réduit le volume** » à partir de Gestion des disques (après formatage, elle a changé à G : et la partition est devenue F : ).

![[Pasted image 20251031140926.png]]
### 2.3. Lecture clé USB sur VirtualBox

### Sur Windows 11 VM

Je démarre ma VM pour chercher le périphérique en question : Périphériques > USB > sélection

![[Pasted image 20251031140959.png]]
### Sur Debian 13 VM

Même procédure qu’avec Windows 11

![[Pasted image 20251031141036.png]]

### Récupération du volume et la partition d’origine de la clé USB

Supprimer volume > Nouveau volume simple

![[Pasted image 20251031141153.png]]

Même opération avec (F : ) pour lui attribuer le même système fichier (Fat32)

![[Pasted image 20251031141257.png]]

Et même procédure « diskpart » en tant qu’**administrateur de l’invite de commandes** (**cmd**) :

![[Pasted image 20251031141341.png]]

![[Pasted image 20251031141407.png]]
