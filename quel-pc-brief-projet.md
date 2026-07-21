# Projet "Quel PC" — synthèse du brainstorm

*Document de travail, juillet 2026. Résume les décisions et les pistes de la discussion.*

---

## Le projet en une phrase

Un site web très simple qui aide une personne qui ne connaît rien à l'informatique à savoir quel ordinateur choisir, en traduisant ses besoins réels en un profil d'ordinateur clair, sans jamais lui imposer de jargon.

## Le besoin

Constat de départ, être régulièrement sollicité par des proches pour les aider à choisir leur matériel. Le besoin est réel et récurrent. Cas d'usage prioritaire retenu comme porte d'entrée, la rentrée de septembre 2026, avec des étudiants et des parents qui doivent changer d'ordinateur sans savoir quoi prendre.

## Positionnement

Le produit n'est pas un comparateur de plus. Sa valeur tient dans la couche de traduction, transformer un besoin exprimé en langage humain en une recommandation compréhensible.

Trois piliers.

1. Neutralité. On ne vend pas de matériel, on conseille. C'est ce qui nous différencie des revendeurs et des sites d'affiliation.
2. Profil plutôt que modèle imposé. On recommande un type d'ordinateur et quoi vérifier, pas un produit unique à acheter absolument. Le profil ne périme pas, une liste de modèles oui.
3. Confiance par la simplicité et le design. Pour ce public, la confiance ne vient pas des specs qu'il ne comprend pas, elle vient d'un parcours clair, d'un ton de conseil et d'un raisonnement transparent.

## Ce qui existe déjà

Le créneau est saturé en anglais. Choosist est presque exactement le même concept, déjà en ligne. Tout un écosystème de sites quiz anglophones vit de l'affiliation, avec une qualité inégale. Microsoft propose un quiz grand public correct mais limité à Windows, donc biaisé.

En français, c'est beaucoup plus vide. Ce qui existe est soit un guide éditorial non interactif comme Que Choisir, soit un questionnaire de revendeur donc orienté vers son propre stock, comme LDLC. Personne de vraiment neutre et bien conçu.

### Décision

Démarrer en français. C'est là que la concurrence est faible et que le conseil neutre et de qualité est un espace libre. L'anglais reste la vision d'export, une fois le moteur prouvé et différenciant, pas le point de départ.

## La réponse produit

Réponse principale, un profil d'ordinateur, durable et neutre.

En complément, deux ou trois machines validées à la main. Elles servent d'exemple concret pour rassurer et posent le rail de l'affiliation pour plus tard. Elles doivent former une couche à part, clairement datée, du genre "nos machines du moment". Si un modèle disparaît, le conseil de fond tient toujours.

Monétisation prévue plus tard par l'affiliation, une fois les premiers utilisateurs présents, sans jamais biaiser le classement.

## Les supports

Priorité une, un site web pensé mobile d'abord. C'est le seul support qui capte les deux canaux d'acquisition réels, le lien partagé qu'on envoie par SMS ou WhatsApp, et la recherche Google en août. Un lien qu'on ouvre sans rien installer est la fonction la plus importante, même si elle a l'air de rien.

Pas d'application. On n'installe pas une app pour un achat fait une fois tous les trois ou quatre ans, et l'installation est une barrière pour un public non technique. On peut avoir la sensation d'app avec un site mobile fluide, une question à la fois, plein écran.

Extension navigateur, en phase deux seulement. Pensée comme validateur et non comme dénicheur. Elle vérifie un choix que la personne a fait seule et dit si ça correspond au profil recommandé. C'est un outil de confiance, pas de vente. Elle doit rester humble, parler de niveau de correspondance plutôt que d'un oui ou non tranché, et dire clairement quand elle n'a pas réussi à identifier un modèle plutôt que de deviner. Un faux verdict détruit la confiance construite.

## Les comptes

Sans compte par défaut, pour ne pas freiner l'usage.

Compte optionnel, avec plusieurs rôles utiles. Garder en mémoire le profil recommandé. Ouvrir la porte de l'extension. Servir de canal de lien dans le temps, donc de canal de monétisation propre le jour venu, y compris pour prévenir qu'un profil recommandé a évolué.

## Le pivot technique clé

Plutôt que de lire les caractéristiques dans le texte d'une page produit, ce qui est fragile, on se base sur l'identifiant du produit. L'extension n'a plus qu'un seul travail, repérer la référence sur la page. La comparaison au profil est faite par un moteur central, le même pour l'extension, pour la photo en magasin et pour une saisie manuelle. Trois fonctions, un seul moteur.

