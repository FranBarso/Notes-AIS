# Accès au BIOS / UEFI
Les **touches d’accès au BIOS / UEFI** les plus courantes selon la marque 👇: 

![[Pasted image 20260110113235.png]]
# Prérequis minimums officiels

Voici les **prérequis minimums officiels** pour installer **Windows 11** sur une machine physique 👇:

![[Pasted image 20260110113601.png]]
# Voir le Processeur Win10
Voici plusieurs façons de voir les **caractéristiques de ton processeur (CPU)** sous **Windows 10** 👇:
1. Depuis le **Gestionnaire des tâches**
	- **Ctrl + Shift + Esc**
	- Onglet **Performances -> Processeur**
		=> On y voit: nom du CPU, sa vitesse (**GHz**), le nombre de cœurs et de threads, et l'utilisaten en temps réel. 
		
2. Depuis les **Informations système**
	- **Win + R** pour taper `msinfo32` **entrée**
		=> Regarder la ligne **Processeur** : modèle complet (i.e. *Intel Core i7-1165G7 @ 2.80GHz*)
		
3. Avec **PowerShell** ou l’Invite de commandes
	- Taper: `Get-CimInstance Win32_Processor | Select-Object Name, NumberOfCores, NumberOfLogicalProcessors`
		=> On y voit le nom du CPU, le nombre de **cœurs physiques** et de **threads (logiques)**.
		
4. Commande rapide sur le **terminal (cmd)**:
	- taper la commande `wmic cpu get name`
		=> Affiche uniquement le nom du processeur

# Voir la RAM
Voici les façons les plus simples de voir la **mémoire RAM** sur Windows 10 👇:

1. Depuis le **Gestionnaire des tâches**
	- **Ctrl + Shift + Esc**
	- Onglet **Performances -> Mémoire**
		=> On y voit : **Quantité totale** de RAM installée, la **vitesse (MHz)**, Le **type** (DDR3, DDR4, DDR5) et le **nombre d'emplacements utilisés / disponibles**.
		
2. Depuis les **Informations système**
	- **Win + R** pour taper `msinfo32` **entrée**
		=> Regarder la ligne **Mémoire physique totale installée** 
		
3. Avec **PowerShell**
	- Taper `Get-CimInstance Win32_ComputerSystem | Select-Object TotalPhysicalMemory` 
		 => Le résultat est en **octets** (diviser par 1.073.741.824 pour avoir les **Go**).
	
4. Depuis ligne de commande **(terminal ou cmd)**:
	- Taper: `systeminfo | find "Mémoire physique totale"`

# Voir le stockage
Voici plusieurs façons de voir le **stockage (disques, SSD/HDD, partitions)** sous **Windows 10** 👇:

1. Depuis **Explorateur de fichiers**
	- **Win + E**
	- Clic **Ce PC**
		=> On y voit : chaque disque avec son **nom (C:, D:...)**, la **capacité totale** et l'**espace libre**.
		
2. Depuis la **Gestion du disque**
	- **Win + X** et choisir **Gestion du disque**
		=> On y voit: Le **type de disque** (de base, dynamique), les **partitions**, leur **système de fichiers (NTFS, FAT32)** et l'**espace non alloué**. 
		
3. Depuis **les Paramètres**
	- **Démarrer -> Paramètres -> Système -> Stockage**
		=> On y voit combien d'espace est utilisé et par quoi (applications, fichiers, etc.).
		
4. Avec **PowerShell**
	- Taper `Get-PhysicalDisk | Select FriendlyName, MediaType, Size` 
		 => Indique le **type** (SSD ou HDD) et la **taille** de chaque disque.
	
5. En ligne de commande **(terminal ou cmd)**:
	- Taper: `wmic diskdrive get model,name,size,mediatype`
		=> Montre le **modèle exact**, le **nom du lecteur**, la **capacité** et le **type**.

# Voir le Firmware system
Voici les façons les plus simples de **voir le type de firmware système** (UEFI ou BIOS classique) sur **Windows 10** 👇

1. Depuis les **Informations système**, à travers la fenêtre **Exécuter**:
	- **Win + R** pour taper `msinfo32` **entrée**
		=> Regarder la ligne **Mode BIOS** 
		- **UEFI** -> Le PC utilise UEFI
		- **Hérité (Legacy)** -> Le PC utilise l'ancien BIOS

2. Depuis **PowerShell**:
	- Taper `Get-WmiObject -Class Win32_ComputerSystem | Select-Object BootupState` ou bien `Confirm-SecureBootUEFI` 
		=> Si la commande retourne **True**, le système est en **UEFI** (et Secure Boot activé). Si elle retourne une erreur, on est probablement en **Legacy BIOS**.

