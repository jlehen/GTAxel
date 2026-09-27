# GTAxel

Un jeu d'action en 3D dans un grand pays inspiré de celui de **GTA 5**, mélangé à **Wolfenstein** : tu es **B.J. Blazkowicz**. Tu parcours Los Santos, les collines, le désert et les montagnes, tu voles des voitures et des bateaux, tu échappes à la police, tu achètes des armes, tu attaques le bunker nazi du Kommandant à Fort Zancudo, puis tu affrontes le boss final, **Hitler**, dans le château Wolfenstein, sur le mont Chiliad.

## Jouer

**En ligne : https://jlehen.github.io/GTAxel/**

Ou ouvre `index.html` dans un navigateur (double-clic). Il faut une connexion Internet : le moteur 3D ([Three.js](https://threejs.org)) est chargé en ligne.

| Touche | Action |
|---|---|
| Z Q S D ou flèches | Se déplacer / conduire |
| Q S D, 3 fois de suite | Danser comme Michael Jackson |
| Souris | Regarder |
| Clic gauche | Tirer / frapper |
| Clic droit | Viser (zoom, lunette avec le fusil de sniper) |
| Maj | Courir |
| Espace | Sauter (frein à main en voiture) |
| Ctrl ou C | S'accroupir (on se fait moins toucher) |
| E | Monter / descendre (voiture, bateau), acheter à l'armurerie, prendre l'ascenseur |
| V | Vue à la 1re / 3e personne |
| 1 à 8 ou molette | Changer d'arme |
| M | Carte de tout le pays (molette : zoom, souris ou flèches : se déplacer) |
| Entrée | Taper un code de triche |
| Échap | Pause |

Astuce : pour s'accroupir, préfère **C**. Certains navigateurs ferment l'onglet avec Ctrl+W.

## Le jeu

- **Le pays** : Los Santos au sud (Vinewood, le centre et ses gratte-ciel, la plage de Vespucci, l'aéroport, le port), les collines de Vinewood, le désert de Grand Senora, Sandy Shores au bord de l'Alamo Sea, Grapeseed et ses champs, le mont Chiliad et Paleto Bay au nord. Il faut environ 3 minutes en voiture pour le traverser. Des routes de campagne et des ponts relient les villes.
- **Bâtiments** : entre dans l'armurerie, l'hôpital, le commissariat (monte sur le toit !), les supérettes, le garage LS Customs, la banque, les stations-service, la maison de Franklin, la villa de Michael (avec piscine), la caravane de Trevor, le bar Yellow Jack, les fermes, les hangars d'avions, les entrepôts du port, le bunker et le donjon du château. Au gratte-ciel Maze Bank, un ascenseur t'emmène sur le toit, à 141 m.
- **Eau** : tu nages dans la mer, les lacs et les rivières (sans pouvoir tirer). Une voiture qui entre dans l'eau profonde coule : tu en sors à la nage. Aux pontons, des hors-bord et des jet-skis t'attendent.
- **Banque** : le coffre-fort contient 2 000 $... mais les prendre te donne 3 étoiles d'un coup !
- **Armes** : on commence avec les poings et un couteau. Les autres s'achètent à l'**armurerie** (A orange sur la mini-carte) ou se ramassent sur les ennemis : pistolet, mitraillette, fusil à pompe, fusil d'assaut. Le **fusil de sniper** ne se vend qu'à l'armurerie : vise avec le clic droit pour regarder dans sa lunette et toucher de très loin. Un tir à la tête fait beaucoup plus de dégâts. Hitler tire au **bazooka** et le lâche quand on le tue : ses roquettes volent moins vite qu'une voiture mais plus vite que toi, explosent et font sauter les voitures : cours sur le côté pour les esquiver !
- **Vie** : elle remonte toute seule si on n'est pas touché pendant 5 secondes. Les trousses de soin rendent 50 points. En voiture, on prend beaucoup moins de dégâts.
- **Gilet pare-balles** : il prend les dégâts à la place de ta vie (barre bleue). Il y en a un dans chaque armurerie et chaque commissariat, un dans le bunker et un dans le château.
- **Police** : faire des bêtises donne des étoiles (jusqu'à 5). À partir de 2 étoiles, la police arrive en voiture. Reste 12 secondes hors de sa vue pour perdre une étoile.
- **Voitures** : elles circulent en ville et sur les routes de campagne. Elles penchent dans les pentes et s'envolent sur les bosses prises trop vite. Appuie sur E à côté d'une voiture pour éjecter le conducteur et la voler. Il y en a 6 types, chacun avec sa vitesse et son bruit de moteur : la classique, la Porsche (180 km/h !), le minibus, le gros 4x4 du désert, la limousine et le tricycle. Attention : sur le tricycle, rien ne te protège des balles.
- **Missions** : suis le point jaune sur la mini-carte et la colonne lumineuse. La dernière mission t'envoie au château Wolfenstein (W rouge sur la mini-carte) pour éliminer Hitler.
- **Carte** : la touche M affiche tout le pays en plein écran et met le jeu en pause. On y voit où on est (flèche blanche), l'objectif (point jaune), le nom des villes et les lieux importants. Elle te dit aussi dans quelle colonne et quelle ligne du tableau `CARTE` tu es.
- **Codes de triche** : appuie sur Entrée, tape le code, puis Entrée. `SLIP`, `CHAUSSURE`, `SOUTIF`, `JAMBEDEBOIS`, `BARCA`, `BEBE`… à toi de voir ce qu'ils font ! Retape un code pour l'annuler.
- **Danse** : tape Q S D trois fois de suite (A S D sur un clavier QWERTY) : B.J. met son chapeau et fait le moonwalk, tourne sur lui-même en poussant son petit cri, puis prend la pose de Michael Jackson, la main entre les jambes : « Who's bad ? ». Bouge pour l'arrêter.
- **WASTED** : si tu meurs, tu te réveilles à l'hôpital le plus proche (+ rouge sur la mini-carte) et tu perds 100 $.

## Modifier le jeu

Tout est dans `index.html`, avec des zones faciles à changer en haut du fichier :

1. **`REGLAGES`** : vitesses à pied et à la nage, vie, dégâts des ennemis, nombre de voitures et de piétons, hauteur des montagnes, touches et durée de la danse… Si le jeu rame, mets `distanceVue: 500` ou `ombres: false`.
2. **`ARMES`** : dégâts, cadence de tir, prix, munitions de chaque arme, rayon d'explosion du bazooka, zoom de la lunette du fusil de sniper.
3. **`VOITURES`** : vitesse, accélération, virage, couleurs et bruit de moteur de chaque type de voiture ou de bateau, et la chance de la croiser. Tu peux en inventer : une « Ferrari » avec le modèle `porsche`, par exemple.
4. **`CARTE`** : tout le pays vu du ciel, le nord en haut. Chaque signe est une case de 74 m. Toutes les lignes doivent avoir la même longueur.

   Les lettres sont des pâtés de maisons : les rues sont ajoutées toutes seules autour.

   | Lettre | Pâté de maisons | Lettre | Pâté de maisons |
   |---|---|---|---|
   | `T` | Tours en verre | `K` | Banque |
   | `I` | Immeubles | `Z` | Gratte-ciel avec ascenseur |
   | `M` | Maisons | `E` | Station-service |
   | `P` | Parc | `L` | Maison de Franklin |
   | `A` | Armurerie | `O` | Villa de Michael |
   | `H` | Hôpital | `R` | Caravane de Trevor |
   | `C` | Commissariat | `J` | Bar Yellow Jack |
   | `S` | Supérette | `F` | Ferme |
   | `G` | Garage LS Customs | `D` | Docks du port |
   | `B` | Bunker nazi (soldats + Kommandant) | `N` | Hangar d'avions |
   | `W` | Château Wolfenstein (soldats + Hitler) | `.` | Place |
   | `X` | Départ du joueur | `a` `b` `d`… | Lieux de mission |

   Les autres signes sont le terrain :

   | Signe | Terrain | Signe | Terrain |
   |---|---|---|---|
   | `~` | Eau (mer, lac, rivière) | `=` | Route |
   | `_` | Plage | `#` | Pont (une route sur l'eau) |
   | `,` | Herbe | `+` | Pont en ville |
   | `;` | Champs | `&` | Ponton avec deux bateaux |
   | `:` | Désert | `!` | Piste d'aéroport |
   | `*` | Forêt | `1` à `9` | Collines et montagnes : plus le chiffre est grand, plus c'est haut |

   Une route (`=`) doit toucher le coin d'un pâté pour se brancher sur les rues d'une ville.

5. **`MISSIONS`** : invente tes missions avec ces étapes : `aller`, `voiture`, `eliminer` (`soldat`, `boss` ou `hitler`), `etoiles`, `semer`, `arme`. Un lieu est une lettre de la carte : `'G'` veut dire « le garage le plus proche ».
6. **`TRICHES`** : renomme les codes ou invente les tiens.

Recharge la page (F5) pour voir tes changements. Le fonctionnement complet du jeu est décrit dans [DESIGN.md](DESIGN.md).
