# Sur WS 2025
Soit sur le Tableau de bord 
![[Pasted image 20251207185427.png]]
ou soit sur **Gérer** > **Ajouter des rôles et fonctionnalités**
![[Pasted image 20251207185546.png]]
Pour l’installation de n’importe quel rôle et fonctionnalité, on aura toujours cette Information par défaut :
![[Pasted image 20251207185822.png]]
On choisit les serveurs, selon liste (dans ce cas nous en avons uniquement un):
![[Pasted image 20251207185908.png]]
On choisit les rôles souhaités, dans ce cas uniquement le AD DS (plus complète que les autres AD DS). Dès que l’on le choisit, il ouvre une information des requis que nous pourrons accepter
![[Pasted image 20251207185958.png]]
**Bon à savoir** que le rôle « **DNS** » sera installé automatiquement après, grâce au rôle AD DS (il va nous obliger à le faire).
![[Pasted image 20251207190059.png]]
**Pour info** : on peut même l’installer en ligne de commande avec la commande « **dc promo** »

Pour l’installer sur l’interphase graphique, pour la première fois (sans domaine existant), il faudra choisir « Ajouter une nouvelle forêt » et nous introduisons le nom de notre domaine (dans notre cas, Oclock.lan). **Attention** : Ne jamais utiliser des extensions conflictuels car déjà rependus par défaut (.com, .net, .io, etc).
![[Pasted image 20251207190332.png]]
Pour le niveau fonctionnel, nous devons choisir le plus haut/proche de la version qu’on a installée de WS. Puis le mdp doit être fort (mais pour cette pratique nous avons **rocknroll25 !**)
![[Pasted image 20251207190411.png]]
Finalement, il va redémarrer et nous verrons apparaître les nouveaux rôles sur le Tableau de bord :
![[Pasted image 20251207190445.png]]
Notre outil plus important sera « **Utilisateurs et ordinateurs Active Directory** », qui nous permettra de voir non seulement les utilisateurs et ordinateurs, mais aussi les groupes d’utilisateurs de notre AD.
![[Pasted image 20251207190533.png]]
Cette fois-ci, nous nous concentrerons sur le domaine que nous venons de créer (« oclock.lan »)
![[Pasted image 20251207190655.png]]
Si l’on ouvre le domaine, on pourra voir l’**arborescence** de l’annuaire (AD) avec les **OU** qui ont été automatiquement crées lors de la promotion du serveur comme contrôleur de domaine.
![[Pasted image 20251207190728.png]]
Dans le dossier **Builtin**, on trouve des groupes d’utilisateurs par **défaut** dans un WS, et qui vont servir à différentes fonctionnalités (genre Hyper-V). Si jamais on a besoin d’en savoir plus, ils ont tous une description côté droit.
![[Pasted image 20251207190854.png]]
Dans le dossier **computers**, on trouvera les ordinateurs qu’on rajoutera.
![[Pasted image 20251207190937.png]]
Dans le dossier **Domain Controllers**, on aura tous nos ordinateurs qui fonctionnent en tant que contrôleur de domaine (ou serveur), comme celui que nous avons créé au tout début (WS2025)
![[Pasted image 20251207191015.png]]
Dans le dossier **Users**, on trouve tous les utilisateurs par défaut dans un AD d’un WS. Nous avons uniquement un utilisateur créé par nous lors de l’installation (celui de l’**Administrateur**)
![[Pasted image 20251207191051.png]]
## Création d’une nouvelle UO (dossier pour des utilisateurs)

**Méthode 1** : Il faudra se positionner sur le domaine et choisir l’icône de « créer une nouvelle UO dans le conteneur actuel »
![[Pasted image 20251207191138.png]]
**Méthode 2** : sélectionner le domaine > Nouveau > UO
![[Pasted image 20251207191202.png]]
Attention de suivre la **nomenclature** de noms dans l’entreprise. C’est aussi bon de laisser actif l’option de « protection », car il pourra tout de même être supprimé d’une autre façon en cas de besoin
![[Pasted image 20251207191241.png]]
## Création un nouvel utilisateur

**Méthode 1** : Il faudra se positionner sur l’UO et choisir l’icône de « créer un nouvel utilisateur dans le conteneur actuel »
![[Pasted image 20251207191312.png]]
**Méthode 2** : sélectionner l’UO > Nouveau > Utilisateur

![[Pasted image 20251207191418.png]]
Pareil, faire attention de suivre la **nomenclature** de noms dans l’entreprise et des sessions (genre « prénom.nom@domaine ).

En entreprise, il faut absolument laisser cochée la casse « Utilisateur doit changer le mdp à la prochaine ouverture de session »
![[Pasted image 20251207191455.png]]
**Attention** : OASP (WASP ?) recommande de ne jamais activer la rotation des mdp (genre tous les 3 mois) car cela risque de faire que l’utilisateur mette toujours le même mdp (avec des modifications minimes), ce qui est encore pire en termes de sécurité que de ne jamais demander l’utilisateur de changer son mdp, même si cela partait d’une bonne idée.
# Relier la VM au Serveur (WS)

Si l’on pingue le domaine depuis la VM, on verra qu’il n’y a pas de communication si l’on n’a pas modifié les paramètres réseau
![[Pasted image 20251207191826.png]]
Alors, il nous faudra aller sur la carte **Ethernet** (Rappel : **ncpa.cpl** sur Exécuter)
![[Pasted image 20251207191859.png]]
On laisse bien l’IP de la VM en DHCP, mais au niveau DNS il faudra mettre l’IP du WS.
![[Pasted image 20251207191937.png]]
Même si ce n’est pas la dernière manip à faire, maintenant le ping passera depuis la VM au domaine du WS
![[Pasted image 20251207192007.png]]
Il faudra **renommer** notre **VM** : Système > Renommer ce PC (avancé) > Modifier

Attention : à ce stade, impossible de rejoindre le domaine sans faire beuguer le processus (une chose à la fois)
![[Pasted image 20251207192037.png]]
## Rejoindre le domaine

Avec même procédure que pour renommer, mais cette fois-ci on peut rejoindre le domaine (on verra qu’il avait déjà changé le nom de l’ordinateur après le redémarrage :
![[Pasted image 20251207192106.png]]
**Attention** : dès fois il faut redémarrer une deuxième fois pour qu’il arrive à demander le mdp de l’administrateur créé avec le domaine (**rocknroll25!** ):
![[Pasted image 20251207192141.png]]
Cela redémarrera la VM encore une fois, et on pourra se connecter avec un autre utilisateur, cette fois-ci dans le domaine :
![[Pasted image 20251207192228.png]]
Pour les utilisateurs lambda, j’ai utilisé le mdp **Rocknroll25!** ou **rocknroll25!** 

**Attention** : la première connexion de l’utilisateur prend du temps pour le démarrage. Ils peuvent tous se connecter.
![[Pasted image 20251207192301.png]]
A ce stade, si j’actualise mon AD (côté WS), je pourrai voir les deux **ordinateurs liés** dans le fichier « Computers » :
![[Pasted image 20251207192335.png]]