3. Depuis le **Gestionnaire de disques**:
	- **Win + X** 
	- Clic droit sur le **disque système (C:) -> Propriétés -> Volumes**
		=> Regarder la ligne **Style de partition**
		- **GPT** = UEFI
		- **MBR** = BIOS hérité

# Voir le TPM

Voici plusieurs méthodes fiables pour **vérifier la présence et la version du TPM** (Trusted Platform Module) sur ton PC Windows 10 👇

1. Depuis la Sécurité/Contrôle, à travers la fenêtre **Exécuter**:
	- **Win + R** pour taper `tpm.msc` **entrée**
		=> Une fenêtre **Gestion du module de plateforme sécurisée** s'ouvre:
		- Si l'on voit **“Le TPM est prêt à être utilisé”**, le PC en a un.
		- Regarde **Version de spécification** : 
			-  **2.0** ✅ = compatible Windows 11
			- **1.2** ⚠️ = compatible seulement via contournement

2. Depuis **PowerShell**:
	- Taper `Get-Tpm`
		=> Résultat :
		- `TpmPresent : True` → il y a un TPM 
		- `TpmReady : True` → il est activé
		- `SpecVersion : 2.0` → version utilisée
  
3. Depuis l'outil **Informations système**, à travers la fenêtre **Exécuter**:
	- **Win + R** pour taper `msinfo32`
		=>Regarder la ligne **État du module de plateforme sécurisée**:
		- Si elle dit “Présent” et “Version 2.0” → parfait.
		- Si “Non présent” ou “Désactivé”, il faut l’activer dans le BIOS/UEFI.

4. Depuis le **BIOS**:
Redémarrer → entrer dans le **BIOS/UEFI**  
Chercher une section nommée :
- _Security_, _Advanced_, ou _Trusted Computing_
- Option **TPM**, **PTT (Intel)** ou **fTPM (AMD)**  
    ➡️ Vérifier qu’il est **activé**.

# Voir Carte Graphique (GPU)

Voici les façons simples de **voir la carte graphique (GPU) et sa version** sous **Windows 10** 👇:

1. Depuis le **Gestionnaire de périphériques**, à travers la fenêtre **Exécuter**:
	- **Win + R** pour taper `devmgmt.msc`
	- Déployer **Cartes graphiques**
		=> On y voit le **modèle exact** (Intel / NVIDIA / AMD).
		Pour la version du pilote:
		- Double-clique sur la carte
		- - Onglet **Pilote** → **Version du pilote**

2. Depuis le **Gestionnaire des tâches**:
	- Ctrl + Shift + Esc
	- Onglet **Performances → GPU**
		=> On y voit: Modèle du GPU + utilisation en temps réel.
		
3. Depuis **Diagnostic DirectX**, à travers la fenêtre **Exécuter**:
	- **Win + R** pour taper `dxdiag`
	- Onglet **Affichage** où on voit:
		- Nom de la carte graphique
		- Mémoire vidéo
		- Version du pilote
		- Support DirectX (utile pour Windows 11 / jeux)

4. Depuis ligne de commande **(terminal ou cmd)**:
	- Taper `wmic path win32_VideoController get name,driverversion`

### 🧠 À retenir
- **Modèle GPU** → compatibilité
- **Version du pilote** → stabilité & performances    
- **DirectX 12 + WDDM 2.0** → requis pour Windows 11

### 🧠 Règle simple à retenir
- GPU **Intel HD/UHD Gen 6+** → OK    
- **NVIDIA GTX série 700+** → OK    
- **AMD Radeon RX** → OK    
- GPU trop ancien → Windows 11 refusé (sauf contournement)

# Voir Écran

Voici comment **vérifier si l'écran est compatible avec Windows 11** 👇

### ✅ **Exigences Windows 11 pour l’écran**
- **Résolution minimale** : **1280 × 720 (HD)**    
- **Taille** : **≥ 9 pouces**    
- **Profondeur de couleur** : **8 bits par couleur**

1. Via **Paramètres**:
	- Clic droit sur le bureau -> **Paramètres d'affichage**
		=> On vérifie **Résolution d’affichage** (ex. 1920×1080 → OK) et Échelle et disposition.
		
2. Avec **DxDiag**, à travers la fenêtre **Exécuter**:
	- **Win + R** pour taper `dxdiag`
	- Onglet **Affichage** où on Vérifie la résolution et le périphérique d’affichage.
		
3. Depuis ligne de commande **(terminal ou cmd)**:
	- Taper `wmic desktopmonitor get screenheight,screenwidth`
		=> Si largeur ≥ **1280** et hauteur ≥ **720** → compatible.

### 🧠 **Conclusion rapide**
- **Écran HD ou Full HD** → ✅ compatible     
- **Très ancien écran < 720p** → ❌ non compatible (rare sur laptop)






