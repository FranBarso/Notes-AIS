**Objectif :**
Mettre en place une alarme dans Zabbix qui doit se déclencher uniquement si le fichier test.txt n’existe pas sur les **machines Windows** surveillées.

**Consignes :**
Le fichier test.txt doit être recherché à la racine du disque C: (ou à un autre emplacement défini).

Tant que le fichier est présent, l’alarme ne doit pas se déclencher (pas d’erreur, pas de problème).

Si l’utilisateur supprime le fichier :
- Zabbix doit remonter une erreur indiquant que le fichier a été supprimé.
- L’alarme doit être visible afin de prévenir l’administrateur.

**Points attendus :**
- Création ou utilisation d’un item Zabbix permettant de vérifier l’existence du fichier.
- Mise en place d’un trigger qui s’active uniquement en cas d’absence du fichier.
- Vérification que l’alarme ne génère pas de faux positifs (elle reste silencieuse tant que test.txt existe).

Astuce : pensez à tester votre configuration en créant puis en supprimant le fichier pour vérifier que le comportement correspond bien à la consigne.
## Étape 1 : Création du fichier sur Windows C\ :
![Assets/Attachments/Pasted image 20260121205210.png]
## Étape 2 : Création d’un item « existence du fichier »

Dans Zabbix : `Data Collection → Hosts → la VM Win → Items → Create item``
![[Assets/Attachments/Pasted image 20260121205237.png|Pasted image 20260121205237.png]]
Sélection de la clé à partir de la ressource

**📖** **Ressources**
- Doc Agent 1 (Passif) : [https://www.zabbix.com/documentation/current/en/manual/config/items/itemtypes/zabbix_agent](https://l.oclock.io/aldebaran-technicien-infrastructure-b8350d164340a992e4e39322f84d428a)

Vérification de l’item sur `Monitoring → Latest data``
![[Assets/Attachments/Pasted image 20260121205321.png|Pasted image 20260121205321.png]]
## Étape 3 : Création d’un trigger (problème en cas d’absence)

Dans Zabbix : `Data Collection → Hosts → la VM Win → Triggers → Create trigger`
![[Assets/Attachments/Pasted image 20260121205356.png|Pasted image 20260121205356.png]]
## Étape 4 : Test d’alerte

Aperçu du dashboard selon l’absence ou la présence du document surveillé :

![[Assets/Attachments/Pasted image 20260121205159.png|Pasted image 20260121205159.png]]
