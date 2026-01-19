## Introduction à LDAP

Surement le rôle phare et plus connu et plus utilisé de WS

Lightweight Directory Access Protocol (**LDAP**) est un protocole standard pour interroger et modifier des annuaires. Il fournit une manière structurée d’accéder à des informations d’identités, de ressources et de politiques.

Les annuaires sont optimisés pour la lecture. Ils stockent des entrées hiérarchisées, indexées, et faciles à parcourir pour des opérations fréquentes comme l’authentification.

LDAP repose sur un modèle de données simple : des entrées avec des attributs.

Chaque entrée est identifiée par un Distinguished Name. Les opérations centrales sont Bind, Search, Add, Modify et Delete.

## LDAP sur Windows Server

Active Directory implémente LDAP comme interface d’annuaire.

ADDS expose un schéma LDAP et répond aux requêtes via le port 389/636, tout en intégrant Kerberos, NTLM et les GPO (on reparlera de ces derniers plustard).

Dans Windows, LDAP n’est pas l’authentification mais la porte d’entrée vers les objets. L’authentification s’appuie principalement sur Kerberos.

## Historique de LDAP

Le protocole LDAP a été développé dans les années 1990 pour simplifier l'accès aux annuaires électroniques. Depuis ses débuts, il a considérablement évolué pour devenir un standard incontournable dans la gestion des identités et des accès dans les organisations.

LDAP est largement utilisé dans de nombreux domaines, tels que les entreprises, les établissements d'enseignement et les services gouvernementaux. Il offre une méthode efficace de centralisation des informations utilisateur et de gestion des autorisations, ce qui facilite la collaboration et l'accès aux ressources.

De plus, LDAP est évolutif et peut s'intégrer à d'autres protocoles pour offrir une solution complète de gestion des identités et des accès.

## Configuration de LDAP

Une configuration LDAP typique implique plusieurs étapes clés :

### Création des objets

Active Directory permet de créer des objets LDAP, comme les utilisateurs, les groupes et les ordinateurs. La création d'objets LDAP suit une hiérarchie, où les objets sont organisés dans des unités d'organisation (OU) et des domaines.

### Définition des attributs

Chaque objet LDAP possède des attributs, qui sont des caractéristiques qui le définissent. Les attributs peuvent être des informations telles que le nom d'utilisateur, le mot de passe, l'adresse e-mail ou les groupes auxquels l'utilisateur appartient.

### Configuration des politiques

Active Directory offre des politiques LDAP qui définissent les règles et les restrictions relatives aux objets. Ces politiques peuvent être appliquées à des groupes spécifiques d'utilisateurs ou d'ordinateurs.

### Schéma LDAP

Le schéma décrit les classes d’objets et attributs.

Dans AD, il est extensible : on peut ajouter des attributs ou classes personnalisées tout en respectant des OID (Object Identifier) uniques.
![[Pasted image 20251207183933.png]]
### Contrôle d’accès LDAP

Les ACL (Access Control Lists) définissent qui lit, écrit ou supprime.

AD utilise un modèle basé sur les Security Descriptors avec héritage granulaire.

L’authentification est distincte de l’autorisation. Kerberos fournit des tickets ; les ACL tranchent l’accès aux objets et attributs.️

