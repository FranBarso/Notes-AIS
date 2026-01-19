# Tester connexion internet

## Regarder l’IPv4 et Passerelle

Invite de commandes (terminal ou command prompt) : **ipconfig/all**

On y peut même pinguer google.com
![[Pasted image 20251207182736.png]]
## Modifier IPv4

Exécuter : **ncpa.cpl** (pour aller dans Connexions réseau rentrer dans ses propriétés)
![[Pasted image 20251207183035.png]]
Rentrer dans les **propriétés** de l’IPv4 (sauf si l’on cherche juste à une IP par **DHCP**) pour pouvoir **modifier** l’IP, masque, passerelle et DNS.
![[Pasted image 20251207183117.png]]
Une fois validée, ce sera toujours bien de **désactiver** (puis **réactiver**) la carte Ethernet
![[Pasted image 20251207183203.png]]
Toujours vérifier avec un ping côté invite de commande (terminal)
## Modification du nom du WS

Système (même endroit que sur une machine Windows), puis tout en bas (Renommer ce PC)
![[Pasted image 20251207183245.png]]
Et on s’intéresse au bouton « **modifier** » sans besoin de mettre de description, puis faire attention de suivre la nomenclature des noms sur l’entreprise (dans ce cas nous mettons « WS2025 »)
![[Pasted image 20251207183356.png]]
**Attention**, on ne fait qu’une seule chose à la fois sur WS (dans ce cas renommer le serveur), puis il va redémarrer.

Win10 sur ProxMox : J’ai refait une Win10Client (VM 101), pour pouvoir la cloner après. Or, si l’on clone une VM il faudra toujours modifier l’IP pour éviter les conflits.
![[Pasted image 20251207183553.png]]
Celle de VM102
![[Pasted image 20251207183621.png]]

