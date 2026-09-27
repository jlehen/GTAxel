# GTAxel

Un jeu d'action en 3D dans une ville, inspiré de **GTA** et **Wolfenstein** : tu es **B.J. Blazkowicz**. Tu voles des voitures, tu échappes à la police, tu achètes des armes, tu attaques le bunker nazi du Kommandant, puis tu affrontes le boss final, **Hitler**, dans le château Wolfenstein.

## Jouer

**En ligne : https://jlehen.github.io/GTAxel/**

Ou ouvre `index.html` dans un navigateur (double-clic). Il faut une connexion Internet : le moteur 3D ([Three.js](https://threejs.org)) est chargé en ligne.

| Touche | Action |
|---|---|
| Z Q S D ou flèches | Se déplacer / conduire |
| Souris | Regarder |
| Clic gauche | Tirer / frapper |
| Clic droit | Viser (zoom) |
| Maj | Courir |
| Espace | Sauter (frein à main en voiture) |
| Ctrl ou C | S'accroupir (on se fait moins toucher) |
| E | Monter / descendre de voiture, acheter à l'armurerie |
| V | Vue à la 1re / 3e personne |
| 1 à 7 ou molette | Changer d'arme |
| M | Carte de toute la ville (molette : zoom, souris ou flèches : se déplacer) |
| Entrée | Taper un code de triche |
| Échap | Pause |

Astuce : pour s'accroupir, préfère **C**. Certains navigateurs ferment l'onglet avec Ctrl+W.

## Le jeu

- **Armes** : on commence avec les poings et un couteau. Les autres s'achètent à l'**armurerie** (A orange sur la mini-carte) ou se ramassent sur les ennemis : pistolet, mitraillette, fusil à pompe, fusil d'assaut. Un tir à la tête fait beaucoup plus de dégâts. Hitler tire au **bazooka** et le lâche quand on le tue : ses roquettes explosent et font sauter les voitures.
- **Vie** : elle remonte toute seule si on n'est pas touché pendant 5 secondes. Les trousses de soin rendent 50 points. En voiture, on prend beaucoup moins de dégâts.
- **Gilet pare-balles** : il prend les dégâts à la place de ta vie (barre bleue). Il y en a un à l'armurerie, un dans le bunker et un dans le château.
- **Police** : faire des bêtises donne des étoiles (jusqu'à 5). À partir de 2 étoiles, la police arrive en voiture. Reste 12 secondes hors de sa vue pour perdre une étoile.
- **Voitures** : elles circulent en ville. Appuie sur E à côté d'une voiture pour éjecter le conducteur et la voler.
- **Missions** : suis le point jaune sur la mini-carte et la colonne lumineuse. La dernière mission t'envoie au château Wolfenstein (W rouge sur la mini-carte) pour éliminer Hitler.
- **Carte** : la touche M affiche toute la ville en plein écran et met le jeu en pause. On y voit où on est (flèche blanche), l'objectif (point jaune), l'armurerie, l'hôpital, le bunker et le château.
- **Codes de triche** : appuie sur Entrée, tape le code, puis Entrée. `SLIP`, `CHAUSSURE`, `SOUTIF`, `JAMBEDEBOIS`, `BARCA`, `BEBE`… à toi de voir ce qu'ils font ! Retape un code pour l'annuler.
- **WASTED** : si tu meurs, tu te réveilles à l'hôpital (+ rouge sur la mini-carte) et tu perds 100 $.

## Modifier le jeu

Tout est dans `index.html`, avec des zones faciles à changer en haut du fichier :

1. **`REGLAGES`** : vitesses, vie, dégâts des ennemis, nombre de voitures et de piétons… Si le jeu rame, mets `ombres: false`.
2. **`ARMES`** : dégâts, cadence de tir, prix, munitions de chaque arme, rayon d'explosion du bazooka.
3. **`CARTE`** : chaque lettre est un pâté de maisons, les routes sont ajoutées toutes seules. Toutes les lignes doivent avoir la même longueur.

   | Lettre | Pâté de maisons |
   |---|---|
   | `T` | Tours en verre |
   | `I` | Immeubles |
   | `M` | Maisons |
   | `P` | Parc |
   | `A` | Armurerie |
   | `H` | Hôpital |
   | `B` | Bunker nazi (soldats + Kommandant) |
   | `W` | Château Wolfenstein (soldats + Hitler, le boss final) |
   | `.` | Place |
   | `X` | Départ du joueur |
   | `a` `b` `c`… | Lieux de mission |

4. **`MISSIONS`** : invente tes missions avec ces étapes : `aller`, `voiture`, `eliminer` (`soldat`, `boss` ou `hitler`), `etoiles`, `semer`, `arme`.
5. **`TRICHES`** : renomme les codes ou invente les tiens.

Recharge la page (F5) pour voir tes changements. Le fonctionnement complet du jeu est décrit dans [DESIGN.md](DESIGN.md).