La granularité de l'identifiant est le point de vigilance. Un simple nom de modèle ne suffit pas, car il existe en plusieurs configurations. Ce qui fixe la config exacte est le numéro de pièce fabricant complet ou le code EAN. Formulation prudente à conserver, "d'après la référence, ce modèle a normalement tel processeur", car une référence peut avoir des variantes régionales.

Source de données envisagée, Icecat. C'est un catalogue ouvert de fiches produit, avec inscription de base gratuite, interrogeable par code EAN ou UPC et par numéro de pièce fabricant, disponible en XML ou JSON, avec une très large couverture européenne. La base de traduction référence vers specs se branche plutôt qu'elle ne se construit.

Pour l'achat en magasin physique, même moteur. On oriente vers le scan du code-barre de la boîte, qui porte l'EAN, plutôt que la recopie du nom de modèle. Une fiche mémo du profil, sauvegardée sur le téléphone, sert partout, en ligne comme en rayon devant un vendeur, et couvre le magasin physique que l'extension ignore.

## Le formulaire, cœur du MVP

Principe central, ne jamais demander à la personne d'évaluer son besoin technique. Elle ne peut pas répondre à "as-tu besoin de puissance". On demande ce qu'elle fait, un comportement qu'elle connaît, et le moteur en déduit les specs qu'elle ne connaît pas.

Six questions, une par écran, moins de cinq minutes.

1. Usage principal, une ou deux réponses. Fixe la bande de puissance de base et le besoin ou non d'une carte graphique.
2. Façon de travailler, une chose à la fois ou beaucoup de fenêtres ouvertes ou gros logiciels. Calibrage fin qui module la mémoire vers le haut ou le bas. C'est ce qui rattrape le cas de la personne qui a toujours quinze onglets ouverts sans croire celle qui surestime son besoin.
3. Mobilité, fixe ou transporté. Fixe la taille d'écran et le poids.
4. Prise électrique, seulement si la personne est mobile. Décide de la priorité batterie.
5. Habitude d'OS, sans jargon, Windows ou univers Apple ou aucune idée.
6. Budget, l'ancre de réalité.

Logique du moteur. L'usage fixe une bande. La façon de travailler la décale d'un cran. Le budget plafonne, et en cas de conflit on ne ment pas, on affiche l'arbitrage honnêtement.

Sortie. Un profil en langage clair, le raisonnement lié aux réponses, ce qu'il faut vérifier avant d'acheter, et l'emplacement daté pour la sélection maison.

## La maquette

Une maquette cliquable a été produite, mobile d'abord, en français. Elle montre le parcours des six questions avec branchement conditionnel, le calibrage mémoire visible selon la façon de travailler, l'arbitrage budget honnête, et la fiche profil de sortie. Identité visuelle, fond neutre chaud, vert comme fil conducteur qui est aussi la couleur du "ça correspond" de la future extension, titres en Bricolage Grotesque, texte en Inter pour la lisibilité.

Le moteur y est volontairement simple et les libellés de specs restent à affiner.

## Feuille de route

MVP rentrée septembre 2026, la seule chose qui doit sortir à temps.
Site mobile, questionnaire, profil de sortie, deux ou trois suggestions maison. Sans compte.

Après le lancement, par ordre logique.
Compte optionnel et persistance du profil. Fiche mémo pour le magasin. Moteur d'identification par référence branché sur Icecat. Photo ou scan en magasin. Extension validateur. Affiliation. Puis export en anglais.

## Points de vigilance

La fraîcheur des données est ce qui tue ce type de projet. Le choix du profil plutôt que du modèle la neutralise en grande partie.

La confiance est tout le fonds de commerce. Tout ce qui la fragilise, faux verdict d'extension, sensation d'être vendu, doit être écarté.

La granularité de l'identifiant conditionne la fiabilité du moteur d'identification.

L'extension et la photo sont du post-lancement. Elles ne peuvent pas sortir pour la rentrée, donc elles ne doivent pas distraire du MVP.

## Prochaines étapes possibles

Durcir la logique du moteur, par exemple le stockage selon les usages ou le cas Mac.
Retravailler une question qui semble bancale.
Lister ce qu'il faut pour passer de la maquette à un vrai site en ligne.
