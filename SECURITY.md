# Politique de sécurité

## Périmètre

Ce dépôt contient la documentation, les rapports et les scripts d’un audit
d’OWASP Juice Shop. Juice Shop est **volontairement vulnérable** : ses failles
connues (injections, défis JWT, etc.) ne sont pas à signaler ici. Elles sont
documentées dans [`docs/`](docs/).

Sont à signaler :

- un secret réel (clé, jeton, mot de passe) présent dans un fichier ou dans
  l’historique, y compris dans un rapport censé être expurgé ;
- une donnée personnelle publiée par erreur ;
- une faille dans les scripts de [`scripts/`](scripts/) ou dans les
  workflows de [`.github/workflows/`](.github/workflows/).

## Faux positif connu

[`scripts/keycheck.py`](scripts/keycheck.py) contient le motif
`-----BEGIN RSA PRIVATE KEY-----` dans une **expression régulière** : le script
cherche la clé de démonstration codée en dur dans le code de Juice Shop
(constat [F-002](docs/findings/F-002-cle-privee-jwt-codee-en-dur.md)) sans
contenir ni afficher aucune clé. Gitleaks 8.30.1 avec sa configuration par
défaut ne le signale pas ; un autre outil ou une autre configuration peut le
faire. Ce n’est pas un secret à signaler.

## Signaler une vulnérabilité

Ne pas ouvrir d’issue publique. Utiliser le signalement privé de GitHub :
onglet **Security** → **Report a vulnerability**.

Merci d’indiquer le fichier ou le commit concerné, et l’impact constaté.
Ne pas joindre la valeur complète d’un secret : son emplacement suffit.

Une première réponse est donnée sous 7 jours. Un secret confirmé est
d’abord **révoqué et remplacé**, puis retiré de l’historique si nécessaire.
