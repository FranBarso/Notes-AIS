Challenge du 12/11/2025 (SA03E06)
# Challenge
Votre première mission ? **Réussir à vous connecter à l’interface de votre box !** Faites un petit tour des différents menu, notez les points qui vous questionnent / faites des captures d’écran si besoin !

️⚠️ C’est très important que vous réussissiez à vous connecter à votre box, sinon vous ne pourrez pas réaliser l’exercice pratique de demain.

Pour y accéder, rendez-vous sur [http://192.168.1.1](https://l.oclock.io/heimdall-fff57ce593f2abbebb468d32f24c5171) ou [http://192.168.1.254](https://l.oclock.io/heimdall-ba975669a5ed78369f94afd8f698fc88) (ou encore [http://192.168.0.254](https://l.oclock.io/heimdall-6b1e02a40b1fef44781619fee587f1ae) ou [http://192.168.0.1](https://l.oclock.io/heimdall-f34d0be0366a00234fbc09388eb64b6c)), et suivez les instructions pour votre première connexion (il faudra peut-être cliquer sur un bouton sur votre box, ou utiliser votre clé WiFi comme mot de passe, ça dépend des box) !

Facultatif (mais si vous ne le faites pas, vous ne pourrez pas aller jusqu’au bout de l’exercice de demain), en fonction de votre opérateur :
- si Orange, rendez-vous sur les paramètres réseaux, onglet « CGN », et cochez la case « ne pas partager mon IPv4 avec d’autres utilisateurs » ([source](https://l.oclock.io/aldebaran-technicien-support-it-74765c23921ba5436c3786a8e263658c))
- si SFR ou Bouygues, contactez le service client pour demander la désactivation du CG-NAT (demandez à ne plus avoir une IP « partagée », normalement le technicien devrait comprendre, sinon rappelez pour tomber sur un autre technicien ou demander à parler à un technicien de niveau 2)
- si Free, rendez-vous sur votre espace abonné, et cochez la case pour avoir une IP « fullstack »

Si vous avez fait l’étape ci-dessus, **redémarrez votre box ce soir** avant d’aller vous coucher ou demain matin avant d’allumer l’ordi !

En bonus, si vous n’êtes pas trop crevé et qu’il vous reste un peu de temps, je vous encourage à **pratiquer le DNS et le SSH dans Packet Tracer**.
# Challenge SA03E06 : Connexion Box

Je lance la requête à l’ip de mon routeur (192.168.1.1)
![[Pasted image 20251112212556.png]]
Pour que le mdp de toujours soit reconnu, j’ai dû remettre (le même sur mdp oublié) et accepter la manipulation sur la Box.

Dans Paramètres avancés, on rentre sur Réseau > DHCP et j’ai constaté qu’il n’y a pas d’onglet CGN
![[Pasted image 20251112212627.png]]
Je me suis rendu sur ma box : les paramètres disent que le Wi-Fi invité est désactivé :
![[Pasted image 20251112212539.png]]
Je constante sur la communauté orange qu’il n’y a pas de possibilité d’enlever le CGNAT depuis l’interface de la Livebox 6, pour les particuliers. Alors, j’ai dû appeler à plusieurs reprises le service client pour demander la désactivation.

Trois techniciens différents m’ont répété qu’il ne pas possible de le faire pour les comptes des particuliers et qu’ils sont navrés si je ne pourrai pas faire l’exercice pratique de demain à cause de cette impossibilité.
