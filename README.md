# GTAxel

Un jeu de tir à la première personne dans une ville, entre **Wolfenstein 3D** et **GTA** : on vole des voitures, on échappe à la police et on attaque le bunker du Kommandant.

## Jouer

**En ligne : https://jlehen.github.io/GTAxel/**

Ou ouvre `index.html` dans un navigateur (double-clic). Rien à installer.

| Touche | Action |
|---|---|
| Z Q S D ou flèches | Se déplacer / conduire |
| Souris | Viser |
| Clic ou Espace | Tirer |
| E | Monter / descendre de voiture |
| Échap | Pause |

## Le jeu

- **Missions** : suis la flèche jaune et le point clignotant sur la mini-carte.
- **Police** : faire des bêtises donne des étoiles (jusqu'à 5). Plus il y en a, plus les policiers sont nombreux. Reste 12 secondes hors de leur vue pour perdre une étoile.
- **Voitures** : des voitures circulent en ville. Appuie sur E à côté d'une voiture pour éjecter le conducteur et la voler.
- **Police en voiture** : à partir de 2 étoiles, des voitures de police arrivent toutes sirènes hurlantes et les policiers en descendent. Tu peux aussi voler leur voiture !
- **Bunker** : gardé par des soldats. Les ennemis mis K.O. laissent des munitions.
- **Trousses de soin** : +30 de vie.

## Modifier le jeu

Tout est dans `index.html`, avec trois zones faciles à changer en haut du fichier :

1. **`REGLAGES`** : vitesses, vie, balles, dégâts, titre du jeu…
2. **`CARTE`** : la ville est dessinée avec des lettres. Toutes les lignes doivent avoir la même longueur.

   | Lettre | Signification |
   |---|---|
   | `1` `2` `3` `4` `5` `B` | Murs : béton, briques, verre, immeuble, magasin, bunker |
   | `.` `,` `_` | Sols : route, herbe, sol du bunker |
   | `X` | Départ du joueur |
   | `S` `K` `F` `P` | Soldat, Kommandant, policier, piéton |
   | `C` `H` `M` `T` | Voiture, soin, munitions, arbre |
   | `a` `b` `c`… | Lieux de mission |

3. **`MISSIONS`** : invente tes missions avec ces étapes : `aller`, `voiture`, `eliminer`, `etoiles`, `semer`.

Recharge la page (F5) pour voir tes changements.
