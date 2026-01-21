# :computer: **Challenge B303: Supervision réseau**

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
<img width="416" height="182" alt="image" src="https://github.com/user-attachments/assets/ba534ee6-8fd1-434d-a764-e47847f94f7b" />

## Étape 2 : Création d’un item « existence du fichier »

Dans Zabbix : `Data Collection → Hosts → la VM Win → Items → Create item``

<img width="408" height="251" alt="image" src="https://github.com/user-attachments/assets/4f1977bd-4d33-42d8-b3c3-ec5809d38d46" />

 **📖** Sélection de la clé à partir de la [**Ressources**](https://www.zabbix.com/documentation/current/en/manual/config/items/itemtypes/zabbix_agent) (Doc pour Agent 1, Passif).

Vérification de l’item sur `Monitoring → Latest data``

<img width="412" height="236" alt="image" src="https://github.com/user-attachments/assets/4c765eb1-efd0-4b0a-83b0-2671a4f281fc" />

## Étape 3 : Création d’un trigger (problème en cas d’absence)

Dans Zabbix : `Data Collection → Hosts → la VM Win → Triggers → Create trigger`

<img width="408" height="189" alt="image" src="https://github.com/user-attachments/assets/5e30aa87-2362-4034-89fb-7a4720cdc922" />

## Étape 4 : Test d’alerte

Aperçu du dashboard selon l’absence ou la présence du document surveillé :

<img width="410" height="266" alt="image" src="https://github.com/user-attachments/assets/4f53da9b-babd-4967-884a-fcb5a1e404e0" />

