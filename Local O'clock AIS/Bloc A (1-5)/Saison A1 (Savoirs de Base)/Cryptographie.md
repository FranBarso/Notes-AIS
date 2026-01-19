Cours du 15/10/2025
# Antivirus / Antimalware
On parle de sécurité, ce serait dommage de ne pas parler des logiciels antivirus !

Des logiciels dont objective c’est de contenir et éliminer les virus.

**À** **retenir** : Deux grands modes de fonctionnement :

·        analyse de la signature (hash) des fichiers

·        analyse du comportement des programmes (méthode heuristique)

[Logiciel antivirus — Wikipédia](https://fr.wikipedia.org/wiki/Logiciel_antivirus)
## Types de malwares
**Attention**: La liste est non-exhaustive, et certains malwares peuvent être dans plusieurs « catégories ».

- **Ransomware** : chiffre les données, exige une rançon (souvent en bitcoins) pour obtenir la clé de déchiffrement.
- **Spyware** : espionne l’activité de l’utilisateur, permet de voler des données ou des comptes.
- **Adware** : virus publicitaire, sert à générer de l’argent via des clics sur les pubs affichées.
- **Cheval de Troie** : code malicieux embarqué dans une application qui semble légitime.
- **Ver** : virus capable de s’auto-répliquer, de contaminer d’autres machines via le réseau (ou d’autres moyens).
- **Rootkit** : malware furtif, conçu pour ne pas pouvoir être détecté, ou un tout cas très difficilement.
- **Keylogger** : type de spyware, qui enregistre toutes les frappes au clavier. Peut aussi être matériel ! Avec un gestionnaire, on fait copier/coller, donc il ne le suit pas.
- **Coinminer** : malware qui mine du bitcoin (ou autres crypto-monnaies) à l’insu de l’utilisateur.
- **Botnet** : réseau de machines « zombies », contaminées par un malware, permettant de faire par exemple des attaques DDoS.
# Cryptographie
## **Chiffrement** (bidirectionnel) **vs. Hachage** (unidirectionnel)
Deux techniques différentes avec des buts différents… Si le Hachage est hacké, on doit l’oublier car il ne sert plus à rien

**Attention**: Chercher plus d’info

**On dit Chiffrer, et pas crypter :** même concept mais crypter veut dire que tu chiffres sans la clé, donc impossible à ce que ce soit propre. Rien n’est crypté, tout est chiffré.
## Chiffrement symétrique :
![[Pasted image 20251112182114.png]]
Quand il y a une clé pour que le message soit chiffré et non-surveillé par « the man in the middle ». Même clé pour chiffrer et déchiffrer le message. Super rapide à mettre en place. Le WhatsApp avec mamie, symétrique suffit.
## Chiffrement asymétrique :
![[Pasted image 20251112182241.png]]
Avec deux clés (une pour ouvrir et une autre pour fermer). Une clé publique pour chiffrer le message et une autre clé personnelle pour déchiffrer. Tu génères toi-même les clés. En termes de confidentialité c’est parfait. Le « man in the middle » ne peut pas lire, seul le détenteur de la clé privée peut lire le message. Bien utilisé sur la dark web : une personne (A) envoie un message avec la clé publique de quelqu’un en pariculier (B), B est le seul à pouvoir voir le message. Au même temps, si A a communiqué en utilisant directement la clé publique de B, alors B pourra lire le message mais ne saura jamais l’identité de A. Les autres savent qu’il y a une conversation, mais ils ne peuvent pas voir le contenu. Il ne faut jamais donner sa clé privée à personne, il faut bien choisir la bonne clé privée. Si jamais on perd la clé privée (l’ordi se casse et on n’a pas sur-gardé ailleurs, comme dans un gestionnaire de mdp), on doit faire une nouvelle paire de clé. C’est important de renouveler les clés et de ne pas utiliser les mêmes pour chaque site. C’est plus long est plus compliqué à mettre en place que le chiffrement symétrique. La com de la NSA, asymétrique obligatoire. C’est in-faible si bien fait. Par contre, c’est surtout plus lent.
## Chiffrement hybride :
![[Pasted image 20251112182344.png]]
A génère la paire de clés et partage la clé publique avec B > B génère une clé symétrique, reçoit la clé publique de A et partage sa clé symétrique (sécurisé par clé publique) avec A > B reçoit avec sa clé privée et communique sécurisé par la clé symétrique créée par B. Uniquement le premier échange va être plus long, puis la communication avec clé symétrique sera beaucoup plus rapide.

Exemple :
![[Pasted image 20251112182434.png]]

