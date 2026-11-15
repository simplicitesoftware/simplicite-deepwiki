# Copier le lien + webapp spécifique

**URL:** https://community.simplicite.io/t/13515

## Question
### Request description

Bonjour,

J'ai une configuration spécifique sur mon application. Celle-ci est déployée dans /simplicite et non pas /ROOT au niveau du tomcat.

L'url de mon application est donc https://app.seb.fr/simplicite/ui

Quand je copie le lien d'une occurence d'objet (action du socle "Copier le lien"), j ai bien une url du type :

> https://app.seb.fr/simplicite?f=[OBJET]%3B[ROWID]

qui me génère :

> https://app.seb.fr/simplicite/ui/?deeplink=%2Fsimplicite%2Fui%2Fobj%2Fform%2F[OBJET]%3Finst%3Dthe_ajax_[OBJET]%26nav%3Dnew%26row_id%3D[ROWID]%26action%3Dupdate

par contre je suis rediriger vers ma page d'acccueil

L'url suivante est fonctionnelle :

> https://app.seb.fr/simplicite/ui/?deeplink=%2Fui%2Fobj%2Fform%2F[OBJET]%3Finst%3Dthe_ajax_[OBJET]%26nav%3Dnew%26row_id%3D[ROWID]%26action%3Dupdate

J'ai le %2Fsimplicite en trop dans mon deeplink.

Y-a-t il un paramètre spécifique à mettre en oeuvre pour corriger ce point ?

Version :

Simplicité version 6.3.16
Built On 2026-09-09 19:41

## Answer
_No answer provided._