Les Attributs LDAP : [Associer les champs Active Directory et les attributs LDAP](https://www.it-connect.fr/correspondance-entre-les-champs-active-directory-et-les-attributs-ldap/)

### Applications de LDAP

LDAP sert à la centralisation des identités, à l’adresse e-mail, aux applications web, VPN, NAS et bien d’autres intégrations.

Avec ADDS, les applis peuvent s’appuyer sur LDAP pour chercher des comptes, vérifier des groupes, ou récupérer des attributs de profil.

### Création d’un domaine Active Directory

La création commence par l’ajout du rôle ADDS, la promotion en contrôleur de domaine, et la définition du nom DNS du domaine.

On choisit le niveau fonctionnel, on installe DNS si nécessaire, et on prépare les sites et sous-réseaux pour une réplication efficace.

Un role ? C'est quoi ça ?

### Roles de Windows Server

Les rôles de Windows Server sont des fonctionnalités spécifiques qui peuvent être installées pour répondre à des besoins particuliers. Chaque rôle a des responsabilités et des services associés.

Par exemple, le rôle ADDS permet de gérer les identités et les accès dans un environnement Windows, tandis que le rôle DNS gère la résolution des noms de domaine.

Ou encore le role DHCP qui attribue automatiquement des adresses IP aux appareils sur le réseau.

### Le Role : ADDS

Une fois le rôle ADDS installé, nous devons promouvoir le serveur en contrôleur de domaine (DC). Cela implique la création d'un nouveau domaine ou l'ajout à un domaine existant.

Le premier Domaine Contrôleur (DC) crée la base du domaine, la partition de configuration et le catalogue global si sélectionné. Les DC suivants rejoignent et répliquent. On défini également la Forêt.

### C’est quoi une Forêt ?

La forêt est la limite de confiance et de schéma. Elle regroupe un ou plusieurs domaines partageant un catalogue global, une configuration commune, et un schéma unique.

Les forêts permettent l’isolation logique : administration, politiques et identités restent contrôlées dans des frontières claires.

### Forêt, Tree et Domain ️

Un tree regroupe des domaines dans un espace de noms. Un domaine est une unité d’administration, de sécurité et de réplication.

Les trusts automatiques existent entre domaines d’une même forêt. Les trusts externes permettent l’interopérabilité entre forêts.
![[Pasted image 20251207184007.png]]
Attend, j'ai un arbre qui a le même nom que la Forêt... Ce n’est pas un peu confus ?

Oui, ça peut l’être ! Dans cet exemple, “oclock” est le nom de la forêt, tandis que “oclock.lan” est le nom DNS du domaine racine dans cette forêt. L’arbre est simplement la structure logique qui regroupe les domaines partageant ce même espace de noms.

Donc, même si les noms se ressemblent, ils ne désignent pas la même chose :

la forêt = l’ensemble, le domaine racine = le point de départ de l’arbre, et l’arbre = tout ce qui partage le même espace DNS.

Souvent, on choisit des noms proches pour simplifier la gestion, mais attention : côté réseau et compatibilité, Active Directory ne s’appuie pas uniquement sur le DNS...

### C’est quoi NetBIOS !

Avant que le DNS ne soit généralisé, Windows utilisait NetBIOS pour identifier les ordinateurs et les domaines sur le réseau local.

Chaque domaine Active Directory garde donc aussi un nom NetBIOS court, souvent dérivé de son nom DNS, mais limité à 15 caractères (et sans “.”).
![[Pasted image 20251207184101.png]]
![[Pasted image 20251207184120.png]]
Le nom NetBIOS est crucial pour la compatibilité avec les anciens systèmes et applications qui ne supportent pas le DNS. Comme par exemple, les partages réseau via SMB utilisent souvent le nom NetBIOS pour localiser les ressources (mais ça on reviendra plus tard dessus...)

_Maintenant qu’on comprend mieux comment un domaine est identifié à la fois par son nom DNS et par son nom NetBIOS on peut se demander :_

**“Mais où sont stockés concrètement les éléments qui font fonctionner ce domaine ?”**

Réponse : dans le **Sysvol**.

Le **SYSVOL** (pour **System Volume**) est un dossier partagé automatiquement présent sur chaque contrôleur de domaine (DC). Il contient tous les fichiers nécessaires à la réplication et à la cohérence des stratégies dans le domaine.

Dedans, on retrouve notamment :

- Les scripts d’ouverture de session (logon scripts),
- Les GPO (Group Policy Objects) appliquées aux utilisateurs et ordinateurs,
- Et les fichiers publics nécessaires à la configuration du domaine.

Il peut être répliqué par DFS-R dans les environnements récents.
## Conclusion

Du LDAP au SYSVOL
![[Pasted image 20251207184207.png]]
### En résumé :
- **LDAP** fournit la logique et la structure.
- **ADDS** met tout cela en œuvre dans Windows.
- **Forêt**/ **Arbre** / **Domaine** / **Site** structurent l’organisation.
- **DNS** et **NetBIOS** identifient les domaines et hôtes.
- **SYSVOL** assure la cohérence et la réplication des politiques.

- **Les Fondations : LDAP** :
    
    - **LDAP (Lightweight Directory Access Protocol)** est le protocole standard utilisé pour interroger et modifier les annuaires. Il structure les données de manière hiérarchique (comme un arbre) pour faciliter la recherche.
    - Active Directory est l'implémentation Microsoft de LDAP. Il utilise ce protocole pour communiquer, tout en intégrant la sécurité Kerberos.
- **Architecture Logique** :
    
    - **Domaine** : C'est l'unité de base d'administration et de sécurité. Il regroupe des objets (utilisateurs, ordinateurs) partageant une base de données commune.
    - **Arbre (Tree)** : Regroupement de un ou plusieurs domaines partageant un espace de noms DNS contigu (ex: `thm.local` et `us.thm.local`).
    - **Forêt (Forest)** : Le conteneur de plus haut niveau. Elle regroupe un ou plusieurs arbres qui partagent le même **schéma** (définition des objets) et la même configuration. C'est la frontière de sécurité ultime.
    - **OU (Unité Organisationnelle)** : Conteneurs à l'intérieur d'un domaine permettant d'organiser les objets (par département, lieu...) et surtout d'appliquer des **GPO** (Stratégies de groupe) ou de déléguer des droits d'administration.
- **Architecture Physique** :
    
    - **Site** : Représente la topologie physique du réseau (un ou plusieurs sous-réseaux IP). Les sites servent à optimiser la **réplication** (synchronisation) entre les contrôleurs de domaine et à permettre aux utilisateurs de s'authentifier sur le serveur le plus proche.
    - **Contrôleur de Domaine (DC)** : Serveur qui héberge la base de données AD (`NTDS.dit`) et le dossier SYSVOL.
- **Gestion des Objets** :
    
    - **Utilisateurs et Ordinateurs** : Comptes utilisés pour l'authentification sur le réseau.
    - **Groupes** : Permettent de gérer les permissions efficacement (on donne des droits à un groupe, pas à un utilisateur seul).
        - **Types** : Sécurité (pour les permissions d'accès) ou Distribution (pour les e-mails).
        - **Portées** : Domaine Local, Global, Universel (définissent la visibilité du groupe dans la forêt).
- **Le SYSVOL** :
    
    - C'est un dossier partagé présent sur chaque Contrôleur de Domaine. Il contient les éléments publics nécessaires aux clients, comme les **scripts de connexion** et les fichiers des **GPO** (Stratégies de groupe). Il est automatiquement répliqué sur tous les DC.

Active Directory, c’est l’union de ces briques !
