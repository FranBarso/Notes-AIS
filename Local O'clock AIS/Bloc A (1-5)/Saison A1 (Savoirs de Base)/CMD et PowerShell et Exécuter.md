**“Invite de commandes”** = **cmd.exe**  
C’est l’interpréteur de commandes classique de Windows (hérité de MS-DOS).

Mais attention :

- **Invite de commandes (cmd)** → ancien outil, basique
    
- **PowerShell** → plus moderne, plus puissant, orienté objets
    

Les deux permettent d’exécuter des commandes, mais certaines ne fonctionnent que dans l’un ou dans l’autre.

Voici un petit **tableau comparatif clair entre CMD et PowerShell**

![[Pasted image 20260110123601.png]]

La fenêtre **Exécuter (Run)** est un outil Windows qui permet de **lancer directement des programmes, commandes ou outils système** sans passer par les menus.

Elle se lance via le raccourci `Win + R`

➡️ Concrètement : tu tapes un **nom de commande**, tu appuies sur **Entrée**, et Windows l’exécute.

**À quoi ça sert ?**
- Accéder rapidement aux **outils système**    
- Lancer des **commandes d’administration**    
- Gagner du temps (plus rapide que les menus)
    
Voici une **liste utile de commandes** que tu peux lancer via **Win + R → Exécuter** (Windows 10/11) :
### 🧰 Outils système

- `cmd` → Invite de commandes  **(connaître par cœur)**  
- `powershell` → PowerShell    **(connaître par cœur)**
- `control` → Panneau de configuration    
- `settings` → Paramètres Windows    
- `taskmgr` → Gestionnaire des tâches    **(connaître par cœur)**
- `services.msc` → Services Windows    **(connaître par cœur)**
- `msconfig` → Configuration du système    
- `eventvwr` → Observateur d’événements  **(connaître par cœur)**
### 🖥️ Informations & diagnostic

- `msinfo32` → Informations système    
- `dxdiag` → Diagnostic DirectX    
- `perfmon` → Moniteur de performances    
- `resmon` → Moniteur de ressources  
### 💾 Disques & matériel

- `diskmgmt.msc` → Gestion des disques & partition    **(connaître par cœur)**   
- `devmgmt.msc` → Gestionnaire de périphériques   **(connaître par cœur)**
### 🔐 Sécurité

- `tpm.msc` → Gestion du TPM    **(connaître par cœur)**
- `secpol.msc` → Stratégie de sécurité locale (Pro)    **(connaître par cœur)**
- `gpedit.msc` → Stratégie de groupe locale (Pro)    **(connaître par cœur)**
### 🌐 Réseau

- `ncpa.cpl` → Connexions/cartes/interfaces réseau    **(connaître par cœur)**
- `ipconfig` → Configuration IP (via cmd)    **(connaître par cœur)**
### 🧱 Registre & avancé

- `regedit` → Éditeur du registre    
- `sysdm.cpl` → Propriétés système

Voici une **liste ciblée “admin systèmes / cybersécurité”** de commandes utiles dans **Win + R → Exécuter** :
### 🔐 Sécurité / contrôle

- `secpol.msc` → Stratégie de sécurité locale    **(connaître par cœur)**
- `gpedit.msc` → Stratégie de groupe locale     **(connaître par cœur)**
- `tpm.msc` → TPM     
- `wf.msc` → Pare-feu Windows avancé    **(connaître par cœur)**
- `credwiz` → Sauvegarde des identifiants    
- `lusrmgr.msc` → Utilisateurs & groupes locaux (Pro)    
### 🌐 Réseau

- `ncpa.cpl` → Connexions/Cartes/interfaces réseau    **(connaître par cœur)**
- `firewall.cpl` → Pare-feu (basique)    
- `inetcpl.cpl` → Options Internet    
- `ipconfig` → Configuration IP (via cmd)    **(connaître par cœur)**
- `route print` → Table de routage (cmd)    
- `resmon` → trafic réseau + ressources    **(connaître par cœur)**
### 🧠 Diagnostic / logs

- `eventvwr.msc` → Journaux système (logs)    **(connaître par cœur)**
- `perfmon.msc` → Performances    
- `resmon` → Ressources système    
- `wercon` → Rapports d’erreurs    
### 💾 Système / stockage / matériel

- `diskmgmt.msc` → Gestion des disques & partitions   **(connaître par cœur)**    
- `devmgmt.msc` → Périphériques    **(connaître par cœur)**
- `sysdm.cpl` → Propriétés système    **(connaître par cœur)**
- `msinfo32` → Infos système complètes    **(connaître par cœur)**
### 🧑‍💻 Accès consoles

- `cmd` → Invite de commandes    **(connaître par cœur)**
- `powershell` → PowerShell    **(connaître par cœur)**
- `control` → Panneau de configuration

👉 C’est une **porte d’entrée rapide** vers les fonctions internes de Windows.