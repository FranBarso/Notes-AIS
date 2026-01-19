SA03E09 (17/11/2025)
Encore une journée très chargée

Si vous avez encore un peu d’énergie, ce serait pas mal de **pratiquer un peu les VLANs et le routage inter-vlan** ! Si vous êtes trop crevé, gardez ça pour plus tard et relisez tranquillement les slides du jour, ou revenez sur l’atelier/les challenges précédents.

**Pratique VLANs & routage inter-VLANs :**

- Placez 3 switches 2960 et connectez sur ces switches plusieurs PC/portables/serveurs
- Créez 3 VLANs sur tous les switchs :
    - VLAN 10 : LAN1
    - VLAN 20 : LAN2
    - VLAN 30 : LAN3
- Attribuez environ 1/3 des ports de chaque switch à chaque VLAN
- Répartissez les machines dans ces différents VLANs
- Attribuez une adresse IP à vos machines en fonction de leur VLAN :
    - LAN1 : `192.168.1.0/24`
    - LAN2 : `172.16.0.0/16`
    - LAN3 : `10.0.0.0/16`
- Configurez les liens Trunk entre les switch
- Vérifiez : À ce stade les machines d’un même VLAN doivent pouvoir communiquer, mais pas possible de communiquer entre les VLANs.

**Aller un peu plus loin : sécurité & VLANs**

- Changez le VLAN de Management : utilisez le VLAN 50 pour l’administration à distance des switchs
- Configurez une IP sur le VLAN 50 de chaque switch et activez Telnet et/ou SSH (pour tester)
- Limitez les VLANs autorisés sur les liens Trunk
- Changez le VLAN natif des liens Trunk

**Routage inter-VLAN :**

- Ajoutez un switch de niveau 3
- Configurez les différents VLANs et le lien trunk
- Attribuez une IP (passerelle) sur chaque interface VLAN (10, 20 et 30)
- Configurez cette adresse comme passerelle sur vos machines (en fonction de leur VLAN)
- Activez le routage
- Vérifiez : le ping doit passer entre toutes les machines !

**Bonus : ACLs**

- En suivant le début de [cette doc](https://l.oclock.io/aldebaran-technicien-support-it-09d11f0aca5b2d71854e0a658534a283) (partie ACLs standards) essayez de restreindre la communication entre les VLANs : autorisez seulement certaines machines à communiquer entre-elles (par exemple : autoriser les machines du VLAN 20 et 30 à seulement joindre un serveur spécifique dans le VLAN 10).