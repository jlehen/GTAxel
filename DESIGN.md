# GTAxel — Document de design

Mis à jour le 1er octobre 2026. Ce qui a changé, jour par jour, est dans le « Journal des modifications », tout à la fin.

## Vision

GTAxel est un jeu d'action en 3D, en monde ouvert, qui se joue dans le navigateur. Il mélange GTA (ville libre, voitures, police, braquages) et Wolfenstein : on incarne B.J. Blazkowicz, qui chasse les nazis de Los Santos et de ses environs jusqu'au boss final, Hitler, dans le château Wolfenstein, sur le mont Chiliad, puis braque un musée, une bijouterie et une grande banque. Entre deux missions, il peut dévaler à ski, en snowboard ou en luge les pentes enneigées du mont Gordo. Il a été imaginé par un garçon de 10 à 13 ans, qui doit pouvoir le modifier lui-même.

**Piliers de design**

- **Liberté** : dès le départ, on va où on veut, à pied ou en voiture volée. Les missions sont un fil conducteur, pas un couloir.
- **Pardonnant** : les ennemis visent mal, deux policiers seulement peuvent toucher B.J. à la fois, la vie remonte toute seule et la mort ne coûte que 100 $ : on doit pouvoir faire des bêtises sans être puni trop vite. Les braquages sont l'exception voulue : ils doivent être « le plus réalistes possible », donc dangereux (vigiles qui visent bien, mitrailleuses, fumée toxique, heavy robot). Mourir y coûte toujours 100 $, et on garde le butin déjà volé.
- **Bidouillable** : tout tient dans un seul fichier `index.html`. Les réglages, les armes, les voitures, les ennemis, la carte, les sommets, les remontées, les pistes de ski, les missions et les traductions sont des tableaux commentés en français, en haut du fichier. On voit une modification en appuyant sur F5. Les nombres de `REGLAGES`, `ARMES`, `ARMES_ROBOT`, `VOITURES` et `ENNEMIS` se changent aussi dans le menu, sans ouvrir le code (voir « L'écran des réglages »).
- **Zéro installation** : un double-clic ou un lien suffit, pourvu qu'on ait Internet. En ligne : [jlehen.github.io/GTAxel](https://jlehen.github.io/GTAxel/).

Pas de sang ni de gore : les personnages touchés tombent au sol. Pas de croix gammée non plus : les nazis se reconnaissent à leur uniforme, leur casque allemand et leur brassard rouge, et leurs bannières portent un W pour Wolfenstein.

## Boucle de jeu et contrôles

Le joueur alterne entre deux boucles. Les missions rapportent l'argent qui achète des armes ; les bêtises attirent la police jusqu'à ce qu'on la sème ou qu'on meure.

```mermaid
flowchart LR
  E[Explorer le pays<br>à pied, en voiture, en bateau ou en avion]
  E --> M[Faire une mission<br>suivre le point jaune] --> G[Gagner de l'argent<br>200 à 250 000 $] --> A[Acheter des armes<br>à l'armurerie]
  A -- armes plus fortes : bunker, puis château --> E
  E --> B[Faire des bêtises<br>voler, frapper, tirer] --> P[La police arrive<br>1 à 5 étoiles]
  P --> S[Semer la police<br>12 s caché = -1 étoile] --> E
  P --> W[WASTED<br>la vie tombe à 0] --> H[Réveil à l'hôpital<br>-100 $, plus d'étoiles] --> E
```

Une partie commence à pied, sans argent, avec les poings et un couteau. Le héros, B.J. Blazkowicz, a les cheveux blonds courts, un maillot blanc à manches courtes et un pantalon militaire. Il n'y a pas de fin : après la 10e mission, le pays reste libre.

### Contrôles

| Touche | À pied | En voiture |
| --- | --- | --- |
| Z Q S D ou flèches | Se déplacer | Accélérer, freiner, tourner |
| Q S D, 3 fois de suite | Danser comme Michael Jackson | Rien |
| Souris | Regarder | Tourner la caméra autour de la voiture |
| Clic gauche | Tirer ou frapper (pas en nageant ; en volant, tirer seulement) | Rien |
| Clic droit | Viser (zoom, tir plus précis ; lunette avec le fusil de sniper) | Rien |
| Maj | Courir ; en volant, chaque appui le fait aller plus vite | Rien |
| Maj, 3 fois de suite (en moins de 0,6 s) | Voler comme Superman, ou arrêter de voler | Rien |
| Espace | Sauter (environ 1 m), rien en nageant | Frein à main, virage plus serré ; à ski, en snowboard ou en luge : sauter |
| Ctrl ou C | S'accroupir (bascule) | Rien |
| E ou F | Monter en voiture, en bateau, en avion, en hélicoptère, sur des skis, un snowboard ou une luge, acheter une arme ou le masque à gaz, prendre l'ascenseur, un télésiège ou la télécabine, parler au garagiste, voler le butin, poser la perceuse ou l'explosif, éjecter le pilote du heavy robot ou monter dedans ; sur le télésiège, sauter du siège | Descendre (pas en plein looping, ni en plein vol) ; en marche, B.J. saute et roule par terre. À ski, au départ d'une remontée : la prendre, avec ses skis |
| V | 1re ou 3e personne | Vue intérieure ou extérieure |
| 1 à 8, molette | Changer d'arme (9 : les yeux laser, avec le code `SUPERMAN` ou `DIEU`) | Rien |
| M | Ouvrir ou fermer la grande carte | Ouvrir ou fermer la grande carte |
| Entrée | Taper un code de triche | Taper un code de triche |
| Échap | Pause | Pause |

Les touches sont repérées par leur position : Z Q S D sur un clavier AZERTY, W A S D sur un QWERTY. Seule la touche M suit la lettre imprimée sur le clavier.

**En avion** : Z accélère, S ralentit (et freine au sol). L'avion va là où l'on regarde avec la souris ; au clavier, Q et D tournent, Espace et C lèvent ou baissent le nez. **En hélicoptère** : Espace monte, C descend, Z Q S D le font avancer, reculer et glisser sur le côté, la souris le tourne. Dans les deux, V passe de la vue derrière à la vue du cockpit, et E ne fait descendre qu'une fois posé (voir « Avions et hélicoptères »).

**Sur une échelle** : on grimpe en avançant vers le mur, on descend en s'en éloignant, Espace fait lâcher prise.

**À ski, en snowboard ou en luge** : Z pousse sur le plat (à ski avec les bâtons, en snowboard avec le pied arrière), S freine (en chasse-neige, puis recule un peu), Q et D tournent, même sur place, Espace fait sauter d'un mètre. C'est la pente qui fait avancer (voir « La glisse »).

**Dans le heavy robot** : Z Q S D le font marcher (4 m/s, 6 m/s avec Maj), la souris le tourne et vise, le clic gauche tire à la mitrailleuse lourde, le clic droit lance une roquette, E fait descendre, V passe de la vue derrière l'épaule à la vue dans la cabine. On ne peut ni sauter, ni s'accroupir, ni changer d'arme, ni danser.

### Déplacements

| Allure | Vitesse |
| --- | --- |
| Course (Maj) | 8 m/s |
| Marche | 4 m/s |
| En visant | 2,4 m/s |
| Accroupi | 2 m/s |
| Nage (Maj) | 4 m/s |
| Nage | 2,2 m/s |
| Moonwalk (pendant la danse) | 1,5 m/s, à reculons |
| Sur une échelle | 2,5 m/s, vers le haut ou vers le bas |
| En volant (Superman) | 12 m/s, + 12 m/s à chaque appui sur Maj, jusqu'à 100 m/s (360 km/h) |

Le code de triche `Z6PO` multiplie toutes ces vitesses par 0,6, sauf celles du vol.

- Une marche de 60 cm au plus se monte sans sauter (`PASMAX`) : escaliers, trottoirs, lits, conteneurs empilés... Le terrain, lui, se monte à pied quelle que soit la pente.
- **Nage** : là où l'eau est trop profonde pour avoir pied (plus de 1,30 m), B.J. nage, couché à la surface. Il ne peut ni tirer, ni sauter, ni s'accroupir, et son arme est rangée. En nageant, il remonte sur une plage ou un ponton (marche de 1,90 m au plus). On ne se noie pas.

### Sauter, tomber, rouler

- **Le saut** monte à 1 m (`forceSaut` 6 m/s, `gravite` 18 m/s²). En montant, B.J. replie les jambes (celle d'appel plus que l'autre) et lance les bras en avant ; en redescendant, il tend les jambes vers le sol et écarte les bras pour l'équilibre. S'il tombe de haut (plus de 9 m/s, soit après 2,25 m de chute), il pédale et fait des moulinets avec les bras. Avec une arme à la main, seules les jambes bougent. La pose change en douceur, en un dixième de seconde environ. Il la garde pendant tout le saut, sommet compris, jusqu'à ce qu'il retombe ; en descendant un escalier, elle ne vient que s'il tombe vite (plus de 4 m/s). Ses membres ont du poids (voir « Les personnages ») : ils restent un peu en arrière quand il s'élance, et les moulinets suivent les bras avec un temps de retard.
- **L'atterrissage** : il amortit en pliant les genoux, d'autant plus qu'il tombe vite (à fond à 14 m/s), puis se redresse en un tiers de seconde. Son buste, sa tête et ses bras continuent sur leur lancée, puis reviennent ; ses pieds, eux, restent posés.
- **Tomber de haut fait mal** : au-delà de 4 m (`hauteurSansMal`), il perd 10 points de vie par mètre en plus (`degatsChute`). Le gilet pare-balles ne protège pas. Mesuré : de 3 m, rien ; de 9 m, 50 points ; de 20 m, il meurt (on meurt à partir de 14 m). Tomber dans l'eau profonde ne fait rien. La hauteur est calculée d'après la vitesse à l'arrivée (hauteur = vitesse² ÷ 2 × gravité) : une échelle lâchée de haut, un toit, un avion qui explose en vol, tout compte.
- **Après une chute qui fait mal**, s'il ne bougeait pas, il se reçoit sur un genou, le poing droit au sol, la jambe gauche devant, le bras gauche en arrière, et reste ainsi 0,9 s sans pouvoir bouger ni sauter. S'il courait ou marchait (plus de 3 m/s à l'horizontale), il fait une roulade.
- **La roulade** : B.J. se met en boule (les genoux contre la poitrine, les bras autour, la tête rentrée) et roule dans le sens où il allait, sans qu'on puisse le diriger, ni tirer, ni monter en voiture. Il perd 12 m/s chaque seconde (12 m/s² de frottement), fait un tour tous les 3 m environ (2 tours par seconde au plus), bute contre les murs, et nage s'il roule dans l'eau profonde. Presque arrêté (moins de 1,5 m/s), il finit son tour, se déplie en un quart de seconde, se retrouve accroupi et se relève. Son arme est rangée pendant la roulade. Plus il va vite, moins il arrive à rester en boule (`raideur` de 25 à 8, entre 4 et 20 m/s) : sorti d'une voiture lancée, ses bras et ses jambes battent et claquent par terre.
- **Sauter d'un véhicule lancé** : au-dessus de 4 m/s (14 km/h), B.J. sort en roulade, dans le sens où allait le véhicule, avec sa vitesse. Au-delà de 10 m/s (36 km/h, `vitesseSansMal`), ça fait mal : 1,5 point par m/s en plus (`degatsRoulade`), sans que le gilet protège ; même à 209 km/h (la Lamborghini), on perd 72 points au plus, donc on ne meurt pas si on avait toute sa vie. Mesuré : à 36 km/h, 2 tours sur 3,5 m sans mal ; à 72 km/h, 3 tours sur 15 m et 13,5 points ; à 108 km/h, 5 tours sur 33 m et 28 points. Pas de roulade en sortant d'un bateau (on tombe à l'eau). Un véhicule qui explose éjecte B.J. de la même façon.
- **En mourant**, B.J. s'effondre comme les autres personnages (voir « Les personnages ») ; s'il était en l'air, il tombe jusqu'au sol.
- **Avec le code `SUPERMAN` ou `DIEU`**, tomber de haut ne fait pas mal : B.J. se reçoit toujours sur un genou, et c'est ce qu'il y a dessous qui est écrasé (voir « Les super-pouvoirs de SUPERMAN et de DIEU »).

### La danse

Taper gauche, arrière, droite trois fois de suite (Q S D Q S D Q S D, ou A S D sur un clavier QWERTY) fait danser B.J. comme Michael Jackson. Il faut 9 touches sans aucune autre au milieu ; il n'y a pas de temps limite. Les touches sont dans le réglage `touchesDanse`.

La danse dure 6 s, en trois pas. Leurs durées sont dans le réglage `moonwalk` (3, 1 et 2 s).

| Pas | Durée | Ce que fait B.J. |
| --- | --- | --- |
| Moonwalk | 3 s | Il se met de profil et recule d'environ 4,4 m, à 1,5 m/s (`vitesseMoonwalk`). Ses jambes marchent vers l'avant, le pied qui avance glisse sur la pointe. La tête baissée, le coude en avant, il tient le bord de son chapeau de la main droite ; son bras gauche bouge à peine. « Moonwalk ! » s'affiche |
| Toupie | 1 s | Il fait 2 tours et quart sur la pointe des pieds, vite puis de moins en moins, la main droite toujours au chapeau, le bras gauche serré contre lui et un genou plié. Il pousse son petit cri : « hi-hiii ! » |
| Pose | 2 s | Face à la caméra, d'un coup sec, le geste de Michael Jackson : la main droite entre les jambes, le bras gauche tendu sur le côté, les genoux pliés et écartés, sur la pointe des pieds, le bassin en avant, la tête baissée sous le chapeau. « WHO'S BAD ? » s'affiche |

- La danse passe en 3e personne, pour qu'on la voie. Les angles sont pris par rapport à la caméra au moment où la danse commence ; ensuite, la souris tourne autour de B.J. sans le déranger.
- **Le chapeau** : un chapeau noir à ruban clair, rabattu sur les yeux. B.J. le porte du début à la fin de la danse, et seulement pour danser.
- B.J. range son arme pour danser. Le moonwalk s'arrête contre un mur comme une marche normale.
- Appuyer sur une touche pour bouger, sauter ou s'accroupir, tirer ou viser arrête la danse tout de suite. Monter en voiture, tomber à l'eau ou mourir aussi. La dernière touche de la suite, si elle reste enfoncée, ne l'arrête pas.
- On ne danse qu'à pied : en voiture, en bateau ou en nageant, la suite de touches ne fait rien.
- Comme ce sont les touches pour se déplacer, B.J. fait quelques pas de côté et en arrière avant de danser.

### Voler comme Superman

Taper Maj trois fois de suite, en moins de 0,6 s (`tripleMaj`), fait décoller B.J. : « Superman ! » s'affiche, il s'élance vers le ciel (à 8 m/s, il monte d'environ 4 m), puis flotte sur place. Ça marche à pied, en nageant, sur une échelle, pendant une roulade ou une danse ; pas en voiture, ni dans le heavy robot.

- **Commandes** : Z le fait voler là où l'on regarde (vers le haut ou vers le bas, comme l'avion), S en arrière, Q et D sur le côté ; Espace le fait monter, C ou Ctrl descendre. Il vole à 12 m/s (`vitesseVol`). Il prend sa vitesse, et s'arrête, en une demi-seconde environ.
- **Accélérer** : chaque appui sur Maj en volant ajoute 12 m/s (`vitesseVolMaj`) : 24 m/s après 1 appui, 36 après 2, et ainsi de suite jusqu'à 100 m/s (360 km/h, `vitesseVolMax`), plus vite que l'avion. Garder Maj enfoncé ne compte que pour un appui. Quand il s'arrête (aucune touche pour avancer, glisser, monter ou descendre), il repart à 12 m/s. Pendant le vol, sa vitesse s'affiche en km/h, comme en voiture. Attention : 3 appuis en moins de 0,6 s arrêtent le vol, il faut les espacer.
- **La pose** : lancé, il se couche dans le sens où il va, le poing droit tendu au-dessus de la tête, le bras gauche le long du corps, les jambes tendues, un genou à peine plié. En montant tout droit, il reste debout, le bras levé. Sur place, ou en descendant tout droit, il flotte debout, les bras un peu écartés, les jambes qui pendent. Il bascule autour de son bassin, et plus il va vite, plus il se couche (à fond à partir de 6 m/s). Ses membres ont du poids : ils traînent un peu quand il tourne.
- **Les virages** : lancé, il penche dans ses virages, comme l'avion : une épaule plonge vers l'intérieur du virage, jusqu'à 36° (`roulisVirage`). Plus il va vite, plus il penche (à fond à partir de 6 m/s) ; sur place, il reste droit. Il ne penche pas quand il tire ou vise.
- **Se poser** : s'il touche le sol, un toit ou l'eau profonde en descendant, il se pose sans se faire mal, en pliant les genoux (dans l'eau, il se met à nager). En volant à l'horizontale ou en montant, il glisse sur le sol ou sur la pente sans se poser. Les murs l'arrêtent, comme à pied. Avec le code `SUPERMAN` ou `DIEU`, s'il arrive en piqué (plus de 12 m/s vers le bas, ce qui demande au moins un appui sur Maj), il écrase tout comme en tombant (voir « Les super-pouvoirs de SUPERMAN et de DIEU ») ; à la vitesse normale, il se pose en douceur.
- **Arrêter en l'air** : taper encore Maj trois fois de suite. Il tombe, et la chute compte comme les autres (voir « Sauter, tomber, rouler ») : de plus de 4 m au-dessus du sol, ça fait mal ; de 14 m, il meurt.
- **Tirer** : avec une arme à feu, le clic gauche tire et le clic droit vise, comme à pied (lunette du sniper comprise). Pour tirer ou viser, B.J. sort son arme, se tourne vers le viseur et tend les bras dans cette direction, même couché à l'horizontale ou en visant vers le haut ou vers le bas ; il se penche alors dans le sens où il va par rapport au viseur (en arrière s'il recule). Il range son arme peu après le dernier tir (une demi-seconde après la cadence de l'arme), et reprend sa pose de Superman. Au-dessus de 5 m/s, les balles s'écartent deux fois plus, comme en courant. Les poings et le couteau ne servent pas en l'air (ils toucheraient quelqu'un loin en dessous) : le viseur est caché. Avec les yeux laser, il se tourne vers le viseur mais garde sa pose de Superman : il n'a rien à tenir.
- En volant, B.J. ne s'accroupit pas et ne danse pas. Au-dessus de 6 m/s, il est plus dur à toucher, comme quand il court. Monter en voiture ou dans le heavy robot arrête le vol ; mort en plein vol, il tombe.

### Caméras

- **3e personne (par défaut)** : caméra 3,8 m derrière l'épaule droite. En visant, elle se rapproche à 1,8 m et le champ de vision passe de 70° à 45°. Elle avance quand un mur, une cloison, un plancher ou un meuble la gêne, et reste toujours à 25 cm de tout (`MARGE_CAMERA`) : plus près, le bord de l'image passerait à travers, et on verrait un instant la pièce d'à côté ou celle du dessus.
- **1re personne (V)** : l'arme est dessinée par-dessus la scène, avec balancement et recul.
- **Lunette du fusil de sniper** : en visant, le champ de vision passe à 14° (70° divisé par le `zoom` de l'arme, qui vaut 5). L'écran devient noir autour d'un rond, avec deux traits noirs en croix. La souris est 5 fois plus douce, pour viser finement. L'arme en 1re personne n'est plus dessinée. En 3e personne, la caméra reste derrière l'épaule, et le noir cache B.J.
- **En voiture** : caméra 8 m derrière une voiture classique, 11 m derrière une limousine, 6 m derrière un tricycle. Elle recule avec la vitesse et se recale seule après 1,5 s sans bouger la souris. En vue intérieure (V), les yeux sont à la place du conducteur.
- **Mort** : vue plongeante sur le corps pendant 3,5 s.
- La caméra ne passe ni sous le terrain ni sous l'eau.

## Le monde

Le pays est une île inspirée de celle de GTA 5, en plus petit et plus simple : Los Santos au sud, avec son aéroport et son port, les collines de Vinewood, le désert de Grand Senora et Sandy Shores au bord de l'Alamo Sea, puis le mont Chiliad et Paleto Bay au nord, et à l'est les très hautes montagnes enneigées du mont Gordo et du San Chianski. Il mesure environ 5,5 km d'ouest en est (3,6 km sans les montagnes de l'est) et 5,2 km du nord au sud. Il faut à peu près 3 minutes en voiture classique pour le traverser du sud au nord.

Tout est construit au chargement à partir du tableau `CARTE` de `index.html` : 70 lignes de 74 signes, le nord en haut. Chaque signe est une case de 74 m. Une lettre est un pâté de maisons de 60 m, entouré de rues de 14 m. Les autres signes sont du terrain, sans rues. Le pays est le même à chaque partie.

La carte compte 315 pâtés, dont 155 d'immeubles, 55 de maisons, 25 de tours, 23 de docks et une station de ski. Il y a aussi 63 cases de piste d'aéroport (dont 2 avec un avion et 2 avec un hélicoptère), 136 cases de route et 2 324 cases d'eau. Les très hautes montagnes ne sont pas dans la carte, mais dans le tableau `SOMMETS` (voir « Les sommets et la neige ») ; les remontées et les pistes de ski sont dans les tableaux `REMONTEES` et `PISTES_SKI`.

### Les signes de la carte

| Signe | Contenu |
| --- | --- |
| `T` | Une grande tour de 20 à 45 étages, ou 4 tours de 12 à 29 étages, en verre ou modernes |
| `I` | 2 ou 4 immeubles de 3 à 10 étages, en brique, béton ou modernes, avec une porte sur la rue. On entre dans environ 1 sur 5 (voir « Les immeubles où l'on entre ») |
| `M` | 4 maisons avec pelouse et arbres, 1 voiture garée |
| `P` | Pelouse, allées pavées, fontaine, jusqu'à 14 arbres, 1 trousse de soin |
| `.` `X` `a`–`z` | Place pavée avec 4 arbres et 2 voitures garées, entourée de bornes en béton (une tous les 3 m, à 3 m du bord, sauf sur 12 m au milieu de chaque côté pour entrer en voiture). `X` est le départ, les minuscules sont les lieux de mission |
| `A` `H` `C` `S` `G` `K` `Z` `E` `L` `O` `R` `J` `F` `D` `N` `B` `W` | Pâtés où l'on peut entrer (tableau plus bas) |
| `U` `V` `Q` | Pâtés à braquer, où l'on entre aussi : musée, bijouterie, grande banque (voir « Braquages ») |
| `Y` | Station de ski : une place enneigée, un chalet, et la gare du bas d'un télésiège qui monte au sommet le plus proche du tableau `SOMMETS` (voir « La station de ski et les remontées ») |
| `~` | Eau : mer, lac ou rivière |
| `_` | Plage de sable |
| `,` | Herbe, avec des arbres par-ci par-là |
| `;` | Champs, en bandes jaunes et vertes |
| `:` | Désert, avec des cactus |
| `*` | Forêt de sapins |
| `1` à `9` | Colline ou montagne : 30 m par chiffre (`hauteurMontagnes`), donc 270 m pour un `9` |
| `=` | Route de campagne |
| `#` | Pont : une route qui passe sur l'eau |
| `+` | Pont en ville : les rues autour de cette case d'eau passent dessus |
| `&` | Ponton en planches, avec un hors-bord et un jet-ski amarrés |
| `!` | Piste d'aéroport |
| `^` | Piste d'aéroport avec un avion à piloter |
| `@` | Piste d'aéroport avec une hélistation et un hélicoptère à piloter |

### Le relief et l'eau

- **Hauteur du terrain** : chaque case a une hauteur (tableau `ALTITUDE` : –9 m pour l'eau, 0,3 m pour la plage, 1,5 m pour l'herbe, 3 m pour le désert, 4 m pour la forêt, 30 m par chiffre). Le terrain passe en douceur d'une case à l'autre, avec des bosses en plus (jusqu'à 1,2 m, plus en montagne ; sur les sommets du tableau `SOMMETS`, de grandes arêtes à la place). Une route prend la hauteur moyenne des cases autour d'elle.
- **Villes à plat** : les pâtés qui se touchent (même en diagonale) forment une ville, toute à la même hauteur : celle du terrain le plus bas autour d'elle, jamais sous 0 m. Los Santos, Sandy Shores et Paleto Bay sont au bord de l'eau, donc à 0 m. La maison de Franklin, dans les collines, est à 30 m ; le château Wolfenstein, sur le mont Chiliad, à 150 m. Autour d'une ville et de ses rues, le terrain reste plat sur 4 m, puis rejoint le reste en 40 m.
- **Eau** : un grand plan à 1 m sous les rues (`EAU`), qui ondule et reflète le ciel. Là où le terrain passe dessous, il y a de l'eau. Les bords de l'eau sont sablés.
- **Couleurs** : herbe, forêt, champs, désert ou sable selon la case, mélangées d'une case à l'autre. La roche grise (ou rousse dans le désert) apparaît sur les pentes raides et au-dessus de 260 m. La neige couvre le haut des sommets du tableau `SOMMETS`, sauf leurs pentes de plus de 55°, et s'en va par plaques en descendant.
- **Végétation** : 12 sapins par case de forêt, 5 en montagne (2 au-dessus de 7), 2 arbres par case d'herbe, 1 cactus par case de désert, 2 palmiers par case de plage à Los Santos, et des rochers dans les montagnes. Dans la neige, des sapins givrés, et plus aucun arbre au-dessus de 350 m. Rien ne pousse sur les pistes de ski, ni sous les câbles des remontées.

### Les sommets et la neige

Les très hautes montagnes ne sont pas dessinées avec des chiffres dans `CARTE` (270 m au plus), mais décrites dans le tableau `SOMMETS`, juste après la carte : un nom, une case (`col`, `ligne`), une hauteur et un rayon en cases. Leur nom s'écrit sur la grande carte, juste sous le sommet.

| Sommet | Case | Hauteur | Rayon | Sommet mesuré |
| --- | --- | --- | --- | --- |
| Mont Gordo | colonne 54, ligne 20 | 900 m | 17 cases (1 258 m) | 855 m |
| San Chianski | colonne 57, ligne 34 | 650 m | 11 cases (814 m) | 606 m |

- **Forme** : un sommet ajoute `hauteur × (1 − d)²` à la hauteur des cases de terre (`sommetEn`), d allant de 0 au sommet à 1 au pied, au bout du rayon. La pente est raide en haut et douce en bas : pour le mont Gordo, environ 55° près du sommet, 45° à mi-hauteur (430 m), 35° à 225 m et 12° tout en bas. Là où deux sommets se chevauchent, c'est le plus haut des deux qui compte, ce qui creuse un col entre eux (à 210 m, entre le mont Gordo et le San Chianski). Comme le reste du terrain, le tout est adouci d'une case à l'autre : les sommets sont arrondis, un peu moins hauts que prévu.
- **Des replats et des murs** : la pente n'est pas régulière. Entre le sommet et le pied, elle s'adoucit et se raidit 5 fois (tous les 250 m sur le mont Gordo, tous les 160 m sur le San Chianski), de 35 % en plus ou en moins, sans jamais remonter. Ces vagues ne font pas des cercles parfaits : elles se décalent d'un versant à l'autre. Tout près du sommet (les premiers 8 % du rayon), il n'y en a pas. Sur les murs de plus de 55°, on voit la roche.
- **Pas dans l'eau** : une case d'eau ne monte pas (un sommet qui déborde sur la mer fait des falaises sur la côte), et un sommet posé sur l'eau déclenche une alerte.
- **Routes et villes** : le sommet est ajouté à la hauteur des cases avant le calcul des routes et des villes : une ville posée sur la pente est aplanie comme les autres.
- **Bosses** : sur les sommets, pas de petites bosses (on y skie), mais de grandes arêtes et de grands creux de 260 m de large, jusqu'à 6 % de la hauteur que le sommet ajoute à cet endroit. Ailleurs, les bosses suivent la hauteur du terrain sans les sommets.
- **La neige** dépend de la hauteur que la montagne ajoute au terrain : au-dessus de 150 m (`neigeHaut`), tout est blanc ; en dessous de 25 m (`neigeBas`), il n'y en a plus ; entre les deux, elle s'en va par plaques, de plus en plus rares en descendant (`neigeEn`). Mesuré à l'ouest du mont Gordo, loin des pistes : tout blanc jusqu'à 700 m du sommet, les trois quarts à 750 m, un tiers à la moitié vers 800 à 850 m, moins d'un cinquième à 900 m, plus rien à 1 000 m (la station est à 1 150 m). Les pistes de ski gardent leur neige jusqu'en bas, sur leur largeur et 12 m de chaque côté en s'effaçant. Sur les pentes de plus de 55° environ, la neige ne tient pas : on voit la roche. Elle se voit aussi sur la mini-carte et la grande carte.
- **Arbres** : dans la neige, tous les arbres sont des sapins givrés, d'un vert très pâle, et il n'en pousse plus au-dessus de 350 m.
- **Dans la carte**, les cases sous les sommets sont de l'herbe (`,`), avec de la forêt au pied, au nord, à l'est et au sud, et une plage là où cette terre touche la mer. Les anciennes collines à l'est de la Senora Freeway, au nord-est et au sud-est de Grapeseed (lignes 9 à 14 et 18 à 21), ont été aplanies : c'est maintenant le pied du grand massif.

### La station de ski et les remontées

La station de ski (`Y`, colonne 39, ligne 16) est au pied du mont Gordo, au bord de la Senora Freeway, juste à l'est de Grapeseed ; une case de route (`=`) la branche sur la freeway. C'est une place enneigée, avec un chalet et deux gares : celle du télésiège du mont Gordo (toit rouge) et, 22 m plus au nord, celle de la télécabine des Marmottes (toit jaune). Sur les cartes, c'est un rond bleu marqué d'un flocon (❄). Avec ses 4 remontées, ses 8 pistes et son boardercross, c'est un vrai domaine skiable (voir « Les pistes de ski »).

| Remontée | De | À | Câble | Pylônes | Sièges | Trajet |
| --- | --- | --- | --- | --- | --- | --- |
| Télésiège du Mont Gordo | La station (2 m) | Près du sommet du mont Gordo (819 m) | 1 409 m | 22 | 133 sièges | 106 s |
| Télécabine des Marmottes | La station (2 m) | L'épaule nord-ouest du mont Gordo (279 m) | 774 m | 15 | 34 cabines | 65 s |
| Télésiège du San Chianski | Le col entre les deux montagnes (209 m) | Près du sommet du San Chianski (577 m) | 512 m | 8 | 61 sièges | 46 s |
| Télésiège du Col | Le col (210 m) | Le versant sud du mont Gordo (695 m) | 748 m | 12 | 80 sièges | 62 s |

- **Le tracé** : de chaque `Y`, un télésiège monte tout droit vers le sommet le plus proche du tableau `SOMMETS`, et s'arrête à 5 % de son rayon avant le sommet. Les autres remontées sont dans le tableau `REMONTEES`, après la carte : un nom, la case de la gare du bas (`de`) et celle de la gare du haut (`vers`), avec des virgules si on veut (48.5 = entre deux colonnes), et `cabines: true` pour une télécabine. Autour d'une gare qui n'est pas sur une place `Y`, le terrain est mis à plat sur 14 m, puis rejoint la pente en 20 m.
- **Les gares** : un quai en pierre de 8 × 12 m, quatre poteaux, un toit (rouge pour un télésiège, jaune pour la télécabine), et la grande roue où tourne le câble, à 3,2 m au-dessus du quai. Le câble reste à plat, à 3,2 m, jusqu'au portique de la gare, à 7 m du milieu : il passe sous le toit (5,2 m), et les sièges avec lui.
- **Les pylônes** : un tous les 60 m environ, 10 m au-dessus du terrain. Le câble passe partout à 7 m au moins au-dessus du terrain (3,2 m au sortir des gares, puis de plus en plus sur 20 m) : là où il frôle le plus, le jeu ajoute un pylône, jamais à moins de 10 m d'une gare, et recommence. Sur la traverse de chaque pylône et de chaque portique, sous chaque câble, un balancier porte 4 poulies noires où roule le câble. On bute contre les pylônes, à pied comme à ski.
- **Les sièges** : un tous les 25 m en ligne, bleus, suspendus 2,4 m sous le câble, à deux places. Ils montent à droite (en regardant le haut), font le tour de la grande roue, et redescendent vides à gauche, à 15 m/s (`vitesseTelesiege`).
- **Débrayables** : à moins de 9 m d'une gare, les sièges ralentissent à 2 m/s (`vitesseGare`) pour qu'on monte dessus, puis reprennent leur vitesse en 30 m. Ils se resserrent donc dans les gares : un tous les 3,30 m. Avec `vitesseGare` égal à `vitesseTelesiege`, ils ne ralentissent plus.
- **Le garde-corps** : deux bras, une barre devant le ventre et un repose-pieds. Il est levé dans les gares et se baisse en route, entre 12 et 30 m de la gare.
- **Les cabines** de la télécabine : une tous les 60 m, rouges, jaunes, bleues, vertes ou orange. Un toit, un plancher, des parois basses sur trois côtés (on entre par la droite), un banc au fond, à deux places. Les skis, le snowboard ou la luge voyagent dehors, debout contre la paroi.
- **Monter** : à pied, ou sur des skis, un snowboard ou une luge, appuyer sur E sous le toit de la gare du bas, à moins de 3,5 m du départ (« Appuie sur E pour prendre le télésiège », ou « la télécabine »). B.J. s'assoit sur le siège libre le plus proche parmi ceux qui sont dans la gare : un vrai siège de la remontée, pas un siège à lui. S'il n'y en a pas (toutes les places prises, ou pas de cabine en gare), il suffit de rappuyer. Il ne peut pas tirer, ni danser, ni voler. La souris tourne la caméra.
- **Sur le siège**, ses skis sont à ses pieds, son snowboard pend à son pied avant (le droit), la planche de travers ; sa luge est posée sur ses genoux. Mesuré : le milieu des fixations des skis à 6 cm de ses pieds, la fixation avant du snowboard à 11 cm.
- **Sauter du siège** : E en route (« Appuie sur E pour sauter du télésiège », ou « de la cabine ») : il tombe, et la chute compte comme les autres (voir « Sauter, tomber, rouler » ; à ski, voir « La glisse »). Mesuré : à ski, sauté de 6 m, il se reçoit sans mal.
- **En haut**, B.J. descend du siège 5 m avant le milieu de la gare, et se retrouve à 4 m à droite, tourné vers la pente, sur ses skis s'il en avait. La gare est sur un replat : il faut pousser (Z) pour en sortir.
- **Les skis, le snowboard et la luge des gares** : un de chaque en bas et en haut de chaque remontée, à droite du câble (à 6,5, 7,8 et 9,1 m), tournés vers la pente : 24 en tout. À chaque arrivée en haut, il en revient un de chaque, en bas et en haut, s'il n'y en a plus à moins de 12 m (`garnir`). Ils sont à tout le monde : les prendre n'est pas un vol, même devant la police.

### Les pistes de ski

Les pistes sont dans le tableau `PISTES_SKI`, après `REMONTEES` : un nom, une couleur, et les points par où elle passe (`[colonne, ligne]`, du haut vers le bas). Le jeu trace une courbe douce par ces points.

| Piste | Couleur | Longueur | De… à | Pente moyenne (la plus raide) | Kickers | Elle va |
| --- | --- | --- | --- | --- | --- | --- |
| La Gordo | Noire | 1 051 m | 805 à 2 m | 37° (58°) | 2 | Du haut du télésiège du mont Gordo à la station, au sud du câble |
| Les Crêtes | Rouge | 525 m | 813 à 295 m | 45° (62°) | 1 | Du haut du télésiège du mont Gordo au haut de la télécabine |
| Les Marmottes | Bleue | 669 m | 283 à 2 m | 23° (32°) | 2 | Du haut de la télécabine à la station, entre les deux câbles |
| Boardercross | Rouge | 671 m | 253 à 11 m | 20° (43°) | 3 | Du haut de la télécabine à la station, au nord du câble |
| Le Col | Rouge | 630 m | 803 à 203 m | 44° (68°) | 1 | Du haut du mont Gordo au col |
| La Liaison | Rouge | 405 m | 683 à 443 m | 31° (49°) | | Du haut du télésiège du Col à La Gordo |
| Le San Chianski | Noire | 298 m | 569 à 224 m | 49° (59°) | | Du haut du San Chianski au col |
| Hors-piste du Gordo | Jaune | 445 m | 811 à 307 m | 49° (58°) | | Du haut du mont Gordo au haut de la télécabine, tout droit |

- **Largeur** : 32 m (14 m pour un boardercross). Aucune piste ne remonte : c'est vérifié sur chacune, point par point.
- **Le balisage** : un piquet de 1,80 m de la couleur de la piste tous les 30 m de chaque côté (tous les 15 m sur le boardercross) ; ceux de droite, en descendant, ont le haut orange, comme sur les vraies pistes. Jaune, c'est un hors-piste. Au départ, un panneau à la couleur de la piste porte son nom, écrit des deux côtés. On passe à travers les piquets.
- **La neige** : une piste garde sa neige jusqu'en bas, même là où la montagne n'en a plus : de loin, ce sont des rubans blancs dans l'herbe. Aucun arbre, aucun rocher n'y pousse (ni à moins de 8 m sous un câble).
- **Les kickers** (`kickers: [520, 900]`, à tant de mètres du départ) : un tremplin de neige de 1,20 m de haut, 10 m de long et 7 m de large, sur un côté de la piste (une fois à gauche, une fois à droite). Il monte en courbe (13° de plus que la pente au bout), et au bout, le vide. Mesuré : sur Les Marmottes, à 43 km/h, 1 s en l'air et 19 m ; à 72 km/h, 1,2 s et 27 m ; sur La Gordo, à 90 km/h, 1 s et 27 m, à 2,3 m de la neige. On se reçoit toujours sans tomber.
- **Sur les cartes**, chaque piste est un trait de sa couleur, et la légende de la grande carte les explique.

**Le boardercross** (`boardercross: true`) est une piste étroite, en zigzag :

- **Des virages relevés** : le bord extérieur de chaque virage monte comme un mur, jusqu'à 3,5 m (à fond dès que le virage tourne sur moins de 35 m de rayon).
- **Des bosses à la file** (les « whoops ») dans les lignes droites : 4 bosses de 90 cm, une tous les 12 m, tous les 150 m.
- **Trois kickers** au milieu de la piste (1 m de haut, 7 m de long, 11 m de large), et un bourrelet de neige de 50 cm le long de chaque bord.
- **Le chronomètre** : deux banderoles en travers, « DÉPART » (rouge, à 10 m du début) et « ARRIVÉE » (jaune, à 15 m de la fin). Sur des skis, un snowboard ou une luge, passer sous la première lance le chronomètre (« BOARDERCROSS : Top départ ! »), qui s'affiche à côté de la vitesse ; passer sous la seconde l'arrête (« 25.4 s : nouveau record ! »). Sortir de la piste de plus de 4 m annule le tour. Le record reste jusqu'à ce qu'on ferme la page. Mesuré : 25,4 s en suivant le milieu de la piste sans freiner, 113 km/h au plus, 3 décollages.
- Ce relief est trop fin pour la grille du terrain (un point tous les 9,25 m) : il est ajouté à la hauteur du terrain et dessiné par-dessus, en neige un peu bleutée, avec un point par mètre.

**Les autres skieurs** : 30 personnes (`skieurs`) skient, font du snowboard ou de la luge (un tiers chacun), en anorak et bonnet de toutes les couleurs, les skieurs avec des bâtons.

- Chacun descend une piste en slalom, à 25 à 47 km/h. En bas, il va au départ d'une remontée à moins de 100 m, s'assoit sur un siège libre et monte ; là-haut, il choisit une piste qui part à moins de 80 m. Si la piste finit loin de toute remontée, il continue sur une autre piste qui passe à moins de 100 m.
- Sur un siège, ils sont assis comme B.J., leur matériel aux pieds ; à deux par siège au plus.
- Ils apparaissent un par un (un toutes les demi-secondes), sur une piste au hasard, jamais à moins de 200 m de B.J.
- Ce sont des véhicules avec leur pilote : leur rentrer dedans à plus de 40 km/h les fait tomber, comme B.J. ; on peut leur prendre leurs skis (E), et une balle les touche. Tombé, le skieur devient un piéton, et un autre skieur le remplace ailleurs.
- Mesuré après 6 minutes : 15 sur les pistes, 12 sur les remontées, 3 en route vers un départ, aucun bloqué. B.J. prend les skis de l'un d'eux (il repart à pied, avec son bonnet), en fait tomber un autre d'une balle, rentre dans un troisième à 60 km/h (les deux tombent, 10 points de vie en moins) : 30 s plus tard, ils sont de nouveau 30.

### Les villes

| Ville | Où | Ce qu'on y trouve |
| --- | --- | --- |
| Los Santos | Sud | Vinewood et son musée d'art, le centre (tours, gratte-ciel Maze Bank, banque, grande banque Pacific Standard, commissariat), la bijouterie Vangelico, Vespucci et sa plage, la villa de Michael, l'hôpital, l'armurerie, LS Customs, le fleuve et ses deux ponts, l'aéroport, ses hangars, ses avions et ses hélicoptères, le port avec ses conteneurs et ses grues ; les gangs Families, Ballas et Vagos au sud |
| Paleto Bay | Nord | Maisons, supérette, hôpital, armurerie, station-service, garage LS Customs |
| Grapeseed | Nord-est | Deux fermes et une supérette au milieu des champs |
| Sandy Shores | Au sud de l'Alamo Sea | Caravane de Trevor, bar Yellow Jack, supérette, hôpital, commissariat, armurerie, aérodrome avec un avion, le gang Lost MC |
| Harmony | Désert | Station-service et supérette |
| Chumash | Côte ouest | Maisons et supérette |
| Fort Zancudo | Côte ouest | Le bunker nazi, une caserne, un hangar avec un avion et une piste |
| Mont Chiliad | Nord | Le château Wolfenstein, au bout d'une route de montagne |
| Station de ski | Est, au pied du mont Gordo | Le télésiège du mont Gordo, la télécabine des Marmottes, un chalet, des skis, des snowboards et des luges, l'arrivée de trois pistes |

Deux stations-service isolées bordent les grandes routes, et la maison de Franklin domine Los Santos dans les collines de Vinewood.

### Les routes

- **En ville**, les rues longent chaque pâté, avec trottoirs de 20 cm, lampadaires tous les 18 m (une voiture lancée les renverse) et passages piétons à chaque carrefour. Une rue qui traverse l'eau (`+`) est un pont avec des garde-fous.
- **Dos d'âne** : une rue de ville sur 8 environ (`dosDAne`, 0,12) a un dos d'âne en son milieu, jamais sur un pont : 86 en tout. C'est une bosse arrondie de 12 cm (`hauteurDosDAne`) sur 4 m, peinte de bandes jaunes et noires en biais, sur toute la largeur de la rue. Les voitures qui circulent ralentissent à 18 km/h en passant dessus (pas la police). Voir « Conduite » pour ce qu'il fait à la voiture de B.J.
- **À la campagne**, les cases `=` et `#` qui se touchent (même en diagonale) forment des routes de 10 m de large, arrondies dans les virages. Le bout d'une route se branche sur le coin de pâté le plus proche, dans son prolongement. Les grandes routes :
  - la **Great Ocean Highway**, qui longe la côte ouest de Los Santos à Paleto Bay, avec deux ponts ;
  - la **Senora Freeway**, qui monte de Los Santos à Sandy Shores, puis à Grapeseed et Paleto Bay par la côte nord ;
  - la **Route 68**, qui traverse le pays d'ouest en est, par Harmony ;
  - la route des collines de Vinewood, de Los Santos à la Route 68 ;
  - la route du château, qui grimpe de Grapeseed au sommet du Chiliad ;
  - une case de route, qui relie la Senora Freeway à la station de ski, au pied du mont Gordo.
- Une route monte et descend en douceur : sa hauteur est lissée le long de son tracé, et le terrain est creusé ou remblayé sur 7 m de chaque côté, puis rejoint le reste en 13 m. La route du château reste raide : environ 30 %.
- **Ponts** : une route au-dessus de l'eau reste au moins 3,5 m au-dessus de la surface, pour que les bateaux passent dessous. Le tablier fait 1,2 m d'épaisseur, avec deux rambardes et un pilier tous les 3 points de la route. Les rambardes ne retiennent pas : on peut tomber à l'eau.
- **Pontons** : une jetée de planches de 36 m part de la plage vers le large, 50 cm au-dessus de l'eau. Il y en a 5 : Vespucci, Paleto Bay, Sandy Shores (sur l'Alamo Sea), le port de Los Santos et Chumash.

### Les pistes de cascades

Deux pistes pour faire le fou en voiture, inspirées du jeu *Stunts* (1990). Elles sont décrites dans le tableau `CASCADES` : une case de départ, une direction, puis des morceaux posés bout à bout. Une piste fait 9 m de large, en goudron avec des bordures rouges et blanches. Toute la piste est à une seule hauteur, celle du terrain en moyenne ; le terrain est mis à plat dessous sur 7,5 m de chaque côté du milieu, puis rejoint le reste en 15 m. Il n'y pousse ni arbre ni rocher. Une voiture attend à côté du départ.

| Piste | Où | Départ | Morceaux, dans l'ordre | Voiture |
| --- | --- | --- | --- | --- |
| Stunt Park de Palomino | À l'est de Los Santos, au sud du réservoir | Colonne 32, ligne 49, vers l'est | Tremplin (2,5 m, trou de 16 m), looping, 4 bosses, virage relevé de 180°, tire-bouchon, pont de 5 m, tremplin (3 m, trou de 22 m) | Porsche |
| Sauts de Grand Senora | Dans le désert, à l'est de Harmony | Colonne 27, ligne 30, vers l'est | Tremplins de 3 et 4 m (trous de 25 et 35 m), pont de 6 m, tremplin de 5 m (trou de 45 m) | Classique |

| Morceau | Forme | Réglages (et leur valeur si on n'en met pas) |
| --- | --- | --- |
| `droit` | Une ligne droite, par terre | `longueur` (30 m) |
| `virage` | Un arc de cercle. Relevé, il penche vers l'intérieur : le bord extérieur monte à 4,5 m pour 30°. Il se relève sur le premier quart et redevient plat sur le dernier | `sens` (`'gauche'` ou `'droite'`), `angle` (90°), `rayon` (25 m), `releve` (0°) |
| `tremplin` | Une rampe à 30 % jusqu'à la hauteur, un trou, puis une rampe à 20 % pour retomber. Avec `saut: 0`, la rampe s'arrête dans le vide | `hauteur` (3 m), `saut` (20 m) |
| `looping` | Un cercle debout. La sortie est décalée de 11 m à droite de l'entrée | `rayon` (9 m) |
| `tire-bouchon` | La piste fait un tour complet sur elle-même en avançant : au milieu, à deux rayons de haut, on roule la tête en bas | `longueur` (40 m), `rayon` (5 m) |
| `pont` | Une rampe à 25 %, un pont sur des piliers, une rampe pour redescendre | `hauteur` (5 m), `longueur` (30 m) |
| `bosses` | Des bosses de 10 m de long, qui font décoller à grande vitesse | `nombre` (4), `hauteur` (1,2 m) |

- **Rampes pleines** : les rampes, les bosses et les virages relevés sont en béton jusqu'au sol. On bute contre leurs côtés et contre le bout d'un tremplin, on ne passe pas au travers. Là où le bord est à plus de 1 m du sol, deux rambardes retiennent la voiture. Sous un pont, on passe entre les piliers.
- **Vitesse** : le premier tremplin de Palomino se saute entre 60 et 80 km/h environ ; plus vite, on dépasse la rampe d'arrivée et on retombe par terre. Le looping demande au moins 76 km/h en bas, le tire-bouchon environ 60 km/h (voir « Conduite »).
- Sur la mini-carte et la grande carte, les pistes sont des traits orange, et un rond « C » orange marque leur départ, avec leur nom.

### Les bâtiments où l'on entre

Un bâtiment visitable a des murs de 30 cm, une porte, un sol, des lampes au plafond et des meubles. Ceux qui ont des étages ont un escalier au fond à gauche : une volée par étage, qui va à droite puis revient à gauche, avec un trou dans le plancher au-dessus.

| Lettre | Bâtiment | Étages visitables | Ce qu'il y a dedans |
| --- | --- | --- | --- |
| `A` | Armurerie | Rez-de-chaussée | Comptoir, armes au mur, les 5 stands d'armes, le stand du masque à gaz, 1 gilet pare-balles |
| `H` | Hôpital | Hall (4 étages pleins au-dessus) | Accueil, chaises, lits, 2 trousses de soin. On se réveille devant la porte |
| `C` | Commissariat | 2 étages et le toit | Accueil, bancs, 3 cellules à barreaux ; bureaux et 1 gilet en haut ; 2 voitures de police garées devant |
| `S` | Supérette 24/7 | Rez-de-chaussée | Rayons, frigos, caisse, 1 trousse de soin, 1 voiture garée |
| `G` | Garage LS Customs | Un grand atelier de 5,5 m de haut | Pont élévateur, pneus, établi, 1 voiture, le garagiste (combinaison bleue, casquette rouge) qui blinde les voitures. On y entre en voiture par une porte de 11 m |
| `K` | Banque | Hall de 5 m de haut | Colonnes, guichets, coffre-fort ouvert avec des lingots et 2 000 $ (voir « Argent ») |
| `Z` | Gratte-ciel Maze Bank | Hall, et le toit à 141 m | Accueil, ascenseur jusqu'au toit, hélistation, antenne, garde-fou |
| `E` | Station-service | Petite boutique | Rayon, frigos, caisse, 1 trousse de soin ; pompes sous un auvent |
| `L` | Maison de Franklin | 2 étages et le toit | Salon (canapé, télé), cuisine, chambre en haut, 1 voiture |
| `O` | Villa de Michael | 2 étages et le toit | Comme chez Franklin, en plus grand ; piscine (on ne nage pas dedans), palmiers, une Porsche |
| `R` | Caravane de Trevor | Une pièce | Lit, table, cartons ; dehors, un vieux canapé, des fûts et un 4x4 |
| `J` | Bar Yellow Jack | Rez-de-chaussée | Bar, bouteilles, tabourets, billard, tables, 1 tricycle devant |
| `F` | Ferme | Grange et grenier | Bottes de paille ; silo dehors ; 1 4x4 |
| `D` | Docks | Entrepôt (une fois sur deux) | Conteneurs dedans et dehors, empilés jusqu'à 3 ; ou un parc à conteneurs avec une grue à portique |
| `N` | Hangar d'avions | Un hangar de 10 m de haut | Un avion à piloter, le nez vers la porte de 32 m |
| `B` | Bunker nazi | Le bunker, par l'ouest | Voir ci-dessous |
| `W` | Château Wolfenstein | Le donjon : 4 étages de 4 m et le toit crénelé | Trône, grande table ; 2 trousses de soin (au 2e étage et sur le toit) |
| `U` | Musée d'art de Los Santos | Une grande salle de 6 m de haut | Portique à 6 colonnes et fronton, sol en marbre, le grand tableau derrière un cordon rouge, la couronne, 2 vitrines de bijoux, 2 statues, 4 autres tableaux, des bancs ; 4 vigiles et 2 chiens |
| `V` | Bijouterie Vangelico | Une boutique de 3,6 m de haut | Façade noire et or, murs en bois, 8 vitrines de bijoux, le gros diamant sur une colonne noire ; 1 vigile devant la porte |
| `Q` | Banque Pacific Standard | Un hall de 6 m de haut (4 étages pleins au-dessus) | Portique à piliers, guichets, colonnes de marbre ; au fond, le couloir des lasers, la porte ronde du coffre-fort, la grille et le pactole ; 3 vigiles |

- **Bunker** (`B`) : enceinte de 4 m avec une seule entrée à l'ouest, sacs de sable. Le bunker lui-même s'ouvre aussi à l'ouest : dedans, le Kommandant, 2 soldats, des caisses, une table et un fusil d'assaut. Dehors, 6 soldats, 2 trousses de soin et 1 gilet.
- **Château** (`W`) : remparts crénelés de 7 m avec une grande porte au sud, 4 tours à toit pointu, bannières rouges. Hitler et 8 soldats gardent la cour. Dans la cour aussi : 2 trousses, 1 mitraillette, 1 gilet.
- Les tours, les maisons et 4 immeubles sur 5 sont pleins : on ne peut pas y entrer. Un immeuble plein a une porte fermée (un panneau sombre) sur la rue.

#### Les immeubles où l'on entre

Dans les pâtés `I`, un immeuble sur 5 environ (`immeublesVisitables`, 0,2) se visite : 104 sur la carte. Sa porte (1,8 m de large) donne sur la rue la plus proche, au nord ou au sud du pâté. Dedans, l'escalier monte au fond à gauche, comme dans les autres bâtiments, et chaque étage est meublé (voir plus bas). Un immeuble visitable a au plus 6 étages : s'il devait en avoir plus, il est ramené à 6. Il y en a de 5 sortes, tirées au hasard, toujours les mêmes d'une partie à l'autre :

| Sorte | Nombre | Comment on arrive en haut |
| --- | --- | --- |
| Escalier jusqu'au toit | 33 | L'escalier intérieur monte jusqu'au toit, qui a un garde-fou de 1,1 m |
| Échelle | 13 | L'escalier s'arrête au dernier étage. Une échelle en métal monte le long du mur de côté, du trottoir jusqu'à 1 m au-dessus du garde-fou |
| Escalier de secours | 23 | L'escalier s'arrête au dernier étage. Dehors, contre le mur de côté, un escalier en métal monte en zigzag (deux volées côte à côte, un palier à chaque étage) jusqu'en haut du garde-fou ; dedans, une marche de 55 cm aide à passer du toit au garde-fou |
| Terrasse, par l'intérieur | 16 | Le bas prend tout le pâté, sur 2 étages de moins ; l'escalier intérieur arrive sur son toit, la terrasse. Un haut plus petit (la moitié côté porte, 30 cm en retrait des bords) est posé dessus, avec sa porte sur la terrasse et son propre escalier, jusqu'à son toit une fois sur deux |
| Terrasse, par dehors | 19 | Pareil, mais on monte sur la terrasse par un escalier de secours dehors |

- Les échelles et les escaliers de secours sont sur le côté du bâtiment qui donne sur une rue, jamais entre deux immeubles.
- **Grimper à l'échelle** : en bas, on avance vers le mur, à moins de 70 cm de l'échelle : B.J. l'attrape, face au mur. En avançant vers le mur, il monte à 2,5 m/s ; en s'en éloignant, il descend. En haut, il passe par-dessus le garde-fou et se retrouve sur le toit. Pour redescendre, on avance vers le bord du toit, juste au-dessus de l'échelle. Espace fait lâcher prise (on ne se fait pas mal en tombant). Au pied d'une échelle, l'aide dit « Avance contre l'échelle pour grimper ».

**Les étages**, tirés au hasard un par un (toujours les mêmes d'une partie à l'autre), ont du parquet et sont de 3 sortes :

| Sorte | Combien (sur 503 étages) | Ce qu'il y a dedans |
| --- | --- | --- |
| Appartement | 266 (seulement dans les immeubles profonds, la moitié des étages) | Derrière des cloisons, à gauche du couloir : une salle de bain (carrelage bleu clair au sol et en bas des murs, sauf devant la porte, baignoire pleine d'eau, toilettes, lavabo et miroir, machine à laver) et une chambre (lit double avec couette, oreillers et deux tables de nuit à lampe, mur de couleur et tableau au-dessus du lit, armoire, commode et miroir, tapis, bureau avec un ordinateur). De l'autre côté : un salon (télé allumée sur son meuble, contre un mur de couleur, avec un tableau au-dessus ; canapé en face, table basse, tapis, lampadaire, plante, bibliothèque) et, au fond, la cuisine le long du mur (placards, plan de travail, évier, plaques, placards du haut, frigo) avec une table à manger et 4 chaises |
| Loft | 121 | La même chose, sans cloisons ni salle de bain : le lit à gauche, le salon et la cuisine à droite |
| Bureaux | 116 | Des rangées de bureaux (un écran allumé, une chaise), des armoires à dossiers, une fontaine à eau, des plantes, 4 lampes au plafond |

- **Le chemin reste libre** : de la porte, un couloir de 2,6 m va tout droit jusqu'au fond, puis un passage de 1,6 m longe l'escalier vers la gauche. Les cloisons s'arrêtent au plafond ; les portes sont des passages de 1 m à 1,2 m, sans porte.
- **Les grands immeubles** (45 m de large) ont en plus, de chaque côté, une cloison avec un passage : à gauche une chambre d'enfant (un lit, un bureau, une bibliothèque, des cubes de jouets), à droite une salle de jeux (un billard, deux bornes d'arcade allumées, un canapé rouge et une télé).
- Dans le haut plus étroit d'une terrasse (10 m de profondeur), il n'y a que des lofts et des bureaux.
- Les meubles se montent comme des marches s'ils font moins de 60 cm (un lit, une chaise, une table basse) ; les plus hauts arrêtent B.J. Les tableaux, les tapis, les lampes et les placards du haut ne gênent pas.

#### Les objets à voler et les bonus

Sur certains meubles d'un étage sur deux environ (une table de nuit, la commode, le lavabo, la table basse, le plan de travail, la table à manger, un bureau), un objet attend, qui tourne et flotte comme les autres objets du jeu, au-dessus d'un anneau de couleur. On le prend en passant dessus. Il y en a 418 (un étage sur deux en a un, un sur huit en a deux), toujours aux mêmes endroits.

- **Les objets de valeur** (anneau violet, deux tiers des objets) : le tableau `TRESORS`, en haut de `index.html`, dit leur nom, leur forme et ce qu'ils rapportent. On les voit deux fois plus grands que nature.

| Objet | Prix | Objet | Prix |
| --- | --- | --- | --- |
| Collier de perles | 250 $ | Liasse de billets | 300 $ |
| Montre en or | 400 $ | Console de jeux | 200 $ |
| Bague en diamant | 600 $ | Ordinateur portable | 350 $ |
| Gros diamant | 1 000 $ | Téléphone | 150 $ |
| Lingot d'or | 1 500 $ | | |

  « Montre en or volé ! +400 $ » s'affiche. Voler sous les yeux de la police (un policier à moins de 50 m qui voit B.J., ou une voiture de police) donne une étoile ; sinon, personne ne dit rien.
- **Les bonus** (anneau turquoise, sauf la trousse et le gilet, qui gardent leur couleur) : une trousse de soin (+50 vie), un gilet pare-balles, une caisse de munitions (la moitié d'un chargeur d'achat pour chaque arme à feu qu'on a, sauf le bazooka : « + munitions pour tes armes » ; on ne la prend pas sans arme à feu), une boisson énergisante (une canette verte : on court plus vite pendant 30 s) et un pot-de-vin (une enveloppe pleine de billets : une étoile de moins ; on ne le prend pas sans étoile). Comme les trousses, on ne prend pas un bonus qui ne sert à rien.
- **Ils reviennent** : un objet pris revient à sa place au bout de 10 minutes (`retourTresors`, 600 s).

Un étage fait 3 m, sauf mention contraire. Les trousses de soin et les gilets pare-balles réapparaissent 60 s après avoir été ramassés.

### Le ciel et la vue

- Ciel réaliste avec des nuages qui avancent lentement, un soleil fixe et des ombres autour du joueur.
- Le brouillard commence à 180 m et cache tout au-delà de 900 m (`distanceVue`). Le pays est découpé en morceaux de 8 × 8 cases : seuls ceux qui ne sont pas cachés par le brouillard sont dessinés.
- Les vitres des immeubles reflètent le ciel ; les murs, les pavés et les tuiles ont du relief.
- Tout autour de l'île, la mer s'étend jusqu'à l'horizon. On ne peut pas s'éloigner à plus de 30 m du bord de la carte.

### La population

Seuls les environs du joueur sont vivants. Piétons et voitures apparaissent hors de sa vue et disparaissent quand il s'éloigne. Leur nombre se choisit dans le menu (voir « La foule », plus bas).

| | Piétons | Voitures en circulation |
| --- | --- | --- |
| Nombre (choix du menu) | 15, 30, **60** ou 120 | 8, 16, **32** ou 60 |
| Apparaissent entre | 45 et 170 m | 60 et 230 m |
| Disparaissent au-delà de | 200 m (60 m derrière B.J. qui roule vite) | 280 m (120 m derrière B.J. qui roule vite) |
| Vitesse | 1,4 m/s | 11 m/s (40 km/h) |

- **La foule** : dans le menu, une ligne de boutons pour les piétons et une pour les voitures en circulation : Peu, Normal, Beaucoup ou Énorme (en gras dans le tableau : Beaucoup, le choix au tout premier lancement). Les nombres sont dans le tableau `FOULES`, tout en haut du fichier. Le jeu en tient compte tout de suite, même dans le menu de pause, et le navigateur s'en souvient pour la prochaine fois. Toutes les demi-secondes, il en apparaît jusqu'à un huitième du nombre choisi (15 piétons et 8 voitures pour Énorme) : la ville se remplit en quelques secondes, sans tout faire apparaître d'un coup, ce qui ferait sauter l'image. Les voitures de police et les voitures garées ne comptent pas.
- **En roulant vite** (plus de 10 m/s, soit 36 km/h, plus vite qu'en courant), ce qui est derrière B.J. ne sert à rien, puisqu'il s'en éloigne : les piétons et les voitures en circulation n'apparaissent plus que devant lui, et ceux qu'il a laissés derrière disparaissent dès 60 m (piétons) et 120 m (voitures). Sinon, en voiture, la foule restait derrière lui et la rue devant était vide. Avec Énorme, à 90 km/h en ville, il y a ainsi en moyenne 38 piétons devant B.J. (à moins de 150 m) et 23 voitures (à moins de 250 m), autant qu'à l'arrêt ; sans cela, il n'y en avait que 5 et 8. La police n'est pas concernée.
- **Piétons** : ils ne vivent qu'en ville. Ils vont de coin en coin sur les trottoirs et traversent aux passages piétons (30 % de chances à chaque coin). Ils s'enfuient pendant 8 s si on tire à moins de 40 m ou si on les frappe. Ils n'ont pas tous la même taille (10 % de moins à 6 % de plus que B.J.), ni la même carrure. 4 sur 10 ont les cheveux longs, la moitié des manches courtes, 1 sur 4 un short.
- **Voitures** : elles roulent sur la voie de droite, en ville comme sur les routes de campagne, et choisissent leur direction à chaque carrefour (60 % tout droit). Elles ne prennent pas une rue où une voiture est arrêtée, si elles peuvent passer par une autre : c'est un bouchon. Dans un cul-de-sac, elles font demi-tour. Elles regardent là où elles vont, s'arrêtent devant un obstacle, et font demi-tour après 5 s bloquées. Dans un carrefour, deux voitures qui se bloquent l'une l'autre en se croisant ne s'attendent pas : celle qui a la priorité (tirée au sort) passe d'abord. Avec la foule Énorme, B.J. immobile en ville pendant 3 min, il y a en moyenne moins d'une voiture arrêtée sur 60 (0,3 à 0,5 selon les essais), et au plus 2 à 4 à la file ; elles roulent en moyenne à 36 km/h. Avant, les bouchons ne se défaisaient pas : 18 voitures arrêtées en moyenne, jusqu'à 39 dans le même bouchon, 25 km/h de moyenne. Dans une rue fermée par deux voitures garées, 2 voitures attendent devant en moyenne (12 avant, en un bouchon de 25). Le type de chaque voiture est tiré au sort (voir « Véhicules »).
- **Voitures garées** : il y en a devant les maisons, les places, les magasins et dans les garages, prêtes à être volées. Leur type est tiré au sort de la même façon, sauf chez Michael (une Porsche), Franklin (une classique), Trevor (un 4x4), à la ferme (un 4x4), au Yellow Jack (un tricycle) et au commissariat (2 voitures de police).
- Personne d'autre que B.J. ne va dans l'eau profonde : les piétons et les ennemis font demi-tour au bord.

### Les gangs

Quatre gangs traînent dans leur quartier, un pâté de maisons chacun (tableau `GANGS`, en haut de `index.html`). Sur la mini-carte et la grande carte, leur quartier est colorié de leur couleur, et la légende les nomme (« Gang Ballas »).

| Gang | Couleur | Où | Membres | Arme |
| --- | --- | --- | --- | --- |
| Families | vert vif | Sud de Los Santos (colonne 18, ligne 55) | 5 | Pistolet |
| Ballas | violet | Sud de Los Santos (22, 56) | 5 | Mitraillette, en rafales |
| Vagos | jaune | Est du fleuve, à Los Santos (30, 54) | 5 | Pistolet |
| Lost MC | noir | Sandy Shores, près de la supérette (33, 24) | 4 | Fusil à pompe |

- **Tant qu'on les laisse tranquilles**, ils restent en rond au milieu de leur pâté, entre les maisons, et se font face. Un membre de gang porte un maillot et une casquette de la couleur de son gang.
- **Ils attaquent** si on en frappe, en blesse ou en renverse un, si on tire à moins de 50 m d'eux, ou si l'un d'eux voit B.J. à moins de 15 m avec une arme à feu à la main (pas en voiture). Alors tout le gang attaque, comme des policiers : 70 points de vie (2 balles de pistolet), 6 dégâts par balle (`ENNEMIS.gang.degats`), le double au fusil à pompe de près. Ils ne quittent pas leur pâté.
- **Ils se calment** quand B.J. est à plus de 100 m, ou quand il meurt.
- **Un membre tué** lâche son arme et 20 à 99 $. Ça ne donne pas d'étoile : la police ne s'en mêle pas.
- **Ils reviennent** : quand B.J. est à plus de 250 m de leur quartier, un gang qui a perdu des membres revient au complet.

## Combat et armes

Il y a 8 armes, dont 2 au départ (poings et couteau), et une 9e qu'on n'a qu'avec un code de triche : les yeux laser. Le pistolet, la mitraillette, le fusil à pompe et le fusil d'assaut s'achètent à l'armurerie ou se ramassent sur les ennemis. Le fusil de sniper s'achète seulement à l'armurerie : aucun ennemi ne le lâche. Le bazooka ne s'achète pas : c'est Hitler qui le lâche. Un tir à la tête fait 2,5 fois plus de dégâts.

### Les armes

| Arme | Dégâts par coup | Coups par seconde | Portée | Prix | Munitions achetées | Particularité |
| --- | --- | --- | --- | --- | --- | --- |
| Poings | 15 | 2,2 | 2 m | départ | illimitées | Repousse la cible de 50 cm |
| Couteau | 50 | 2 | 2,3 m | départ | illimitées | Repousse la cible de 50 cm |
| Pistolet | 40 | 3,3 | 90 m | 200 $ | 36 | Un clic par tir |
| Mitraillette | 22 | 12,5 | 60 m | 800 $ | 150 | Automatique, peu précise |
| Fusil à pompe | 8 plombs × 20 | 1,1 | 30 m | 1 200 $ | 30 | Très dispersé |
| Fusil d'assaut | 34 | 8,3 | 130 m | 2 000 $ | 120 | Automatique, précis |
| Bazooka | 250 au centre | 0,67 | 150 m | lâché par Hitler | 10 roquettes | Explose dans un rayon de 6 m |
| Fusil de sniper | 150 | 0,67 | 250 m | 2 500 $ | 20 | Un clic par tir, lunette qui grossit 5 fois |
| Yeux laser | 40 | 15 | 200 m | codes `SUPERMAN` et `DIEU` | illimitées | Automatique : deux rayons rouges qui partent des yeux |

- Racheter une arme déjà possédée coûte moitié prix et ne donne que des munitions.
- Une arme ramassée donne la moitié des munitions ; si on l'a déjà, le quart.
- Les coups de poing et de couteau touchent l'ennemi le plus proche devant soi, jusqu'à 50° de côté.
- La dispersion est divisée par 2 en visant et doublée en courant.
- Renverser quelqu'un avec une voiture à plus de 14 km/h fait 200 dégâts.
- **Pneus** : une balle dans un pneu le crève (pas sur une voiture blindée). À plus de 50 km/h, la voiture part en tête-à-queue : de quoi arrêter une voiture de police (voir « Accidents »).
- **Fusil de sniper** : une balle suffit pour un piéton, un policier ou un soldat. Il en faut 3 pour le Kommandant (2 à la tête) et 6 pour Hitler (3 à la tête). Dans la lunette, la balle s'écarte d'au plus 13 cm à 200 m ; sans viser, d'au plus 37 cm à 50 m. Un nazi touché de loin est alerté, mais il ne tire que s'il voit B.J. à moins de 45 m : on peut l'abattre sans risque, par l'entrée du bunker ou la porte du château.
- **Yeux laser** (touche 9) : on ne les a que tant qu'un code de triche qui les donne est allumé (`SUPERMAN`, `DIEU` : ceux qui ont `laser: true`). Ils ne s'achètent pas, ne se ramassent pas, et `IDKFA` ne les donne pas. Tant qu'on garde le clic gauche enfoncé, deux rayons rouges vont des yeux de B.J. au point visé, avec un grésillement et des étincelles là où ils touchent. Chaque tir (15 par seconde) compte comme une balle de pistolet, sans jamais manquer de munitions : ça fait fuir les piétons, alerte les ennemis et donne des étoiles comme une arme à feu. Mesuré : un policier meurt en 2 tirs (moins d'un dixième de seconde), un soldat en 3, le Kommandant en 0,7 s, Hitler en 1,5 s ; une voiture classique prend feu au bout de 4 s de rayons sur le même côté, et explose 5 s plus tard. B.J. n'a rien à la main : ses bras bougent comme sans arme, et les vigiles et les gangs ne le prennent pas pour un homme armé. En 1re personne, les rayons partent du bas de l'image et se rejoignent sur le viseur.
- **Bazooka** : la roquette part du canon vers le viseur et vole tout droit à 25 m/s (90 km/h, `vitesseRoquette`), plus vite que B.J. qui court (8 m/s). Elle explose sur le premier mur ou voiture qu'elle touche, si elle passe à moins de 1 m du milieu du corps d'un personnage, par terre si on vise le sol, ou au bout de 150 m. Les dégâts baissent avec la distance à l'explosion, jusqu'à 0 à 6 m ; il n'y a pas de bonus à la tête. L'explosion blesse aussi B.J. s'il est trop près (jusqu'à 40 points s'il est collé) et fait exploser les voitures à moins de 6 m. Un personnage tué par une explosion compte comme s'il avait été abattu : un piéton ou un policier donne une étoile.

### Les impacts de balles

Chaque balle laisse une trace là où elle finit : celles de B.J. comme celles des ennemis.

- **Sur les murs** (et les planchers, les plafonds, les meubles : tout ce qui est construit) : un trou noir entouré de plâtre arraché, clair, avec quelques fissures, de 11 à 19 cm de large, et une petite bouffée de poussière. Il en reste 300 (`impactsMurs`) : au-delà, le plus vieux s'efface. Pas d'impact sur le sol dehors (rues, trottoirs, herbe), ni sur les arbres, les lampadaires, les personnages et le heavy robot.
- **Sur les voitures** : un trou noir de 3 cm, entouré de métal nu là où la peinture est partie, et deux étincelles. Il en reste 20 par voiture (`impactsVoiture`). Le trou est collé à la tôle : il suit la voiture, s'enfonce avec la tôle quand elle se cabosse, et part avec le pare-chocs ou le rétroviseur qui tombe. Pas de trou dans une vitre (elle se fêle), un pneu (il crève), un blindage (des étincelles seulement) ni des skis. Les trous s'effacent quand la voiture explose, ou quand le garage la répare. Les bateaux, les avions et les hélicoptères en prennent aussi.
- **Les balles des ennemis** : une balle arrêtée par un mur y laisse son impact. Une balle ratée ne s'arrête plus en l'air à côté de B.J. : elle continue tout droit, 60 m au plus, et laisse son impact là où elle finit (le mur derrière lui, le plancher). Quand B.J. est en voiture, la balle s'arrête dans la tôle, touchée ou ratée, et y fait un trou. Mesuré : 6 soldats à 14 m, B.J. à 2 m devant une façade, pendant 30 s : 83 impacts, tous sur la façade ; B.J. en voiture, 6 soldats à 14 m, pendant 25 s : 17 à 20 trous.
- **Les yeux laser** (codes `SUPERMAN` et `DIEU`) laissent sur les murs une marque noire de brûlé, sans plâtre clair, et sur les voitures les mêmes trous que les balles.
- Le réglage `tailleImpacts` grossit tous les impacts (1 : normal, 3 : énormes).

### Les personnages

| Type | Vie | Arme | Coups de pistolet pour tuer | Ce qu'il lâche |
| --- | --- | --- | --- | --- |
| Piéton | 50 | aucune | 2 | 10 à 69 $ (6 fois sur 10) |
| Policier | 70 | pistolet | 2 | Un pistolet |
| Soldat nazi | 90 | fusil d'assaut | 3 | Une mitraillette ou un fusil d'assaut |
| Kommandant | 450 | fusil à pompe | 12 (5 à la tête) | Un fusil à pompe et 1 000 $ |
| Hitler (boss final) | 900 | bazooka | 23 (9 à la tête) | Le bazooka et 2 000 $ |
| Vigile (braquages) | 100 | pistolet, fusil à pompe, mitraillette ou fusil d'assaut | 3 | Son arme |
| Chien de garde | 45 | ses crocs | 2 | Rien |
| Policier d'élite (4 étoiles) | 140 | fusil d'assaut | 4 | Un fusil d'assaut |
| Membre de gang | 70 | celle de son gang (tableau `GANGS`) | 2 | Son arme et 20 à 99 $ |

Leur vie et leur arme sont dans le tableau `ENNEMIS`. Les corps disparaissent au bout de 15 s. Le chien est un berger allemand, fauve au dos noir, oreilles dressées ; mort, il tombe sur le côté. Le policier d'élite porte un casque, une tenue noire et un gilet pare-balles.

Un personnage a un visage (yeux, sourcils, bouche, nez, oreilles), des coudes et des genoux. Ses genoux se plient quand il marche, quand il s'accroupit et quand il s'assoit sur un tricycle ou une moto. Plus il va vite, plus ses coudes sont pliés et plus il se penche en avant.

**Coups, chutes et morts** :

- **Des membres qui ont du poids** : quand un personnage ne se tient plus (tué, renversé, soufflé, bousculé ; B.J. en l'air ou en roulade), son buste, sa tête, ses bras et ses jambes sont comme des pendules. Ils traînent derrière quand le corps tourne, continuent quand il s'arrête d'un coup, pendent vers le sol, claquent par terre et y restent. Ses muscles les ramènent vers sa pose avec une force, la `raideur` : 0 ou presque pour un mort (tout mou), 9 pour un vivant qui vole (il se débat), 25 pour B.J. qui saute. Les articulations ont des limites : un genou ou un coude ne plie pas à l'envers, la tête et le buste ne partent pas trop loin. Ni les mains, ni les pieds, ni la tête ne passent sous le sol.
- **Touché sans être tué** (une balle, un coup de poing ou de couteau), il encaisse : le buste et la tête partent en arrière pendant 0,3 s. La tête et les bras suivent avec un temps de retard (la tête part jusqu'à 40° en arrière), puis tout revient en place en une demi-seconde.
- **Tué**, il s'effondre en 0,8 s : ses genoux lâchent d'abord (le bassin descend de 30 cm), puis il bascule, de plus en plus vite, à la renverse si B.J. était devant lui, sur le ventre s'il était derrière. Ses muscles lâchent en même temps : ses bras pendent, traînent derrière lui pendant la chute et retombent où ils peuvent, sa tête ballotte. Il finit à plat, sur le dos ou sur le ventre, les bras et les jambes là où ils sont tombés : le long du corps, écartés, au-dessus de la tête, un genou plié... Au bout de 3 s, il ne bouge plus. Le chien, lui, tombe sur le côté, comme avant.
- **Renversé par une voiture** (celle de B.J., ou une voiture en accident), il vole devant elle, un peu plus vite qu'elle (× 1,1) et vers le haut (2 m/s + le quart de sa vitesse), en tournant tête en arrière (les jambes fauchées partent devant) et un peu de côté (jusqu'au quart de cette vitesse), les membres qui battent et traînent : vivant, il se débat ; mort, il est tout mou. Il retombe, rebondit un peu (30 %), roule et glisse (il perd 90 % de sa vitesse chaque seconde au sol), puis se couche à plat, sur le dos ou sur le ventre selon comment il est tombé. Il perd 10 points de vie par m/s au-delà de 2 m/s (`degatsRenverse`) : un piéton (50 points) survit sous 25 km/h, et se relève. Mesuré : à 15 km/h, son bassin monte à 1,1 m du sol, il retombe à 2 m et se relève en 1,1 s ; à 60 km/h, son bassin monte à 1,75 m et il retombe mort à 25 m. Un chien renversé meurt toujours, sans voler.
- **Soufflé par une explosion**, il est projeté loin d'elle et à la renverse : jusqu'à 12 m/s de côté et 9 m/s vers le haut, moins s'il était loin. Mesuré : trois soldats à 2, 4 et 6 m d'une explosion retombent à 11 à 19 m ; le plus proche est tué, les deux autres se relèvent.
- **Bousculé par B.J.** : en marchant, B.J. pousse les passants de son chemin, et ils vacillent. En courant (plus de 6 m/s), il les renverse : ils tombent à la renverse (3,5 m/s), sans se faire mal, puis se relèvent. C'est comme un coup sans dégâts : un piéton s'enfuit, un policier donne une étoile (s'il n'y en avait pas), un vigile déclenche l'alarme, un membre de gang fait attaquer tout son gang. B.J. ne renverse ni le Kommandant ni Hitler.
- **Se relever** : couché mais vivant, il se relève en 1,1 s, en pliant les genoux, ses membres encore mous reprenant des forces, puis repart (un piéton en courant : il a eu peur).

### Le joueur

- **Vie** : 100 points. Elle remonte de 8 points par seconde après 5 s sans être touché, soit de 0 à 100 en 12,5 s. Une trousse de soin rend 50 points. Tomber de haut en fait perdre (voir « Sauter, tomber, rouler »).
- **Boisson énergisante** (un bonus des immeubles) : pendant 30 s (`dureeEnergie`), B.J. va 40 % plus vite à pied et à la nage (`vitesseEnergie`, 1,4) : 11,2 m/s en courant.
- **Masque à gaz** : il s'achète 500 $ à l'armurerie (`prixMasque`), une fois pour toutes. B.J. le met tout seul dans la fumée toxique de la bijouterie, qui ne lui fait alors plus rien. On le voit sur son visage : du caoutchouc noir, deux hublots, une cartouche filtrante.
- **Gilet pare-balles** : 100 points de protection (`giletMax`), qui prennent les dégâts à la place de la vie. Il ne se recharge pas tout seul : il faut ramasser un autre gilet. Il y en a 7 : dans les 3 armureries, au premier étage des 2 commissariats, dans le bunker (près de l'entrée) et dans le château (près de la porte). Quand B.J. en porte un, on le voit sur son torse, en bleu foncé.
- **Quand il est touché** : l'écran rougit sur les bords et un son grave retentit.

### Les ennemis

Un ennemi ne tire que s'il voit le joueur : ligne de vue dégagée, à moins de 70 m pour un policier et 45 m pour un soldat, un vigile ou un membre de gang (`vue`). Il tire toutes les 1 à 2 s, 0,6 à 1,2 s pour le Kommandant et 1,5 à 3 s pour Hitler (`tir`). Les vigiles et les policiers d'élite armés d'une mitraillette ou d'un fusil d'assaut tirent en rafales : 3 à 5 balles à 0,13 s d'écart, puis une pause de 1,2 à 2 s. Il avance à 4,5 m/s (`vitesse`) si le joueur est à plus de 22 m et recule s'il est à moins de 6 m. Tous ces chiffres, et ceux du tableau ci-dessous, sont dans le tableau `ENNEMIS`, une ligne par sorte d'ennemi (le policier d'élite a la sienne, `elite`).

**Les murs protègent** : un mur, un plancher, un toit, un meuble haut, un tronc d'arbre ou une colline entre les yeux de l'ennemi et ceux de B.J. (à 1,5 m au-dessus des pieds) l'empêche de le voir, même un mur de 30 cm. Par une porte ouverte, il le voit. Chaque balle s'arrête aussi sur le premier mur de son chemin : son trait s'arrête là, elle y laisse un impact (voir « Les impacts de balles »), et elle ne blesse pas. On est donc à l'abri dans un immeuble (loin de la porte), à l'étage, derrière le mur d'enceinte du fort ou accroupi derrière le muret d'un toit. C'est vrai pour tout ce qui tire des balles : policiers, soldats, vigiles, gangs, heavy robot et mitrailleuses de la banque. Mesuré dans un immeuble, avec 3 étoiles, pendant 90 s : au premier étage ou dans un coin du rez-de-chaussée, aucune balle ne touche B.J. ; face à la porte, 20 à 30 le touchent, toutes par la porte. En faisant le tour du fort par dehors pendant 3 minutes : aucune (avant la correction : 128, toutes à travers le mur).

| Ennemi | Dégâts par balle |
| --- | --- |
| Policier | 5 |
| Soldat | 7 |
| Kommandant | 12 |
| Hitler | 35 par roquette, au centre de l'explosion |
| Vigile | 9, le double au fusil à pompe à moins de 15 m |
| Policier d'élite | 9 |
| Chien de garde | 12 par morsure, toutes les 0,9 s ; il court à 9 m/s |
| Heavy robot | 10 par balle de mitrailleuse, 40 par roquette (`degats`, `degatsRoquette`) |
| Mitrailleuses de la banque | 5 par balle (`degatsMitrailleuse`, dans `REGLAGES`) |
| Membre de gang | 6, le double au fusil à pompe à moins de 15 m |

Avec le code de triche `Z6PO`, les balles font moitié moins mal (2,5 pour un policier), même celles des mitrailleuses de la banque, du heavy robot et des gangs ; pas les roquettes ni les morsures de chien.

La chance de toucher vaut 35 % à courte distance (`precision`) et baisse avec l'éloignement : environ 25 % à 25 m et 7 % au-delà de 50 m. Les vigiles, les policiers d'élite et le heavy robot visent mieux : 50 % de près ; les mitrailleuses de la banque, 30 % (`precisionMitrailleuses`, dans `REGLAGES`). Elle est divisée par 2 si on est accroupi, et multipliée par 0,6 si on court. En voiture, elle est multipliée par 0,7 et on ne prend que 40 % des dégâts ; dans une voiture blindée, rien ne passe ; dans le heavy robot, on ne prend que 30 % des dégâts (`protectionRobot`).

**Chacun son tour** : seuls les 2 policiers les plus proches qui voient B.J. peuvent le toucher (`tireursPolice`, dans `REGLAGES`) ; les policiers d'élite et le heavy robot comptent parmi eux. Les autres tirent quand même, mais leurs balles passent à côté : ça siffle de partout, sans tuer en quelques secondes. Abattre les plus proches donne leur tour aux suivants. Les roquettes du robot n'attendent pas leur tour. Les nazis, les vigiles, les gangs, les chiens et les mitrailleuses de la banque ne sont pas concernés : leurs combats ont un nombre fixe d'ennemis.

Hitler tire au bazooka. Sa roquette vole comme celle du joueur : il vise B.J. là où il est au moment du tir (il ne prévoit pas où il va). Elle explose si elle passe à moins de 1 m de lui, sur un mur ou une voiture, ou par terre. Elle laisse une traînée de fumée grise, qui aide à la voir venir. À 20 m, elle met 0,8 s à arriver : en courant sur le côté dès qu'on voit la flamme, on l'esquive encore, de justesse. Une roquette ratée vise le sol à 3 à 6 m de B.J. et peut encore le blesser (rayon de 5 m). Elle explose aussi sur les soldats, policiers ou passants qui se trouvent sur son chemin, et les blesse comme le bazooka de B.J. (jusqu'à 250) : on peut se cacher derrière eux. Un piéton ou un policier tué par Hitler ne donne pas d'étoile à B.J. Hitler n'est jamais blessé par sa propre roquette. Elle fait exploser la voiture de B.J. s'il est dedans.

**Temps de survie estimé, sans bouger ni se soigner** :

| Situation | Temps moyen avant de mourir |
| --- | --- |
| 1 policier à 10 m | environ 85 s |
| Le Kommandant à 10 m | environ 20 s |
| Hitler à 10 m, sans bouger | environ 16 s |
| Les 8 soldats à 20 m qui voient le joueur | environ 10 s |
| Un fourgon blindé débarque 4 policiers d'élite à 22 m (4 étoiles) | environ 7 à 10 s (4 à 6,5 s avant « chacun son tour ») |

Avec un gilet pare-balles, ces temps doublent à peu près. Contre Hitler, on tient bien plus longtemps en esquivant ses roquettes. Ce sont des calculs à partir des réglages, pas des mesures en jeu, sauf le fourgon blindé : mesuré devant la bijouterie (9,5 s).

Les nazis (soldats, Kommandant et Hitler) ne quittent jamais l'enceinte du bunker ou du château. Ils attaquent quand ils voient le joueur, ou quand il tire à moins de 50 m.

## Police et recherche

Le niveau de recherche va de 0 à 5 étoiles. Chaque bêtise ajoute une étoile ; 12 s sans être vu par la police en retirent une, comme un pot-de-vin trouvé dans un immeuble. À 0 étoile, les policiers sont pacifiques.

### Ce qui donne une étoile

- Tuer un piéton, à l'arme ou en l'écrasant.
- Tuer un policier.
- Tuer quelqu'un au volant, d'une balle ou en faisant exploser sa voiture : il compte comme un piéton ou un policier abattu (voir « Dégâts »).
- Frapper un policier, tirer à moins de 30 m de lui ou tirer sur sa voiture quand il est au volant, quand on n'a encore aucune étoile.
- Voler une voiture de police, ou n'importe quelle voiture sous les yeux de la police. Voler un objet de valeur dans un immeuble sous les yeux de la police.
- Renverser un policier en le bousculant, quand on n'a encore aucune étoile.
- Braquer la banque : prendre les 2 000 $ du coffre donne 3 étoiles d'un coup.
- Déclencher l'alarme d'un braquage : on monte d'un coup à 4 étoiles (musée, bijouterie) ou 5 (banque Pacific Standard).
- Tuer un vigile.

### La réponse de la police

| Étoiles | Policiers au plus (à pied et en route) | Voitures de police en route, au plus | En plus | Temps minimum pour tout perdre |
| --- | --- | --- | --- | --- |
| 1 | 2 | 0 | | 12 s |
| 2 | 6 | 1 | | 24 s |
| 3 | 10 | 2 | | 36 s |
| 4 | 16 | 4 | Une voiture sur deux est un fourgon blindé, avec 4 policiers d'élite | 48 s |
| 5 | 22 | 5 | Le heavy robot | 60 s |

Ces nombres sont dans les réglages `policiers` et `voituresPolice`. Les policiers qui arrivent en voiture comptent déjà (2 par voiture, 4 par fourgon) : la police ne dépasse pas le nombre du tableau.

- **À pied** : un renfort apparaît toutes les 4 s, hors de vue, entre 45 et 170 m, au coin d'un pâté : il n'y en a pas en pleine campagne.
- **En voiture** : dès 2 étoiles, une voiture de police apparaît toutes les 6 s entre 90 et 230 m. Elle roule à 65 km/h, sur les rues comme sur les routes de campagne, et prend à chaque carrefour le chemin le plus court jusqu'au joueur (recalculé chaque seconde). À moins de 30 m, elle s'arrête et 2 policiers en descendent.
- **Fourgons blindés** : dès 4 étoiles (`etoilesBlindes`), une voiture sur deux est un fourgon blindé. Il roule à 122 km/h (`vitesseBlindes`) : il rattrape une voiture classique, pas une Porsche. Les balles ne lui font rien, il tient 3 roquettes. Arrivé, il débarque 4 policiers d'élite, qui tirent en rafales. Chacun son tour (voir « Les ennemis ») : seuls les 2 plus proches peuvent toucher B.J.
- **Après une alarme de braquage**, pendant une minute, les renforts à pied et en voiture arrivent 3 fois plus vite (toutes les 1,3 s et toutes les 2 s).
- **Être vu** : un policier vivant à moins de 50 m avec une ligne de vue dégagée, ou une voiture de police conduite à moins de 50 m. Les étoiles clignotent en bleu tant que la police voit le joueur. Un mur cache (voir « Les ennemis ») : dans un immeuble, loin de la porte, les policiers à pied ne voient plus B.J.
- **Fin de poursuite** : à 0 étoile, les renforts à plus de 50 m disparaissent. Mourir remet aussi les étoiles à 0.

La sirène s'entend à moins de 180 m d'une voiture de police en route, et les policiers apparaissent en points rouges et bleus sur la mini-carte.

### Le heavy robot

À 5 étoiles (`etoilesRobot`), la police envoie un heavy robot, comme dans *Wolfenstein : The New Order*. Il arrive 15 s après la 5e étoile, hors de vue, entre 70 et 170 m ; il n'y en a qu'un à la fois, et le suivant arrive 15 s après qu'on s'en est débarrassé. Quand on perd toutes ses étoiles, il repart s'il est à plus de 50 m.

- **Le robot** : 4,7 m de haut, gris-bleu acier, sur deux grosses jambes avec des vérins. Son torse est une caisse blindée, avec « POLICE » sur le ventre, deux gyrophares, deux phares et deux pots d'échappement. Devant, derrière une vitre blindée, un policier est assis aux commandes. Au bras gauche, une mitrailleuse à 6 canons qui tournent ; au bras droit, un lance-roquettes à 4 tubes.
- **Il marche** à 4 m/s (`ENNEMIS.robot.vitesse`, la même quand B.J. le pilote), droit sur B.J. quand il le voit (à moins de 110 m), sinon par les rues, en suivant le chemin des voitures de police. Chaque pas fait un bruit sourd, et fait trembler la caméra quand il est à moins de 40 m. Il bute contre les murs et les autres robots, ne passe pas sous les portes et ne va pas dans plus de 2 m d'eau.
- **Il écrase** ce qu'il trouve sur son chemin en marchant, qu'il soit piloté par la police ou par B.J. : un personnage à moins de 1,7 m de son centre est tué (1 000 dégâts) et projeté de côté (5 m/s, et 3 m/s vers le haut) ; une voiture qu'il touche a le toit aplati d'un bout à l'autre (voir « Dégâts ») : les vitres éclatent, le conducteur est tué, puis elle prend feu et explose au bout de 5 s. Il passe ensuite à travers l'épave. Les bateaux, les avions, les voitures blindées, les carcasses brûlées et la voiture où se trouve B.J. l'arrêtent, comme un mur. Quand B.J. le pilote, ce qu'il écrase compte comme s'il l'avait tué (une étoile par piéton ou policier).
- **Il tire** quand il voit B.J. et lui fait face : des rafales de 10 énormes balles (un gros trait jaune), à 0,12 s d'écart, puis une pause de 1,5 à 2,5 s ; et une roquette toutes les 5 à 8 s, comme celles d'Hitler (rayon 5 m). Ses balles cabossent la voiture où se trouve B.J.
- **Le vaincre** : son blindage arrête tout (les balles ricochent), sauf la vitre de la cabine. Elle tient 350 points (`ENNEMIS.robot.vitre`) : 9 balles de pistolet, 11 de fusil d'assaut, ou 2 roquettes. Une fois la vitre en éclats, on peut abattre le pilote (70 points, tête × 2,5 ; une explosion le blesse aussi), ou s'approcher à moins de 3,8 m et appuyer sur E pour l'éjecter : il tombe à côté et attaque. Sans pilote, le robot s'agenouille.
- **Le piloter** : E à côté d'un robot sans pilote fait monter B.J. dans la cabine (on le voit assis, derrière la vitre cassée). La mitrailleuse lourde fait 45 dégâts par balle, 11 balles par seconde, et porte à 150 m ; les roquettes font 250 dégâts (rayon 6 m), une toutes les 1,2 s. Il a 500 balles et 12 roquettes (tableau `ARMES_ROBOT`). Dedans, on ne prend que 30 % des dégâts. En mourant, B.J. est éjecté.
- Sur la mini-carte, le robot est un gros point qui clignote en rouge et bleu, gris quand personne ne le pilote.

## Véhicules

Tous les véhicules se volent, garés ou en circulation, police comprise. Il suffit d'appuyer sur E à moins de 1,30 m du bout du véhicule (3,50 m de son milieu pour une voiture classique), et à peu près à la même hauteur que lui. Si quelqu'un conduit, il est éjecté : un civil s'enfuit, un policier attaque. En montant, le nom du véhicule s'affiche en haut de l'écran pendant 2 s (« PORSCHE », « VOITURE DE POLICE »…), dans la langue choisie.

### Les types de véhicules

Il y a 13 types de voitures, une moto, un Segway, un tricycle, la voiture et le fourgon blindé de la police, 2 bateaux, un avion, un hélicoptère, et pour la glisse des skis, un snowboard et une luge (voir « La glisse »). Ils sont décrits dans le tableau `VOITURES`, en haut de `index.html`.

| Type | Vitesse maximale | 0 à 100 km/h | Virage | Chance | Taille (long. × larg. × haut.) | Couleurs | Signes particuliers |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Classique | 115 km/h (32 m/s) | 2,0 s | 1 | 6 | 4,4 × 1,8 × 1,45 m | les 10 | Berline à 4 portes, pare-chocs chromés |
| Porsche | 180 km/h (50 m/s) | 1,3 s | 1,2 | 2 | 4,3 × 1,9 × 1,28 m | rouge, jaune, gris, noir, bleu | Basse, phares ronds, aileron, 2 pots d'échappement |
| Minibus | 90 km/h (25 m/s) | jamais | 0,8 | 3 | 5 × 1,95 × 2,1 m | 5 couleurs vives | Haut couleur crème, phares ronds, 4 vitres de chaque côté |
| 4x4 du désert | 108 km/h (30 m/s) | 1,7 s | 0,9 | 2 | 4,8 × 2,05 × 2 m | sable, kaki | Grosses roues, pare-buffle, galerie avec jerricans, roue de secours, 4 projecteurs |
| Limousine | 101 km/h (28 m/s) | 2,7 s | 0,6 | 1 | 7,4 × 1,85 × 1,45 m | noir, blanc | Très longue, 4 vitres de chaque côté, baguettes chromées |
| Tricycle | 72 km/h (20 m/s) | jamais | 1,4 | 1 | 2,5 × 1,3 × 1,25 m | les 10 | Moto à 3 roues : on voit le pilote, et rien ne le protège |
| Moto | 173 km/h (48 m/s) | 1,2 s (calculé) | 1,3 | 2 | 2,2 × 0,8 × 1,2 m | rouge, noir, bleu, jaune, vert | Réservoir, carénage, selle, pot chromé ; la fourche, le guidon et le phare tournent avec la roue avant. Elle penche dans les virages. On voit le pilote, et rien ne le protège |
| Segway | 22 km/h (6 m/s) | jamais | 2,2 | 1 | 0,8 × 0,75 × 1,3 m | noir, blanc | Deux roues côte à côte, une plateforme, un manche et un guidon : on s'y tient debout. Tourne presque sur place |
| DeLorean | 151 km/h (42 m/s) | 2,1 s (calculé) | 1 | 1 | 4,2 × 1,86 × 1,14 m | inox | Un coin tout plat en inox brossé, lamelles noires sur la vitre arrière, bande noire sur les flancs ; derrière, les tuyaux et le réacteur de la machine à remonter le temps. À 88 miles à l'heure, voir plus bas |
| Coccinelle | 108 km/h (30 m/s) | 3,1 s (calculé) | 1,1 | 2 | 4,05 × 1,55 × 1,5 m | jaune, bleu, rouge, vert, crème | Toute ronde, ailes bombées, phares ronds sur les ailes, marchepieds, pare-chocs chromés ; son moteur pétarade |
| Skoda Kodiaq | 130 km/h (36 m/s) | 2,1 s (calculé) | 0,95 | 2 | 4,76 × 1,88 × 1,68 m | vert, blanc, bleu nuit, gris, bordeaux | Le modèle 2025 : un grand SUV carré, feux très fins, feux arrière reliés par un trait, passages de roue noirs, barres de toit |
| Audi TT | 158 km/h (44 m/s) | 1,7 s (calculé) | 1,15 | 1 | 4,05 × 1,78 × 1,35 m | gris, jaune, rouge, noir, bleu | Toute ronde, toit en dôme, les quatre anneaux chromés sur la calandre |
| Lamborghini | 209 km/h (58 m/s) | 1,1 s (calculé) | 1,2 | 1 | 4,8 × 2,03 × 1,14 m | vert pomme, orange, jaune, violet, noir | La plus rapide : un coin très plat et très large, prises d'air noires sur les flancs, grand aileron |
| Rolls-Royce | 144 km/h (40 m/s) | 2,5 s (calculé) | 0,7 | 1 | 5,8 × 2 × 1,65 m | noir, bleu nuit, bordeaux, gris | Longue, haute et carrée, grande calandre chromée, la statuette sur le capot, baguette chromée ; le moteur le plus silencieux |
| Audi Quattro de rallye | 166 km/h (46 m/s) | 1,4 s (calculé) | 1,25 | 1 | 4,2 × 1,82 × 1,36 m | blanc | Une boîte des années 80 : énorme aileron, becquet, 4 phares de course sur le capot, bandes et bavettes rouges ; son moteur pétarade |
| Austin Mini | 122 km/h (34 m/s) | 2,3 s (calculé) | 1,5 | 2 | 3,05 × 1,41 × 1,35 m | vert anglais, rouge, jaune, bleu, blanc | Toute petite, toit blanc, phares ronds, calandre chromée ; tourne très sec |
| Voiture de police | 115 km/h (32 m/s) | 2,0 s | 1 | 0 | 4,4 × 1,8 × 1,45 m | blanc | Classique avec bande bleue et gyrophares |
| Fourgon blindé | 137 km/h (38 m/s) | 2,3 s (calculé) | 0,8 | 0 | 5,8 × 2,3 × 2,55 m | noir | Caisse d'acier, petites vitres, grosses roues, pare-buffle, marchepieds, « POLICE » sur les flancs, gyrophares, projecteurs. Blindé : les balles ricochent, il tient 3 roquettes |
| Hors-bord | 108 km/h (30 m/s) | pas mesuré | 0,8 | 0 | 5,5 × 2,1 × 1,4 m | blanc, rouge, bleu, noir | Coque en V, pare-brise, moteur à l'arrière ; on voit le pilote |
| Jet-ski | 86 km/h (24 m/s) | pas mesuré | 1,5 | 0 | 3 × 1,15 × 1,1 m | jaune, bleu, rouge, vert | Petite coque, selle, guidon ; on voit le pilote |
| Avion | 252 km/h (70 m/s) | décolle à 115 km/h, en 5,3 s | — | 0 | 16 × 20 (ailes) × 5,2 m | le dessus blanc ; rouge, bleu, vert, orange | Petit avion de ligne à deux moteurs sous les ailes, train d'atterrissage, hublots, cockpit |
| Hélicoptère | 144 km/h (40 m/s) | 115 km/h en 4 s (mesuré) | — | 0 | 11,5 × 2,4 × 3,4 m | bleu, rouge, noir, jaune | Cabine en bulle vitrée, longue queue, deux patins, un grand rotor et un petit à l'arrière, qui tournent |

- **Chance** : sur 29 véhicules tirés au sort, il y a en moyenne 6 classiques, 3 minibus, 2 Porsche, 2 4x4, 2 motos, 2 Coccinelle, 2 Kodiaq, 2 Mini, et 1 de chacun des autres (limousine, tricycle, Segway, DeLorean, Audi TT, Lamborghini, Rolls-Royce, Quattro). La voiture et le fourgon de police ne sont jamais tirés au sort : ils n'arrivent que quand on est recherché.
- **Virage** : 1 = comme la classique. Le Segway, la Mini et le tricycle tournent sec, la limousine et la Rolls-Royce très large.
- **La moto penche** vers l'intérieur des virages, roues et pilote compris, comme une vraie : de l'angle dont la pencherait la force du virage (atan(accélération de côté ÷ 9,8)), jusqu'à 50°. Garée, elle tient droite.
- **La DeLorean à 88 miles à l'heure** (142 km/h, 39,3 m/s), comme dans *Retour vers le futur* : un éclair, un grand boum, « 88 MILES À L'HEURE ! Retour vers le futur ! », et pendant 1,5 s deux traînées de feu derrière les roues arrière. Ça recommence si elle repasse sous 126 km/h. On ne voyage pas dans le temps.
- Les vitesses et les temps du tableau ont été mesurés en ligne droite, pied au plancher.
- En circulation, tout le monde roule à 40 km/h.
- **Avions et hélicoptères** (`vole: 'avion'` ou `'helico'`) : voir plus bas.
- **Bateaux** (`bateau: true`) : on ne les croise pas en circulation, ils attendent aux pontons. Ils flottent, n'avancent que là où il y a au moins 50 cm d'eau, et s'arrêtent net contre la plage, un ponton ou un pilier de pont. Leur nez se lève quand ils foncent. Comme sur le tricycle, rien ne protège le pilote. En descendant au large, on nage.

### La glisse : skis, snowboard, luge

Ce sont des véhicules du tableau `VOITURES` avec `glisse: true`, sans roues ni moteur. On les prend aux gares des remontées (voir « La station de ski et les remontées »). En montant dessus, leur nom s'affiche avec leurs commandes (« SKIS », « Z : pousser · S : freiner · Espace : sauter »).

| Type | Vitesse maximale (le long de la pente) | Poussée | Virage | Taille (long. × larg.) | Couleurs | Pose de B.J. |
| --- | --- | --- | --- | --- | --- | --- |
| Skis | 108 km/h (30 m/s) | 3 m/s² | 1,5 | 1,75 × 0,45 m | rouge, bleu, jaune, noir, blanc | Debout, les genoux pliés, les mains en avant, un bâton dans chaque main. Il penche dans les virages, les skis aussi |
| Snowboard | 115 km/h (32 m/s) | 2,5 m/s² | 1,3 | 1,55 × 0,5 m | vert, orange, violet, noir, bleu | De côté sur la planche, le pied droit devant, les pieds écartés, les bras écartés, la tête tournée vers l'avant. Il penche en avant ou en arrière dans les virages |
| Luge | 79 km/h (22 m/s) | 2 m/s² | 0,8 | 1,3 × 0,5 m | bois clair, bois foncé, rouge | Assis, les jambes tendues devant, les mains sur les montants. Il penche avec la luge |

- **C'est la pente qui fait avancer** : elle accélère de 9,8 × sin(pente) m/s chaque seconde en descente, et freine autant en montée. La neige freine de 0,4 m/s chaque seconde (`frottementNeige`) ; sans neige (herbe, route, rue, ville), 15 fois plus : on s'arrête vite. Entre les deux, là où la neige s'en va par plaques, ça freine d'autant plus qu'il en reste moins. La place de la station compte comme de la neige. L'air freine de 0,004 × vitesse², et tourner freine de 0,1 × vitesse. Pour ralentir, on tourne en travers de la pente.
- **Les touches** : Z pousse sur le plat, jusqu'à 4 m/s. S freine de 12 m/s chaque seconde, puis fait reculer un peu (2 m/s). Q et D tournent, même à l'arrêt, pour se mettre dans la pente ; à pleine vitesse, deux fois moins vite. Espace fait sauter (une fois par appui).
- **Pousser** (Z, sous 16 km/h) : à ski, B.J. plante ses deux bâtons devant lui et pousse jusque derrière, un geste par seconde environ. En snowboard, il se tourne vers l'avant, sort le pied arrière (le gauche) de la planche et pousse avec, comme en trottinette ; le pied avant reste sur sa fixation. Mesuré : le pied avant à 5 cm de sa fixation, le pied arrière à 16 à 32 cm à côté de la planche, de 30 cm derrière à 30 cm devant. En luge, il ne bouge pas.
- **Le saut** (Espace) : 4,5 m/s (`sautGlisse`) en plus de la vitesse à laquelle la pente descend sous les skis. On décolle donc d'un mètre de la neige, à l'arrêt comme à fond dans une pente raide. Mesuré : 1,05 m sur le plat ; 0,75 m à 85 km/h dans une pente de 35°, 0,7 s en l'air, sans chute.
- **La vitesse maximale** compte le long de la pente : dans une pente raide, on avance moins vite à l'horizontale (le compteur donne la vitesse à l'horizontale). Mesuré sur La Gordo, depuis le haut, 3 s de poussée puis plus rien, en suivant la piste : à ski, 69 km/h au bout de 3 s, 59 km/h à 10 s (un replat), 78 km/h à 25 s (à 282 m de haut), 95 km/h à 40 s (à 66 m) ; en snowboard, 91 km/h à 25 s ; en luge, 69 km/h à 25 s et 72 km/h à 40 s (à 205 m).
- **Collé à la neige** : les jambes amortissent les bosses, même quand la pente plonge après un replat. Les skis ne quittent la neige qu'à un vrai rebord (si la neige passe en une image à plus de 15 cm, plus 2 cm par m/s, sous eux : le bout d'un kicker) ou quand on saute. Ils suivent la neige sous leur milieu. Dans une pente, le sol descend sous les skis de vitesse × tangente de la pente (au lieu du sinus des voitures), pour qu'ils restent collés même à 50°.
- **La réception** : seul compte ce qui tape en travers de la pente. Dans une pente raide, on se reçoit en douceur, comme au bas d'un tremplin, et la vitesse de la chute qui va dans le sens de la pente n'est pas perdue. La neige ne fait pas rebondir. On ne déchausse et on ne se fait mal qu'en tombant de vraiment très haut : plus de 15 m/s en travers (`chuteGlisse`), soit 11 m de chute sur du plat. Mesuré sur le plat de la station : de 8 m, on se reçoit sans mal ; de 25 m, on tombe.
- **La chute** : un choc à plus de 40 km/h (un sapin, un pylône, une voiture, un autre skieur) ou une réception trop dure fait partir l'engin en accident, et B.J. est éjecté comme d'une moto : il roule dans la neige et, au-dessus de 36 km/h, se fait mal (1,5 point par m/s en plus). Mesuré : lancé à 72 km/h contre un pylône, 15 points.
- **Penché, la main sur la neige** : debout, B.J. penche dans les virages (jusqu'à 50° de la verticale), mais jamais à plus de 52° de la neige : dans une pente raide, en tournant vers le haut, il ne s'enfonce plus dans la montagne. À plus de 30° de la neige, il tend la main vers elle (à ski, celle du côté où il penche ; en snowboard, penché en avant, les deux), tout à fait à 50°. Si la main arrive sous la neige, le bras se relève juste ce qu'il faut. Mesuré, virage à fond à 86 km/h dans une pente de 50° : 54° au plus (le temps que le corps suive la pente), et la main, au plus bas, à 0 à 3 cm au-dessus de la neige.
- **Les tenues de glisse** (tableau `TENUES_GLISSE`) : B.J. se change en montant, et remet sa tenue en descendant. À ski, la combinaison fluo des années 80 : rose avec trois éclairs en zigzag (jaune, vert, bleu), un bras bleu et un bras jaune, gants et chaussures verts, bandeau jaune, lunettes miroir. En snowboard, la tenue du rider : veste kaki à capuche, pantalon noir très large, bonnet, gants et chaussures orange, masque bleu. En luge, la surprise : le Père Noël sur son traîneau, manteau rouge bordé de blanc, ceinture noire, bonnet à pompon et grande barbe blanche. Un code de triche actif passe par-dessus.
- Ils ne s'abîment pas (ni bosses, ni feu). B.J. range son arme, et rien ne le protège des balles.
- **La caméra** plonge avec la pente (de 80 % de la pente, en plus du regard) : sinon, dans une pente raide, on ne verrait que le ciel.
- **Le son** : pas de moteur, seulement le souffle du roulement, qui monte avec la vitesse. Espace ne fait pas crisser de pneus.

### Avions et hélicoptères

Il y a 8 avions : un dans chaque hangar (`N`, 5 à l'aéroport de Los Santos et 1 à Fort Zancudo), un sur la piste de Los Santos et un sur l'aérodrome de Sandy Shores (`^`). Il y a 2 hélicoptères, sur les hélistations de l'aéroport de Los Santos (`@`). On les vole avec E, comme une voiture ; une annonce rappelle les commandes. Ils ne s'abîment pas (ni bosses, ni vitres, ni accidents), mais une roquette les fait exploser, même en vol.

- **La caméra** : dedans, la souris ne tourne plus la caméra autour de l'appareil, elle vise, comme à pied. L'avion et l'hélicoptère se tournent vers là où l'on regarde. La mini-carte dézoome deux fois plus qu'en voiture. En vol, le compteur donne aussi la hauteur au-dessus du sol ou de l'eau (« 216 km/h · 85 m »).
- **L'avion au sol** : il roule comme une voiture (Z : plus vite, jusqu'à 70 m/s en l'air ; S : il freine fort), tourne vers où l'on regarde quand il roule, et cogne les murs et les voitures avec son fuselage (pas avec ses ailes). À 115 km/h (`decollage`, 32 m/s), une annonce dit de regarder vers le haut ; dès qu'on lève le nez (souris ou Espace), il décolle. Il lui faut environ 85 m de piste.
- **L'avion en l'air** : il tourne vers où l'on regarde (au plus 0,7 radian par seconde), en penchant dans le virage (de 0,9 radian par radian par seconde, `roulisVirage` : jusqu'à 36°), et son nez suit le regard, vers le haut ou le bas (au plus 0,6 radian, soit 34°). Il ralentit en montant et accélère en piquant. Sans gaz, il garde sa vitesse. Sous 115 km/h, il décroche : il tombe, de plus en plus vite, et pique du nez. On ne monte pas au-dessus de 600 m (`PLAFOND`).
- **Se poser** : l'avion se pose quand il touche le sol (ou un toit) en descendant de moins de 5 m/s, à peu près à plat (penché de moins de 20°, le nez pas plus bas que 9°). Sinon, il s'écrase et explose. Il explose aussi si son nez, le bout de ses ailes ou sa queue touche un bâtiment, un arbre ou une colline. Sur l'eau, il coule, et B.J. en sort à la nage.
- **L'hélicoptère** : son rotor met 2 s à tourner à fond ; ensuite, Espace le fait monter et C descendre, à 8 m/s (`montee`), et il tient en l'air tout seul. En l'air, Z Q S D le font avancer, reculer ou glisser sur le côté (jusqu'à 144 km/h devant, 60 % de côté), en accélérant de 8 m/s par seconde ; il penche le nez en avant quand il avance, et sur le côté quand il glisse. Il penche aussi dans ses virages quand il avance, comme l'avion (jusqu'à 36°, `roulisVirage`), à fond à partir de 36 km/h ; sur place, il tourne à plat, et en reculant il penche de l'autre côté. Il se pose sur le sol ou sur un toit. Il bute contre les murs, et s'y écrase s'il y fonce à plus de 54 km/h ; il s'écrase aussi s'il tombe à plus de 9 m/s.
- **Descendre** : on ne descend qu'une fois posé (« Pose-toi d'abord ! »). Si l'appareil explose en vol, B.J. est éjecté et tombe : de plus de 14 m, il meurt en arrivant en bas (il n'y a pas de parachute).
- **Sans pilote** : un avion ou un hélicoptère abandonné en l'air (B.J. est mort aux commandes) tombe et s'écrase ; posé, il reste où il est.
- Dedans, on est protégé comme dans une voiture : 40 % des dégâts, et on ne peut pas tirer.

### Conduite

| Caractéristique | Valeur |
| --- | --- |
| Marche arrière | 36 km/h |
| Freinage | 2,5 fois plus fort que l'accélération |

- La direction ne répond pas à l'arrêt. Elle est la plus vive vers 20 km/h, puis deux fois moins à pleine vitesse.
- Les roues avant braquent quand on tourne. La carrosserie pique du nez au freinage, se cabre à l'accélération et penche dans les virages (4° au plus).
- Le frein à main (Espace) freine fort et serre le virage.
- Contre un mur ou une autre voiture, au-dessus de 22 km/h, il y a un bruit de choc et la voiture perd 65 % de sa vitesse. Au-dessus de 11 km/h (vers le mur), elle s'abîme (voir « Dégâts ») ; au-dessus de 40 km/h, c'est l'accident (voir « Accidents »).
- **Lampadaires** : au-dessus de 11 km/h, la voiture les renverse. Chacun lui fait perdre 15 % de sa vitesse et un petit creux étroit (0,12). Il tombe dans le sens où elle roule, reste par terre, et se relève quand B.J. est à plus de 300 m. Plus doucement, il arrête la voiture comme un mur.
- **Bornes en béton** (voir « Les signes de la carte ») : hautes de 45 cm (`hauteurBornes`), elles tapent dans le bas de caisse. Sous 14 km/h, elles arrêtent la voiture, quand le pare-chocs qui avance arrive contre elles. Une borne qui est déjà sous la voiture (après un accident, ou arrivée par le côté) ne la retient pas : elle repart. Plus vite, elles abîment le dessous et le bas du pare-chocs (0,025 par m/s) et la font sauter : elle monte à 25 % de sa vitesse et en perd 25 % (30 % sous 31 km/h, pour un petit saut). Au-dessus de 8,5 m/s (31 km/h), c'est un accident : elle décolle le nez en l'air (0,06 × sa vitesse, en radians par seconde), et si la borne tape d'un côté, elle se renverse de l'autre (jusqu'à 0,12 × sa vitesse). Le 4x4 et le fourgon, 50 cm sous la caisse, passent au-dessus sans rien sentir.
- En descendant, le joueur sort du côté qui n'est pas contre un mur. La voiture continue sur son élan puis s'arrête. Si elle roule à plus de 14 km/h, B.J. roule par terre (voir « Sauter, tomber, rouler »).
- **Dos d'âne** : la voiture monte et descend avec la bosse. Prise vite, elle garde l'élan de la montée en passant le sommet, et saute : à 100 km/h, elle monte à 39 cm et reste environ une demi-seconde en l'air, sur une quinzaine de mètres ; à 30 km/h, elle ne fait que passer dessus.
- **Pentes** : la voiture suit le sol et penche avec lui, en avant et sur le côté. La pente la freine en montée et la pousse en descente (`graviteVoiture`, 9,8 m/s², × le sinus de la pente) : une classique monte la route du château sans peine.
- **Sauts** : la voiture tombe avec la vraie gravité (9,8 m/s², `graviteVoiture`). Elle décolle quand le sol descend plus vite qu'elle ne tombe : au bout d'un tremplin, en haut d'une bosse ou d'une côte prise vite, un peu en montant sur un trottoir. Au bout d'un tremplin, elle garde tout l'élan de la rampe, même quand ses roues avant sont déjà dans le vide. En l'air, ni gaz, ni frein, ni volant, et son nez suit peu à peu la trajectoire. Un saut de moins de 30 cm ne compte pas : les amortisseurs le prennent, et on garde la main.
- **Retomber** : elle rebondit un peu (20 % de la vitesse du choc, au-dessus de 3 m/s). Au-dessus de 7 m/s (une chute de 2,5 m sur du plat), elle s'abîme : ses roues se tordent, et l'avant ou l'arrière se cabosse si elle retombe sur le nez ou sur l'arrière (penchée de plus de 17° par rapport au sol). Retomber sur une rampe dans le sens de la pente ne fait presque rien. Après plus de 0,8 s en l'air, « SAUT ! » annonce la longueur du saut.
- **Loopings et tire-bouchons** : la voiture y roule comme sur des rails, sur son élan : ni moteur, ni frein, ni volant, et la pente la ralentit en montant. Elle reste plaquée tant que (vitesse² × courbure) + (9,8 × la part de la piste tournée vers le haut) reste positif. En haut d'un looping de 9 m, il faut 9,4 m/s, donc au moins 76 km/h en bas ; en haut du tire-bouchon, 9,2 m/s, soit environ 60 km/h en bas. Sinon, elle tombe (« Pas assez d'élan ! ») comme elle est, souvent sur le toit : c'est un accident (voir « Accidents »). Le toit s'écrase, et si elle reste sur le toit, elle prend feu puis explose. Trop lente avant d'être à la verticale, elle redescend en arrière. À la sortie, « LOOPING ! » ou « TIRE-BOUCHON ! » s'affiche. On y entre par un bout ou par l'autre, en avant ou en marche arrière. En vue intérieure (V), la caméra tourne avec la voiture.
- **Dans l'eau** : à plus de 40 cm d'eau, la voiture freine fort. À plus de 1,10 m, elle coule : B.J. en sort à la nage, et on ne peut plus y remonter. Elle disparaît au bout de 25 s, quand le joueur est à plus de 60 m.

### Protection

En voiture, le joueur ne prend que 40 % des dégâts, et les ennemis le touchent 30 % moins souvent. En contrepartie, on ne peut pas tirer depuis une voiture.

Le tricycle, la moto, le Segway, le hors-bord, le jet-ski, les skis, le snowboard et la luge n'ont pas de carrosserie : ils ne protègent pas. On y prend les mêmes dégâts qu'à pied, et on ne peut pas tirer non plus.

### La voiture blindée façon Mad Max

Le garagiste de LS Customs blinde les voitures rapides, celles qui vont à au moins 144 km/h (`vitesseBlindable`, 40 m/s) : parmi les voitures du jeu, la Porsche, la Lamborghini, l'Audi Quattro, l'Audi TT, la DeLorean et la Rolls-Royce (la moto n'a pas de carrosserie à blinder). On gare la voiture dans le garage, on descend, et on appuie sur E devant le garagiste : il prend 5 000 $ (`prixBlindage`), des étincelles jaillissent de la soudure, et la voiture est blindée. S'il n'y a pas de voiture dans le garage, si elle n'est pas assez rapide, déjà blindée, ou s'il manque de l'argent, il le dit.

- **Ce qui se voit** : des plaques d'acier rouillé soudées sur les flancs (un peu de travers, avec des rivets et des soudures), sur le capot, le toit et l'arrière ; des barreaux sur le pare-brise et la vitre arrière, deux barres sur les vitres de côté ; un pare-chocs en acier à 5 pointes ; deux pots d'échappement tout droits derrière.
- **Ce que ça fait** : les balles ricochent (« piou ») sans rien abîmer ; les chocs l'abîment 3 fois moins ; elle encaisse 3 roquettes (`roquettesBlindage`), qui la cabossent, et explose à la 4e. Un message dit combien de roquettes elle peut encore prendre. Tant qu'elle tient, rien n'atteint B.J. à l'intérieur : ni balle, ni explosion.
- **Ce que ça coûte** : elle est plus lourde et garde 92 % de sa vitesse et de son accélération (`lourdeurBlindage`) : une Porsche blindée monte à 166 km/h.
- Le garage la répare comme les autres, sans enlever le blindage. Le fourgon blindé de la police, s'il est volé, protège de la même façon.

### Dégâts

Une voiture a cinq côtés, qui s'abîment de 0 (neuve) à 1 (épave) : l'avant, l'arrière, la gauche, la droite et le toit. Les bateaux ne s'abîment pas. Le réglage `degatsVoitures` multiplie tous les dégâts (0 = jamais).

| Ce qui arrive | Dégâts, du côté touché |
| --- | --- |
| Choc contre un mur, un pilier, une voiture | (vitesse vers l'obstacle − 3 m/s) × 0,03 : 0,2 à 36 km/h, 0,5 à 72 km/h, 0,8 à 108 km/h. Frotter un mur en biais abîme peu. L'autre voiture prend autant, de son côté |
| Retomber à plus de 7 m/s | (vitesse − 7) × 0,05 à l'avant ou à l'arrière si elle tombe sur le nez ou l'arrière ; la moitié aux roues |
| Pendant un accident, taper le sol à plus de 3 m/s | (vitesse − 3) × 0,08, là où elle a tapé : le toit, un flanc, un coin (le coup le plus fort de chaque image). Une roue qui tape se tord. Contre un mur ou une voiture, c'est comme sur la route |
| Un lampadaire renversé | 0,12, sur 30 cm de large |
| Une borne en béton | 0,025 par m/s, au dessous et au bas du pare-chocs |
| Une balle | Dégâts de l'arme ÷ 2 000 (0,02 au pistolet), un petit creux de 3 cm avec un trou de balle au milieu (voir « Les impacts de balles »), et la vitre la plus proche (à moins de 80 cm) se fêle, puis se brise. Rien sur une voiture blindée. Une balle dans un pneu le crève (voir « Accidents ») ; ailleurs, elle touche aussi celui qui conduit (voir plus bas) |
| Écrasée par le heavy robot, ou par B.J. qui tombe du ciel (codes `SUPERMAN` et `DIEU`) | 1 au toit, sur chaque cercle de la voiture : le toit s'enfonce de 50 cm d'un bout à l'autre, les vitres éclatent, et elle prend feu. Une voiture blindée ne s'écrase pas : le robot bute contre |
| Une roquette | Tout casse, et la voiture explose (voir plus bas) |

Ce qui se voit :

- **Tôle** : ce qui tape pousse la carrosserie comme un bélier arrondi, de 80 % de la force en mètres (19 cm à 40 km/h, 41 cm à 72 km/h, 65 cm à 108 km/h contre un mur). Ce qui dépasse devant lui est aplati, le reste se froisse, et le capot ou le coffre gondole vers le haut. Le bélier est large de 0,5 m + 0,7 m par point de force pour un mur ou une voiture, de 30 cm pour un lampadaire, de 1,2 m pour le sol. On compte depuis la tôle telle qu'elle est : un deuxième choc au même endroit enfonce plus loin, jusqu'à 90 cm à l'avant et à l'arrière (le capot, le coffre) et 50 cm sur les flancs et le toit. Chaque choc fait sa bosse : une voiture peut être cabossée à plusieurs endroits.
- **Hauteur du choc** : contre un mur, la voiture tape à 35 cm au-dessus du bas de sa caisse. Contre une autre voiture, chacune tape à la hauteur du pare-chocs de l'autre : un fourgon ou un 4x4 enfonce une Porsche au niveau des vitres, une Porsche enfonce le bas d'un fourgon.
- **Vitres** : un choc de plus de 0,08 près d'une vitre la fêle (des fissures blanches) ; une vitre déjà fêlée, ou un choc de plus de 0,3, la brise : elle tombe en éclats, et à sa place on voit le trou sombre de l'habitacle, avec des bouts de verre pointus restés coincés dans le cadre. Un côté abîmé à plus de 0,7 brise toutes ses vitres, et un toit à plus de 0,4 les brise toutes.
- **Pièces qui partent** : les pare-chocs et leur plaque (avant ou arrière, à partir de 0,45 à 0,65), les rétroviseurs (sur le côté, 0,25 à 0,45), l'aileron de la Porsche, et sur le 4x4 le pare-buffle, la roue de secours et la galerie du toit. Elles volent, rebondissent, puis restent 30 s par terre.
- **Phares** : ils s'éteignent quand l'avant passe 0,35 ; les feux arrière, quand l'arrière passe 0,35.
- **Roues** : un choc à moins de 1,5 m d'une roue la tord : elle part de travers (jusqu'à 11°), penche et se dandine en tournant. Des roues avant tordues tirent la voiture d'un côté : il faut tenir le volant. Une chute trop dure tord les quatre.
- **Moteur** : quand l'avant est abîmé, la vitesse maximale baisse (−45 % pour une épave).
- **Fumée et feu** : dès qu'un côté (le plus abîmé) passe 0,5, la voiture fume gris par le capot ; au-dessus de 0,8, noir. À 1 (`degatsFeu` : une épave), elle prend feu : des flammes sortent du haut de la carrosserie côté moteur, dans quelque sens qu'elle soit (sur ses roues, le côté ou le toit), et « AU FEU ! » s'affiche si B.J. est dedans. Elle explose au bout de 5 s (`dureeFeu`) : il faut en sortir avant (E). Les seuils de fumée suivent `degatsFeu` (la moitié, puis les 8 dixièmes) ; `degatsFeu: 2` = jamais de feu. Il faut deux chocs à 72 km/h du même côté, ou, toujours du même côté, 50 balles de pistolet, 59 de fusil d'assaut ou 91 de mitraillette. Une voiture blindée aussi prend feu, mais s'abîme 3 fois moins aux chocs et pas du tout aux balles.
- **Pneus crevés** : la roue s'aplatit, la voiture s'affaisse de ce côté, tire de ce côté (il faut tenir le volant) et perd 15 % de sa vitesse maximale par pneu crevé.
- **Réparer** : entrer en voiture dans un garage LS Customs la répare, gratuitement (« Voiture réparée ! »), pneus compris. Une voiture en feu qui arrive à temps au garage s'éteint.
- **Celui qui conduit** : une balle dans la voiture (pas dans un pneu) le touche aussi, des dégâts de l'arme. Il a autant de vie qu'à pied : 50 pour un passant, 70 pour un policier (2 balles de pistolet). Tué, il tombe à côté de la portière, et la voiture roule sur sa lancée puis s'arrête. Ça compte comme un piéton ou un policier abattu : une étoile, et il lâche de l'argent ou son arme. Tirer sur une voiture de police conduite donne aussi une étoile quand on n'en a aucune. Les balles ne traversent pas une voiture blindée. En plein accident aussi, on peut toucher le conducteur.

### Accidents

Un gros choc, un souffle d'explosion, une borne prise vite, un pneu qui crève à grande vitesse ou une chute de looping : la voiture n'est plus tenue par ses roues. Elle vole, tourne, rebondit et glisse comme une vraie boîte, avec son poids et sa forme, puis s'arrête. Pendant ce temps, ni gaz, ni frein, ni volant, et on ne peut pas descendre. Toutes les voitures, celle de B.J. comprise, font des accidents de la même façon.

| Ce qui arrive | Quand | Ce que ça fait |
| --- | --- | --- |
| Choc contre une voiture | À plus de 40 km/h l'une vers l'autre (`seuilAccident`, 11 m/s) | Les deux voitures sont repoussées : chacune change de vitesse de 1,3 × la vitesse du choc, partagée selon leur poids (la plus légère prend le plus gros coup). Le coup, donné à la hauteur du centre de gravité, la fait tourner sur elle-même s'il tape un bout. La voiture tapée de côté se renverse dans le sens du coup : ses pneus accrochent la route, le haut continue |
| Choc contre un mur | À plus de 40 km/h vers le mur | Elle rebondit (30 % de sa vitesse vers le mur), pivote si elle tape d'un coin, se renverse si elle tape de biais |
| Explosion à côté | Toujours | La carcasse monte à 7 à 10 m/s en tournoyant, poussée à 4 m/s loin de l'explosion (moins haut pour une voiture lourde). Une voiture blindée qui encaisse est soulevée 3 fois moins fort, et retombe presque toujours sur ses roues |
| Borne en béton | À plus de 31 km/h | Elle décolle, le nez en l'air, et se renverse si la borne tape d'un côté |
| Balle dans un pneu | À plus de 50 km/h (`vitesseCrevaison`, 14 m/s) | Tête-à-queue du côté du pneu crevé (au départ, un tour en 3 s à 90 km/h), et un coup de côté pris au hasard : parfois, elle se renverse |
| Chute de looping ou de tire-bouchon | Pas assez d'élan | Elle tombe comme elle est, avec sa vitesse |

- **Le poids** : en gros, le volume de la voiture (longueur × largeur × hauteur), une fois et demie plus pour une voiture blindée. Un fourgon pèse 3 Porsche : il renverse une Porsche, une Porsche rebondit sur lui.
- **Ce qui la fait tourner** : un coup qui ne passe pas par son milieu. Elle tourne facilement autour de sa longueur (les tonneaux), moins bien sur elle-même ou d'avant en arrière. Un coup de côté la fait en plus basculer dans le sens du coup, de 0,15 radian par seconde par m/s de coup (plus ou moins 40 %, au hasard), fois `forceTonneaux` (1) : 0 = elle glisse sans jamais se retourner, 2 = deux fois plus fort. Une voiture haute et étroite (le minibus) se renverse bien plus facilement qu'une voiture basse et large (la Porsche).
- **Mesuré** : une voiture garée prend un coup de côté (5 essais par case, le hasard du coup change à chaque fois). « 2/5 » : elle a basculé (sur le côté ou plus loin) 2 fois sur 5 ; souvent, elle fait un tour complet et retombe sur ses roues. Une voiture qui en tape une autre pareille de côté à 72 km/h lui donne un coup d'environ 13 m/s, à 100 km/h d'environ 18 m/s.

| Coup de côté | 7 m/s | 10 m/s | 13 m/s | 17 m/s | 21 m/s |
| --- | --- | --- | --- | --- | --- |
| Minibus | 3/5 | 5/5 | 5/5 | 5/5 | 5/5 |
| Classique | 0/5 | 1/5 | 2/5 | 4/5 | 4/5 |
| Porsche | 0/5 | 0/5 | 1/5 | 3/5 | 3/5 |

- **Ce qui touche** : le bas de ses 4 roues (3 pour le tricycle), les 8 coins de sa caisse et les 4 coins de son toit. Ils rebondissent un peu (25 %) sur le sol. Les roues frottent fort de côté (0,75) et presque pas dans le sens où elles roulent (0,03) ; la tôle frotte moyennement (0,5). Vue du ciel, elle garde sa file de cercles contre les murs, les lampadaires et les autres voitures, qu'elle pousse (et peut faire partir en accident à leur tour : carambolage). Contre une voiture, c'est la vitesse du point qui tape qui compte, rotation comprise : une voiture qui tourne en toupie, même presque sur place, frappe avec ses bouts, et même un petit coup pousse une voiture déjà accidentée. Quand deux voitures se touchent en plusieurs points (un choc en plein flanc touche les deux cercles de l'autre), le coup est donné au milieu de ces points, dans leur direction moyenne, avant comme pendant un accident : sinon, il partirait d'un bout, et la voiture touchée tournerait sur elle-même pour rien, puis reviendrait taper l'autre.
- **Les piétons** : une voiture accidentée renverse les personnages que touche sa file de cercles, là où elle va à plus de 4 m/s (rotation comprise) : 200 dégâts, et ils volent comme sous une voiture qui roule (voir « Les personnages »). C'est un crime (une étoile) seulement si c'est la voiture de B.J.
- **Deux-roues et tricycle** : rien ne retient leur pilote. Quand une moto, un Segway ou un tricycle part en accident, B.J. est éjecté et roule par terre, avec la vitesse du véhicule (et ses dégâts au-delà de 36 km/h) ; un autre pilote est projeté comme un piéton renversé, et se relève. Sauf dans un looping : on y reste en selle.
- **Les dégâts** : chaque image, le coup le plus fort contre le sol (au-dessus de 3 m/s) cabosse la carrosserie là où il a tapé : le toit quand elle retombe à l'envers, un flanc quand elle roule sur le côté.
- **La fin** : dès qu'elle est droite sur ses roues, sans tourner ni glisser de côté, depuis 0,3 s, on reprend la main, même si elle roule encore. Sinon, il faut qu'elle soit arrêtée (ou que l'accident dure depuis 12 s, qu'elle touche le sol et qu'elle aille à moins de 3 m/s et tourne à moins de 3 radians par seconde : jamais figée en l'air, ni en pleine culbute ; le souffle d'une explosion remet ce compteur à zéro, pour qu'elle retombe et se pose d'abord). Le conducteur d'une autre voiture en sort alors, secoué : un civil s'enfuit, un policier attaque.
- **Couchée sur le côté ou sur le toit** : elle prend feu (« AU FEU ! », de la fumée noire), et explose au bout de 5 s (`dureeFeu`). Il faut en sortir avant (E). On ne monte pas dans une voiture en plein accident ni couchée. Si un autre choc la remet sur ses roues avant, le feu s'éteint, sauf si elle est trop abîmée (voir « Dégâts »).
- **La caméra** ne tourne pas avec la voiture pendant l'accident ; en vue intérieure (V), on tourne avec elle.
- Dans l'eau profonde, l'accident s'arrête : la voiture coule, comme d'habitude. Une épave de la circulation disparaît quand B.J. est loin, comme les voitures qui circulent.

### Explosions

Une voiture explose quand une roquette explose à côté d'elle (6 m pour celle du joueur, 5 m pour celle d'Hitler ou du heavy robot), ou quand elle a brûlé 5 s (trop abîmée, ou couchée). Une voiture blindée encaisse 3 explosions avant d'exploser à la 4e.

- L'explosion fait jusqu'à 150 dégâts aux personnages à moins de 7 m, et jusqu'à 40 à B.J. (`degatsExplosion`).
- Les voitures à moins de 7 m explosent à leur tour : on peut faire sauter toute une file.
- Si B.J. est dedans, il est éjecté avant l'explosion.
- Celui qui la conduisait est tué : il tombe à côté, et compte comme un piéton ou un policier abattu, sauf si c'est une roquette d'Hitler ou du heavy robot.
- Toutes ses vitres volent en éclats, ses pièces partent en l'air et sa tôle s'enfonce des quatre côtés.
- Il reste une carcasse noire, qui brûle 12 s. Le souffle la fait voler en tournoyant (voir « Accidents »). On ne peut plus monter dedans. Elle disparaît au bout de 40 s, quand le joueur est à plus de 60 m.
- Une voiture en feu (trop abîmée, ou couchée sur le côté ou sur le toit) explose d'elle-même au bout de 5 s, blindée ou pas.

### Ce que les voitures ne font pas (encore)

Un conducteur blessé, mais pas tué, continue sa route comme si de rien n'était ; il ne sort pas non plus d'une voiture en feu (il meurt dans l'explosion). Il ne garde pas ses blessures quand il sort (tiré dehors par B.J., ou après un accident). Les voitures ne dérapent pas dans les virages. Les portes ne s'ouvrent pas. On ne voit personne dans les voitures fermées : seul le pilote d'un tricycle, d'une moto ou d'un Segway est visible. Il n'y a pas de klaxon, et les feux arrière ne s'allument pas plus fort au freinage.

## Missions et progression

Les 10 missions s'enchaînent dans l'ordre et rapportent 428 200 $ au total. Les 6 premières emmènent le joueur de la livraison d'un colis au combat final contre Hitler (18 200 $). L'argent gagné avant le bunker (3 000 $ une fois le pistolet payé) suffit pour s'offrir le fusil d'assaut ou le fusil de sniper, mais pas les deux. Les 4 suivantes sont les braquages : d'abord la voiture blindée pour s'enfuir, puis le musée, la bijouterie et la grande banque (voir « Braquages »).

| # | Mission | Étapes | Récompense |
| --- | --- | --- | --- |
| 1 | Le colis | Aller au point `a`, puis au point `b` dans le centre de Los Santos | 500 $ |
| 2 | Armé jusqu'aux dents | Acheter un pistolet à l'armurerie | 200 $ |
| 3 | Voleur de voitures | Amener une voiture dans un garage LS Customs (`G`, le plus proche) | 1 000 $ |
| 4 | Course-poursuite | Monter à 3 étoiles, puis semer la police | 1 500 $ |
| 5 | Opération bunker | Aller au point `d`, à Fort Zancudo, puis éliminer le Kommandant dans le bunker | 5 000 $ |
| 6 | Le château Wolfenstein | Éliminer Hitler dans le château, sur le mont Chiliad | 10 000 $ |
| 7 | Mad Max | Amener une voiture rapide (une Porsche) au garage LS Customs, puis payer le garagiste pour la blinder (5 000 $) | rien |
| 8 | Le musée d'art | Garer la voiture blindée devant le musée (`U`), voler le grand tableau, les 2 vitrines de bijoux, la couronne et les 2 statues, puis semer la police et rapporter le butin à la planque (la caravane de Trevor, `R`), dans la voiture blindée | 60 000 $ |
| 9 | La bijouterie Vangelico | Garer la voiture blindée devant la bijouterie (`V`), voler le gros diamant, puis semer la police et le rapporter à la planque | 100 000 $ |
| 10 | Le casse de la Pacific Standard | Garer la voiture blindée devant la banque (`Q`), passer les lasers, percer le coffre-fort, faire sauter la grille, prendre le pactole, puis semer la police et le rapporter à la planque | 250 000 $ |

Les premières missions restent dans Los Santos. Le bunker est à environ 2,5 km du garage, par la Great Ocean Highway ; le château est tout au nord. La planque des braquages, la caravane de Trevor à Sandy Shores, est à environ 2 km des trois bâtiments.

Pour tester une mission sans refaire les précédentes, le code de triche `MISSION` suivi d'un numéro y saute directement (voir « Codes de triche »).

Après la dernière mission, l'objectif affiche « Pays libre : fais ce que tu veux ! ».

### Types d'étapes

Une mission est une liste d'étapes. Chaque étape est validée dès que sa condition est vraie :

| Type | Condition |
| --- | --- |
| `aller` | Être à moins de 4 m du lieu. Un lieu est une lettre de la carte : s'il y en a plusieurs (un garage `G`), c'est la plus proche qui compte |
| `voiture` | Être en voiture à moins de 7 m du lieu. On peut exiger `rapide: true` (une voiture qui va à au moins `vitesseBlindable`), `blindee: true` (une voiture blindée) et `sansPolice: true` (0 étoile). Devant un pâté à braquer, le lieu est l'endroit où se garer, sur la place devant l'entrée |
| `eliminer` | Plus aucun personnage de ce type en vie (`soldat`, `boss` ou `hitler`) |
| `etoiles` | Avoir au moins ce nombre d'étoiles |
| `semer` | Revenir à 0 étoile |
| `arme` | Posséder l'arme nommée |
| `blindage` | Avoir une voiture blindée par le garagiste |
| `voler` | Tout le butin du pâté (lettre `lieu`) est dans le sac |

### Guidage

- Un point jaune sur la mini-carte montre l'objectif. Il reste collé au bord quand l'objectif est loin.
- Dans le monde, une colonne jaune lumineuse de 5 m marque le lieu, ou une flèche jaune flotte au-dessus de la cible à éliminer ou du butin à voler. Pendant un braquage, elle montre le plus proche de ce qu'on peut prendre ou actionner tout de suite (la perceuse, puis l'explosif, puis le pactole), et le garagiste pour la mission Mad Max.
- Le texte de l'étape s'affiche en bas de l'écran. À la fin, un bandeau annonce « MISSION RÉUSSIE » et la récompense.

### Argent

| Source | Montant |
| --- | --- |
| Missions | 200 à 250 000 $ |
| Hitler | 2 000 $ |
| Le Kommandant | 1 000 $ |
| Piétons tués | 10 à 69 $, 6 fois sur 10 |
| Objets volés dans les immeubles | 150 à 1 500 $ (tableau `TRESORS`) |
| Coffre de la banque | 2 000 $ et 3 étoiles ; il se remplit de nouveau au bout de 5 minutes |
| Mort | -100 $ |
| Blindage chez le garagiste | -5 000 $ |
| Masque à gaz | -500 $ |

### Mort

Quand la vie tombe à 0, l'écran passe en noir et blanc avec « WASTED » pendant 3,5 s. Le joueur se réveille devant l'hôpital le plus proche (il y en a 3 : Los Santos, Sandy Shores, Paleto Bay) avec toute sa vie, 100 $ de moins et 0 étoile. Il garde ses armes, ses munitions, son masque, le butin déjà dans son sac et sa progression dans les missions. S'il pilotait le heavy robot, il en est éjecté.

## Braquages

Trois bâtiments de Los Santos se braquent : le musée d'art (`U`), la bijouterie Vangelico (`V`) et la banque Pacific Standard (`Q`). Chacun a son alarme, ses gardes et son butin. On peut y entrer à toute heure : tant qu'on ne vole rien, qu'on ne tire pas et qu'on ne sort pas d'arme devant un vigile, rien ne se passe. Ils sont faits pour être réalistes et dangereux ; les missions 8 à 10 les enchaînent (voir « Missions »).

### Le butin

- On vole avec E, à moins de 2 m de l'objet. Un objet sous vitrine fait voler la vitre en éclats. Tout va dans le sac, qu'on voit sur le dos de B.J. ; on peut continuer à tirer.
- Le butin n'a pas de prix à l'objet : c'est la récompense de la mission qui le paie, quand on arrive à la planque (la caravane de Trevor) dans la voiture blindée, avec 0 étoile. Le sac se vide alors.
- Le butin volé ne revient pas. Mourir ne fait pas perdre le butin déjà dans le sac.

| Bâtiment | Butin |
| --- | --- |
| Musée d'art | Le grand tableau, une « Nuit étoilée » de 4,2 × 2,6 m (on découpe la toile, le cadre doré reste) ; la couronne en or à 8 pointes, sertie de rubis et de saphirs, sur un coussin de velours ; le collier de rubis ; les bagues en diamant ; la statue grecque en marbre, grandeur nature ; le chat égyptien en or |
| Bijouterie Vangelico | Le gros diamant, taillé en brillant, qui tourne et scintille sous sa cloche de verre |
| Banque Pacific Standard | Le pactole : deux palettes de liasses de billets, avec des lingots d'or dessus |

### L'alarme

L'alarme se déclenche quand on vole un objet, quand on pose la perceuse, quand on touche un laser, quand on blesse un vigile ou un chien, quand on tire à moins de 50 m de l'un d'eux, ou quand un vigile ou un chien voit B.J. à moins de 15 m avec une arme à feu à la main (pas en voiture).

- Les étoiles montent d'un coup : 4 pour le musée et la bijouterie, 5 pour la banque. Pendant une minute, les renforts de police arrivent 3 fois plus vite.
- Tous les vigiles et les chiens du bâtiment attaquent.
- On l'entend jusqu'à 250 m : une sonnerie à deux notes, hachée 16 fois par seconde. Les gyrophares du bâtiment (sur la façade et au plafond) clignotent en rouge, et une lumière rouge clignote dedans.
- Elle s'arrête quand on a semé la police (0 étoile) ou qu'on est mort ; les vigiles se calment.

### Les vigiles et les chiens

- **Les vigiles** (chemise grise, pantalon et casquette noirs) restent dans leur pâté. Ils ont chacun leur arme, pistolet, fusil à pompe, mitraillette ou fusil d'assaut, et visent bien (voir « Les ennemis »). Musée : 4 vigiles (dont un sur la place), banque : 3, bijouterie : 1 devant la porte.
- **Les chiens** (2 au musée) restent aussi dans leur pâté. En alerte, ils courent à 9 m/s, plus vite que B.J., et mordent (12 points toutes les 0,9 s). Ils ne mordent pas à travers une carrosserie : autour d'une voiture ou du robot, ils aboient.

### La bijouterie : la fumée toxique

Quand l'alarme sonne, des bouches au plafond lâchent une fumée verdâtre qui remplit la boutique en 5 s. Dedans, sans masque à gaz, B.J. tousse et perd jusqu'à 12 points de vie par seconde (`degatsFumee`) : le gilet ne protège pas. L'écran se voile de vert. Avec le masque à gaz (armurerie, 500 $), la fumée ne fait plus rien et le voile est léger. La fumée se dissipe en 15 s après l'alarme.

### La banque : lasers, mitrailleuses, coffre-fort

- **Le couloir des lasers** : derrière le hall, un couloir de 3,6 m de large et 11 m de long mène au coffre. 7 lasers rouges le barrent : 4 en travers (dont un à 35 cm du sol, à sauter, un à 1,35 m, à passer accroupi, et deux qui montent et descendent) et 3 debout, qui balaient le couloir de gauche à droite. Il faut passer entre eux, au bon moment.
- **Les mitrailleuses** : si B.J. touche un laser, l'alarme sonne et 3 mitrailleuses automatiques descendent du plafond (deux dans le couloir, une dans la salle du coffre). Elles suivent B.J. et tirent pendant 5 s (`dureeMitrailleuses`), 5 balles par seconde chacune, s'il est en vue. Debout, sans gilet, deux mitrailleuses font perdre environ 75 points en 5 s (on peut en mourir, avec un peu de malchance) ; accroupi, deux fois moins. On peut les détruire : 60 points chacune.
- **La perceuse thermique** : devant la porte ronde du coffre-fort (3,2 m, en acier, avec son volant à trois branches et ses 16 boulons), E pose une perceuse jaune sur son pied magnétique. Elle perce pendant 40 s (`dureePerceuse`), avec des étincelles et un bruit strident ; l'aide affiche le pourcentage. L'alarme sonne tout de suite : il faut tenir. Puis la porte pivote sur ses gonds en 3 s.
- **L'explosif** : derrière la porte, une grille de barreaux ferme la salle du coffre. E colle un pain de plastic avec son détonateur ; la diode clignote et bipe, de plus en plus vite, pendant 5 s (`dureeCharge`). L'explosion (rayon 5 m, jusqu'à 70 points pour B.J.) fait voler les 4 panneaux de la grille. Il faut s'éloigner !
- **Le pactole** est alors au fond, entre les murs de coffres de location.

## Codes de triche

Il y a deux sortes de codes de triche : ceux qu'on allume et qu'on éteint en retapant le code (un « effet » : presque tous changent l'apparence de B.J.), et ceux qui font une action tout de suite, pour tester le jeu. Parmi les premiers, `Z6PO`, `DIEU` et `SUPERMAN` changent aussi le jeu. Entrée ouvre une case « Code : » ; on tape le code, puis Entrée. Pendant la saisie, les touches ne font plus bouger le joueur. Entrée ne fait rien quand la grande carte est ouverte. Un mauvais code affiche « Code inconnu ». Les chiffres se tapent avec ou sans Maj : sur un clavier français, la touche 6 donne « 6 » et non « - », et la touche 8 donne « 8 » et non « _ ».

Dans le menu, sous ⚙ Réglages, le bouton **🎮 Codes de triche** déplie la liste de tous les codes : une ligne par code du tableau `TRICHES`, avec ses autres noms (« IDKFA, ARMES, WAFFEN, WEAPONS ») en jaune, puis son `texte` dans la langue choisie. Au-dessus, une phrase rappelle comment taper un code et comment l'annuler. La liste se fabrique toute seule au chargement : un code ajouté au tableau y est aussi. Elle marche au départ comme en pause (Échap), et cliquer dedans ne lance pas le jeu.

| Code | Effet |
| --- | --- |
| `DIEU`, `GOD`, `GOTT` ou `IDDQD` | Invincible (`IDDQD` : comme dans *Doom*) : les balles, les roquettes, les explosions, les morsures et la fumée toxique ne lui font plus rien ; la vie et le gilet ne baissent plus. B.J. est habillé en Zeus : cheveux blancs, longs dans le cou, moustache et grande barbe blanche en pointe ; torse, bras et jambes nus ; un pagne en paille, tenu par une corde ; des santiags en cuir brun (tige découpée en V, avec des coutures claires, bout pointu, petit talon). Il a aussi les deux super-pouvoirs décrits plus bas : les yeux laser, et la chute qui écrase. Retaper un des quatre noms le rend mortel à nouveau, lui reprend ses pouvoirs et le rhabille |
| `SUPERMAN` | Le costume de Superman : collant bleu (torse, bras et jambes), slip rouge, ceinture jaune, bottes rouges qui montent sur le mollet, l'écusson jaune bordé de rouge avec son « S » sur la poitrine, une cape rouge qui tombe jusqu'aux mollets, les cheveux noirs et un accroche-cœur sur le front. Il a les deux super-pouvoirs décrits plus bas (les yeux laser, la chute qui écrase), mais il n'est pas invincible : les balles et les explosions lui font mal |
| `SLIP` | En slip : jambes nues, slip blanc |
| `CHAUSSURE` | Perd la chaussure gauche (il reste la chaussette blanche) |
| `SOUTIF` | Torse et bras nus, soutien-gorge rose : deux bonnets bordés de dentelle claire, un petit nœud entre les deux, une bande autour du torse avec son agrafe dans le dos, et deux bretelles qui passent sur les épaules |
| `JAMBEDEBOIS` | Jambe droite en bois, sans chaussure |
| `BARCA` | Maillot du Barça à rayures bleues et grenat |
| `BEBE` | Deux fois plus petit, avec une grosse tête, tout nu avec une couche blanche |
| `GOKU` | San Goku en Super Saiyan : kimono orange déchiré en haut, l'épaule droite nue, t-shirt bleu qui dépasse au col et à la manche gauche, ceinture, bracelets et bottes bleus. Ses cheveux dorés se dressent en 13 pics, et une aura dorée l'entoure, avec des flammes qui montent |
| `Z6PO` ou `C3PO` | Z6PO, le robot doré : tout en or, la tête chauve avec deux yeux orange qui brillent et une bouche en fente, des fils gris à la taille, le bas de la jambe droite en argent. Il bouge comme un robot, va 0,6 fois moins vite, et les balles lui font moitié moins mal |
| `IDKFA`, `ARMES`, `WAFFEN` ou `WEAPONS` | Comme dans *Doom* : toutes les armes (bazooka compris), au moins 3 fois leurs munitions, le gilet pare-balles plein et le masque à gaz |
| `RICHE` | Donne 100 000 $ d'un coup, pour tester ce qui coûte cher (le blindage, les armes) |
| `MISSION` suivi d'un numéro | Saute à cette mission, à sa première étape (`MISSION8` : le musée ; `MISSION11` : pays libre). Le sac est vidé. Si la mission a besoin d'une voiture blindée et qu'il n'y en a pas, une Porsche blindée apparaît à 5 m de B.J. |

**Z6PO** (`C3PO` est un autre nom pour le même code : taper l'un annule l'autre) :

- **Il bouge comme un robot** : sa pose ne change que 8 fois par pas, par à-coups. Il fait de petits pas, les genoux presque raides, les coudes pliés et les bras un peu écartés, qui bougent à peine. Il ne se penche pas pour courir, mais se dandine d'un pied sur l'autre. Il se tourne par crans d'environ 11°.
- **Plus lent** : toutes ses allures sont multipliées par 0,6 (`vitesse`) : 2,4 m/s en marchant, 4,8 m/s en courant, et même la nage et le moonwalk. En voiture ou dans le heavy robot, rien ne change.
- **Plus solide** : les balles lui font moitié moins mal (`balles`) : celles des policiers, des soldats, du Kommandant, des vigiles, des policiers d'élite, des mitrailleuses de la banque et de la mitrailleuse du heavy robot. Les roquettes, les explosions et les morsures de chien, non.

**Les super-pouvoirs de SUPERMAN et de DIEU** (dans le tableau `TRICHES`, `laser: true` et `ecrase: true`) :

- **Les yeux laser** : une arme de plus, sur la touche 9 (voir « Les armes »). Elle s'en va quand on annule le code ; si B.J. l'avait en main, il repasse aux poings. Si l'autre code est encore allumé, il la garde.
- **La chute qui écrase** : tomber de plus de 4 m (`hauteurSansMal`) ne fait plus mal. B.J. se reçoit sur un genou, le poing au sol, comme un super-héros, et reste ainsi 0,9 s ; il ne fait jamais de roulade. Tout ce qui est autour de lui prend le choc, dans un rayon de 0,3 m par mètre de chute (`rayonEcrase`), entre 2 m et 8 m (`rayonEcraseMax`) : 2 m pour une chute de 5 m, 6 m pour 20 m, 8 m à partir de 27 m. La caméra tremble, et un grondement sourd retentit.
  - **Les gens** : chacun perd 400 points (`degatsEcrase`) s'il est juste dessous, de moins en moins vers le bord (400 × la part du rayon qui reste), et vole loin de B.J., à la renverse, comme soufflé par une explosion. Un piéton meurt jusqu'à 87 % du rayon, un policier jusqu'à 82 %, un soldat jusqu'à 77 % ; le Kommandant (450 points) et Hitler (900) y survivent. Ça compte comme si B.J. les avait tués : une étoile par piéton ou policier. Mesuré, d'une chute de 25 m (7,5 m à la ronde) : les piétons à 1,2 m et 3 m sont tués, celui à 9 m n'a rien.
  - **Les voitures** : celles dont la carrosserie est à moins de 40 % du rayon (3 m pour une chute de 25 m) ont le toit aplati d'un bout à l'autre, comme sous le heavy robot : les vitres éclatent, le conducteur est tué, elles prennent feu et explosent au bout de 5 s (B.J. n'est pas à l'abri de l'explosion, sauf avec `DIEU`). Les autres, jusqu'au bord du rayon, sont soulevées et partent en accident (au plus 60 % du souffle d'une explosion). Une voiture blindée ne s'écrase pas : elle est seulement soulevée. Les bateaux, les avions, les hélicoptères, les skis et les carcasses brûlées ne bougent pas.
  - **Le heavy robot** : sa vitre prend jusqu'à 400 points (elle en tient 350). Mesuré : B.J. tombe de 30 m à 3 m du robot, la vitre perd 325 points.
  - **Le sol** : il se fissure en toile d'araignée sur 70 % du rayon, autour d'un creux noirci ; 9 plaques se soulèvent autour, des gravats volent et de la poussière monte. Les fissures suivent le sol (un trottoir, une pente, des marches). Elles s'effacent au bout de 2 minutes.
  - **Les toits** : de plus de 10 m (`hauteurCasseToit`), B.J. casse le toit ou le plancher où il tombe, s'il y a une pièce dessous (un bâtiment ou un immeuble où l'on entre) : la dalle doit être mince (65 cm au plus ; ou deux dalles l'une sur l'autre, 1 m au plus en tout : le toit d'un magasin est posé sur son plafond), large d'au moins 1,5 m (le palier d'un escalier de secours est trop étroit), avec 1,80 m de vide dessous, sans meuble haut juste dessous. Il passe au travers avec la moitié de sa vitesse, et retombe à l'étage du dessous, où ça recommence : il écrase ce qui s'y trouve, et peut casser aussi ce plancher. Le trou est carré, de 1,8 à 3 m de côté selon la hauteur de la chute, et il reste : on y retombe en marchant dessus. D'en haut, on le voit noir, avec des bords déchiquetés ; d'en dessous, clair (le jour qui entre). Mesuré sur un immeuble de 4 étages : de 8 m au-dessus du toit, le toit se fissure sans casser ; de 12 m, B.J. traverse le toit et s'arrête au dernier étage ; de 40 m, il traverse aussi un plancher (il s'arrête deux étages sous le toit) ; de 200 m, deux planchers (trois étages sous le toit) ; en marchant ensuite vers un trou du toit, il y retombe. Sur une supérette, de 15 m : il traverse le toit et le plafond, et tombe dans le magasin (au-dessus d'un rayon, le toit se fissure seulement). Un toit plein (une tour, une maison, 4 immeubles sur 5, l'hôpital) ne casse pas : il se fissure comme le sol.
  - **Dans l'eau profonde**, rien : B.J. nage, comme d'habitude.

Les codes à action se retapent autant qu'on veut ; un nombre tapé juste après le code lui est donné (`MISSION8`). Retaper un code d'apparence annule son effet. Les effets se combinent : B.J. est remis dans sa tenue normale, puis chaque code actif est appliqué dans l'ordre du tableau (Z6PO passe donc tout en or, même le kimono de Goku, mais ce que Goku ajoute reste : les pics de cheveux, les bracelets, le haut des bottes et l'aura). `DIEU` est le premier du tableau : les autres codes s'ajoutent par-dessus la tenue de Zeus (avec `SOUTIF`, Zeus porte le soutien-gorge ; avec `Z6PO`, il est tout en or, mais garde sa barbe, son pagne et la tige de ses santiags). `SUPERMAN` est le deuxième : avec `DIEU`, c'est un Superman à barbe blanche, en pagne de paille ; avec `SLIP`, il a les jambes nues et un slip blanc ; avec `Z6PO`, il est tout en or, mais garde son écusson, sa cape et le haut rouge de ses bottes. Ils durent même après une mort, mais pas après un rechargement de la page. À part Z6PO, DIEU et SUPERMAN, les codes d'apparence ne changent rien au jeu : la caméra reste à hauteur d'adulte pour le bébé, et l'arme vue en 1re personne ne change pas. Les codes sont dans le tableau `TRICHES`, en haut de `index.html`.

Dans ce tableau, un code a un `texte` (l'annonce, qui le décrit aussi dans la liste du menu ; celui de `MISSION` n'est jamais annoncé et ne sert qu'à la liste) et un `effet` (ce qu'il change sur B.J.) ou une `action` (ce qu'il fait tout de suite). Il peut avoir un `alias` (un autre nom, ou une liste d'autres noms : `['ARMES', 'WAFFEN', 'WEAPONS']`), une `vitesse` et des `balles` (des nombres qui multiplient ses allures et les dégâts des balles ; s'il y a plusieurs codes actifs, ils se multiplient entre eux), `robot: true` (il bouge par à-coups), `invincible: true` (`blesserJoueur` et la fumée ne font plus rien), `laser: true` (il a les armes qui ont `laser: true` dans `ARMES` : les yeux laser) et `ecrase: true` (tomber de haut ne lui fait rien, et écrase ce qu'il y a dessous).

## Interface et son

L'écran reprend la disposition de GTA 5 : mini-carte ronde en bas à gauche, argent et étoiles en haut à droite. Tous les sons sont fabriqués par le programme ; il n'y a aucun fichier audio.

### Éléments à l'écran

| Emplacement | Élément | Détail |
| --- | --- | --- |
| Bas gauche | Mini-carte | Ronde, elle tourne avec la caméra. Elle dézoome en voiture ou en bateau, deux fois plus en avion ou en hélicoptère. |
| Bas gauche | Barre de vie | Verte, rouge sous 30 points |
| Bas gauche | Barre du gilet | Bleue, sous la barre de vie, seulement quand on porte un gilet |
| Haut droite | Argent | En gros chiffres verts, les milliers séparés (« 250 000 $ ») |
| Haut droite | Étoiles | 5 étoiles, qui clignotent en bleu quand la police voit le joueur |
| Haut droite | Arme et munitions | Nom de l'arme, nombre de balles ou de roquettes (rien pour les poings, le couteau et les yeux laser). Dans le heavy robot : « Heavy robot », ses balles et ses roquettes |
| Haut gauche | Aide | « Appuie sur E pour… » près d'un stand, d'un ascenseur, d'un véhicule (avec son nom : « monter : Porsche », « monter : Hélicoptère »), du garagiste, du butin, de la porte du coffre, de la grille ou du heavy robot, au départ d'une remontée (à pied ou à ski : « prendre le télésiège », « prendre la télécabine »), et dessus (« sauter du télésiège », « sauter de la cabine »). Pendant le perçage du coffre, à moins de 40 m : « Perceuse thermique : 63 % ». Au pied d'une échelle : « Avance contre l'échelle pour grimper » |
| Bas centre | Objectif | Texte de l'étape de mission en cours |
| Centre | Viseur | Un point blanc, avec une arme à feu, en visant, en 1re personne ou dans le heavy robot. Caché dans la lunette et en nageant |
| Plein écran | Lunette | Un rond avec deux traits en croix et du noir autour, en visant avec le fusil de sniper. Le reste de l'écran (mini-carte, argent) s'affiche par-dessus |
| Haut centre | Annonces | « MISSION RÉUSSIE », « +50 vie », « Gilet pare-balles ! », « Tu as semé la police ! », « BRAQUAGE ! », « WHO'S BAD ? », « SAUT ! 35 m », « LOOPING ! », « Pas assez d'élan ! », « AU FEU ! » (voiture en feu), « Voiture réparée ! », « MAD MAX ! », « ALARME ! », « BUTIN ! », « LASER TOUCHÉ ! », « COFFRE-FORT PERCÉ ! », « BOUM ! », « HEAVY ROBOT ! », « MISSION 8 », le nom du véhicule dans lequel on monte (« PORSCHE »), « AVION », « HÉLICOPTÈRE », « SKIS », « SNOWBOARD » et « LUGE » avec leurs commandes, « Pose-toi d'abord ! », ce que dit le garagiste, « Montre en or volé ! +400 $ », « + munitions pour tes armes », « Boisson énergisante ! », « Pot-de-vin ! », « 88 MILES À L'HEURE ! » |
| Bas droite | Compteur | Vitesse en km/h, en voiture seulement (à ski, en snowboard et en luge aussi, à l'horizontale) ; en vol, la hauteur en plus (« 216 km/h · 85 m ») ; sur le boardercross, le chronomètre en plus (« 62 km/h · 12.4 s ») |
| Plein écran | Bords rouges | Quand le joueur est touché |
| Plein écran | Fumée | Un voile vert-gris dans la fumée toxique de la bijouterie, léger avec le masque à gaz |
| Plein écran | WASTED | Noir et blanc à la mort |
| Plein écran | Grande carte | Tout le pays, avec la touche M, et sa légende |
| Centre | Code de triche | « Code : … » pendant la saisie |

**La mini-carte** montre le terrain vu du ciel (herbe, forêt, désert, sable, roche, avec les montagnes éclairées depuis le nord-ouest), la mer et les lacs en bleu, les routes, les rues, les pistes, les pâtés et leurs bâtiments. Des ronds de couleur marquent les lieux :

| Rond | Lieu | Rond | Lieu |
| --- | --- | --- | --- |
| A orange | Armurerie | F vert | Maison de Franklin |
| + rouge | Hôpital | M bleu | Villa de Michael |
| P bleu foncé | Commissariat | T orange | Caravane de Trevor |
| G violet | LS Customs | Y jaune | Yellow Jack |
| $ vert | Banque | Z rouge foncé | Tour Maze Bank |
| S vert | Supérette | B noir | Bunker |
| E rouge | Station-service | W rouge foncé | Château Wolfenstein |
| C orange | Départ d'une piste de cascades | U brun | Musée d'art |
| V doré | Bijouterie Vangelico | Q vert foncé | Banque Pacific Standard |
| ❄ bleu | Station de ski | | |

 Les pistes de cascades sont des traits orange, les remontées des traits tiretés bleu foncé, les pistes de ski des traits de leur couleur (bleu, rouge, noir, ou jaune pour un hors-piste). La neige des sommets est blanche. Le quartier de chaque gang (son pâté et la moitié des rues autour) est colorié de sa couleur. Les ennemis en alerte (dont les vigiles et les chiens) sont des points rouges ; les policiers et voitures de police clignotent en rouge et bleu. Le heavy robot est un gros point, rouge et bleu avec son pilote, gris sans. La flèche blanche du joueur est au centre.

**La grande carte** s'ouvre et se ferme avec la touche M. Elle couvre tout l'écran et met le jeu en pause : rien ne bouge tant qu'elle est ouverte.

- Le nord est en haut, comme dans le tableau `CARTE`. La carte ne tourne pas.
- À l'ouverture, on voit tout le pays. La molette zoome jusqu'à 6 pixels par mètre, et le zoom avant amène sur le joueur.
- La souris, les flèches ou Z Q S D déplacent la vue, sans sortir de la carte.
- Elle montre les mêmes choses que la mini-carte. Tant qu'on n'a pas trop zoomé, elle écrit le nom des villes et des régions (tableau `NOMS_LIEUX`, et le nom de chaque sommet du tableau `SOMMETS`) ; en zoomant, elle écrit aussi le nom de chaque rond.
- **La légende**, à gauche, dans un cadre sombre : chaque sorte de rond (armurerie, hôpital... jusqu'au départ des pistes de cascades), avec son nom, puis le point jaune de l'objectif, la flèche du joueur (« Toi »), les points de la police (rouge et bleu) et des ennemis (rouge), et un carré de la couleur de chaque gang (« Gang Ballas »). Elle reste affichée quel que soit le zoom. Ses ronds viennent du tableau `ICONES` : un nouveau rond y apparaît tout seul. Si la fenêtre est basse, ses lignes se serrent.
- En haut à droite, elle dit dans quelle colonne et quelle ligne du tableau `CARTE` se trouve le joueur : pratique pour modifier la carte à cet endroit.
- La flèche blanche indique où regarde le joueur, ou dans quel sens roule sa voiture. L'objectif est un point jaune entouré d'un anneau qui bat, et son texte est rappelé en haut à gauche.
- Échap ferme la carte et affiche le menu de pause.

**Le menu** affiche le titre et, juste en dessous, le numéro de version (`#version` : le nombre de commits de `main` sur GitHub, demandé au chargement ; il augmente donc tout seul à chaque mise en ligne. Le dernier numéro reçu est gardé dans le `localStorage` du navigateur, et affiché tout de suite, en attendant la réponse de GitHub ou à sa place s'il ne répond pas), les boutons des langues, les deux lignes de boutons de la foule (piétons et voitures, voir « La population »), le bouton ⚙ Réglages, le bouton 🎮 Codes de triche (voir « Codes de triche »), une phrase d'histoire (« Tu es B.J. Blazkowicz… »), la liste des touches et « Clique pour jouer ». Échap libère la souris et ramène ce menu en mode pause.

### L'écran des réglages

Dans le menu, sous les boutons de la foule, le bouton **⚙ Réglages** déplie un écran qui montre les nombres des tableaux `REGLAGES`, `ARMES`, `ARMES_ROBOT`, `VOITURES` et `ENNEMIS`, sans ouvrir le code. Il marche au départ comme en pause (Échap). Cliquer dedans ne lance pas le jeu.

- Chaque tableau est un groupe qui se déplie ; chaque arme, voiture ou ennemi aussi, sous son nom (traduit), et le son du moteur de chaque voiture. Une case porte le nom de la valeur dans le code (`vitesseMarche`, `degats`…) : on la retrouve facilement dans `index.html`.
- Un nombre se tape dans une case, `true` ou `false` est une case à cocher, une liste (`policiers`, `couleurs`, `tir`, `touchesDanse`) s'écrit avec des virgules. Une liste de nombres où se glisse autre chose s'encadre de rouge et ne compte pas.
- Les noms et les modèles (`nom`, `modele`, `vole`) n'y sont pas : un mauvais modèle empêcherait le jeu de marcher. Ils se changent dans le code.
- Le jeu en tient compte tout de suite, sauf pour ce qu'il construit ou calcule au lancement, qui attend F5 : le relief (`hauteurMontagnes`), les immeubles visitables, les dos d'âne, les bornes, les ombres, la distance de vue, l'argent et la vue de départ, les touches de la danse, et les ennemis déjà placés (nazis, vigiles, gangs), dont la vie et l'arme sont fixées quand ils apparaissent.
- Une case changée est jaune, et le bouton ⚙ est bordé de jaune tant qu'il reste un changement. Le navigateur s'en souvient (`localStorage.reglages`) : pour chaque case changée, il garde le nombre du code et celui du menu. Au lancement, il ne remet le nombre du menu que si le code a toujours le même nombre : si on change ce nombre dans `index.html`, c'est le code qui gagne, et le menu l'oublie.
- Remettre le nombre du code dans une case enlève le jaune. **Tout remettre** revient d'un coup à tous les nombres du code, sans recharger la page (ce qui est construit au lancement attend F5).
- L'écran est construit avant le pays : si un réglage empêche le jeu de démarrer (par exemple une arme qui n'existe pas dans `ENNEMIS`), il marche quand même, et Tout remettre répare.

### Langues

Le jeu parle 4 langues : français, allemand (Deutsch), anglais (English) et züritüütsch, l'allemand de Zurich. On choisit avec 4 boutons, sous le titre du menu ; celui de la langue choisie est jaune. Cliquer sur un bouton change la langue tout de suite, sans lancer le jeu. Les boutons marchent dès l'ouverture de la page, pendant le chargement, et aussi dans le menu de pause. Le navigateur se souvient de la langue pour la prochaine fois. Au tout premier lancement, le jeu est en français.

- **Ce qui est traduit** : le menu (dont les boutons de la foule), les objectifs et les noms des missions, l'aide (« Appuie sur E… »), les annonces, ce que dit le garagiste, les noms des armes, des véhicules, du butin et des objets à voler, les munitions, les annonces des codes de triche (et donc leur liste dans le menu), les noms des lieux, les textes et la légende de la grande carte, les prix au-dessus des stands de l'armurerie, et les enseignes des bâtiments : ARMURERIE (WAFFENLADEN, GUN SHOP, WAFFELADE), POLICE (POLIZEI en allemand et en züritüütsch, aussi sur les fourgons blindés et le heavy robot), BANQUE, ESSENCE et le musée d'art.
- **Les touches** : en allemand, en anglais et en züritüütsch, le menu écrit W A S D au lieu de Z Q S D : ce sont les mêmes touches, sur un clavier QWERTZ ou QWERTY.
- **L'argent** s'écrit à la façon de chaque langue : « 250 000 $ », « 250.000 $ », « 250,000 $ », « 250'000 $ ».
- **Ce qui ne change pas** : les codes de triche (`SLIP`, `GOKU`...), les noms propres (Los Santos, Porsche, LS Customs, Bazooka...), « WASTED », « MISSION 8 », « Heavy robot », les enseignes qui sont des noms propres (24/7, LS CUSTOMS, YELLOW JACK, MAZE BANK, VANGELICO, PACIFIC STANDARD) et les alertes pour le bidouilleur.
- Les traductions sont dans le tableau `TRADUCTIONS`, une ligne par phrase française avec ses trois traductions. Une phrase absente du tableau reste en français. Dans une phrase, `{prix}`, `{n}`, etc. sont remplacés par un nombre ou un nom ; une traduction peut les déplacer, ou en laisser tomber un (l'allemand ne répète pas le nom de la voiture chez le garagiste).

### Sons

- **Armes** : chaque arme à feu a son propre coup de feu. Les tirs ennemis s'entendent moins fort de loin.
- **Yeux laser** : un grésillement, une note en dents de scie qui descend de 2 400 à 1 700 Hz à chaque tir (15 par seconde), sans coup de feu.
- **Explosions** : un gros boum grave, plus faible de loin.
- **Chute qui écrase** (codes `SUPERMAN` et `DIEU`) : un grondement sourd de près d'une seconde.
- **Moteur** : chaque type de véhicule a le sien (tableau ci-dessous) : deux notes (celle du moteur, et la même une octave plus bas) et un souffle haché par la note basse, un « tchk » à chaque tour, comme les explosions dans les cylindres (le crépitement). Le son monte dans chaque rapport, puis retombe quand on passe le suivant : pendant 0,2 s, le moteur baisse à 30 % de sa force, comme quand on lève le pied pour passer la vitesse. Il est plus fort et plus clair quand on accélère que quand on lève le pied.
- **Claquements** : quand on lâche l'accélérateur au-dessus de la moitié du régime, l'échappement claque pendant 0,6 s, un claquement toutes les 0,04 à 0,19 s (pas pour un avion ni un hélicoptère). En passant la vitesse suivante, il claque aussi une fois, moitié moins fort.
- **Rauque** : ce chiffre (de 0 à 1) fait tout le caractère du moteur. Plus il est grand, plus le son est clair et résonne, plus il crépite (force : 2,5 × √rauque) et plus il claque (volume : 0,6 × rauque²). À 0 (Segway), ni crépitement ni claquement ; sous 0,13 (Rolls-Royce, limousine), pas de claquement.
- **Voitures des autres** : on entend le moteur de la voiture qui roule le plus près, à moins de 40 m. Il vient de son côté (à gauche ou à droite de la caméra), il monte quand elle approche et descend quand elle s'éloigne (effet Doppler, avec le son à 340 m/s : environ 4 % pour une voiture à 15 m/s), et il devient sourd de loin (à 40 m, le filtre ne laisse passer que 40 % des aigus d'à côté).
- **Roulement et pneus** : un souffle grave qui monte avec la vitesse, un crissement au frein à main au-dessus de 22 km/h, un bruit de choc, un « pan » quand un pneu crève.
- **Lampadaire renversé** : un choc métallique qui descend (« clang »).
- **Glisse** : les skis, le snowboard et la luge n'ont pas de moteur : on n'entend que le souffle du roulement, qui monte avec la vitesse. Un petit bip quand B.J. s'assoit sur une remontée, un autre au départ et à l'arrivée du boardercross.
- **Dégâts** : un bruit de tôle, d'autant plus fort que le choc est fort ; un tintement quand une vitre se fêle, un bruit de verre quand elle se brise ; un choc sourd quand la voiture retombe trop fort.
- **Pause** : le menu et la grande carte coupent tous les sons.
- **Police** : sirène à deux tons, plus forte quand la voiture approche.
- **Signaux** : bips pour un achat, un objet ramassé, une étape réussie, une blessure, la mort.
- **Braquages** : la sonnerie de l'alarme ; le tintement et le fracas d'une vitrine brisée ; la toux dans la fumée toxique ; le crissement de la perceuse thermique ; les bips de l'explosif, de plus en plus rapides ; les rafales des mitrailleuses automatiques ; les aboiements des chiens.
- **Blindage** : le « piou » d'une balle qui ricoche sur une voiture blindée ou sur le heavy robot ; le bruit de la soudure chez le garagiste.
- **Heavy robot** : un bruit sourd à chaque pas ; sa mitrailleuse, plus grave que les autres ; ses roquettes, comme celles du bazooka.
- **Danse** : le petit cri de Michael Jackson (« hi-hiii ! ») au début de la toupie, un bruit sec quand B.J. prend la pose. Le cri dure une demi-seconde : une voix de tête en deux fois, un « hi » court vers 900 Hz, le souffle du « h », puis un « hiii » plus long vers 1 050 Hz. Chaque fois, la voix monte d'un coup, tremble un peu et retombe à la fin.

| Type | Note au ralenti | Note à fond | Rapports | Rauque (0 à 1) | Volume | Caractère |
| --- | --- | --- | --- | --- | --- | --- |
| Classique | 50 Hz | 190 Hz | 4 | 0,3 | 0,05 | Moteur ordinaire |
| Porsche | 75 Hz | 340 Hz | 6 | 0,9 | 0,06 | Aigu, il hurle |
| Minibus | 38 Hz | 125 Hz | 4 | 0,5 | 0,05 | Grave, il pétarade |
| 4x4 du désert | 30 Hz | 130 Hz | 4 | 0,7 | 0,07 | Très grave et fort |
| Limousine | 40 Hz | 140 Hz | 5 | 0,1 | 0,04 | Feutré |
| Tricycle | 45 Hz | 260 Hz | 3 | 1 | 0,04 | Mobylette |
| Moto | 70 Hz | 420 Hz | 6 | 0,95 | 0,06 | Aigu et rageur, il crépite et claque |
| Segway | 180 Hz | 520 Hz | 1 | 0 | 0,02 | Un petit sifflement électrique, sans crépitement |
| DeLorean | 55 Hz | 210 Hz | 5 | 0,4 | 0,05 | Moteur ordinaire, un peu plus aigu |
| Coccinelle | 45 Hz | 180 Hz | 4 | 0,6 | 0,05 | Grave, il pétarade |
| Skoda Kodiaq | 42 Hz | 170 Hz | 7 | 0,2 | 0,045 | Doux, beaucoup de rapports |
| Audi TT | 60 Hz | 280 Hz | 6 | 0,5 | 0,05 | Sportif |
| Lamborghini | 70 Hz | 380 Hz | 7 | 1 | 0,07 | Il hurle, crépite et claque fort |
| Rolls-Royce | 35 Hz | 130 Hz | 8 | 0,05 | 0,035 | Le plus silencieux : presque pas de crépitement, pas de claquement |
| Audi Quattro de rallye | 65 Hz | 330 Hz | 5 | 1 | 0,07 | Il hurle, pétarade et claque fort |
| Austin Mini | 55 Hz | 240 Hz | 4 | 0,5 | 0,045 | Petit moteur nerveux |
| Voiture de police | 50 Hz | 210 Hz | 4 | 0,4 | 0,05 | Comme la classique, un peu plus aigu |
| Fourgon blindé | 28 Hz | 120 Hz | 5 | 0,8 | 0,07 | Très grave, rauque et fort |
| Hors-bord | 40 Hz | 150 Hz | 1 | 0,6 | 0,06 | Grave, sans changer de rapport |
| Jet-ski | 60 Hz | 280 Hz | 1 | 0,9 | 0,05 | Aigu, il pétarade |
| Avion | 110 Hz | 320 Hz | 1 | 0,4 | 0,07 | Il siffle de plus en plus aigu avec la vitesse |
| Hélicoptère | 14 Hz | 24 Hz | 1 | 1 | 0,09 | Un battement grave (« tchop tchop »), qui suit le rotor et non la vitesse |

Polices de caractères : Anton pour les titres et les chiffres, Roboto Condensed pour le texte (Google Fonts).

## Architecture technique

Tout le jeu tient dans `index.html`, environ 7 900 lignes. Il n'y a ni installation, ni compilation, ni fichier image ou son. Le moteur 3D [Three.js](https://threejs.org) 0.186 est chargé depuis Internet (jsDelivr). Le site est publié par GitHub Pages depuis la branche `main`.

### Plan du fichier

| Lignes | Partie | Rôle |
| --- | --- | --- |
| 1–136 | HTML et CSS | Interface et menu, avec les boutons des langues et de la foule, l'écran des réglages (`#reglages`) et la liste des codes de triche (`#triches`) |
| 137–515 | **Foule et langues** (zones à modifier) | `FOULES` et le choix de la foule (`foule`) ; `LANGUES`, `TRADUCTIONS` ; `tr`, les boutons du menu (`traduireMenu`, `etat`), le numéro de version. Un script à part, qui tourne avant le module du jeu |
| 516–529 | Chargement | Three.js et ses modules |
| 530–1212 | **Zones à modifier** | `REGLAGES`, `ARMES` (dont les yeux laser), `TRESORS`, `ARMES_ROBOT`, `VOITURES`, `ENNEMIS`, `CARTE`, `SOMMETS`, `REMONTEES`, `PISTES_SKI`, `NOMS_LIEUX`, `GANGS`, `MISSIONS`, `CASCADES`, `TENUES_GLISSE`, `TRICHES` (et, juste après, la liste des codes du menu, faite à partir du tableau) |
| 1213–1280 | Écran des réglages | Les tableaux qu'il montre (`TABLEAUX`), leur copie avant les changements (`DU_CODE`), les nombres retenus par le navigateur (`changes`, `sauverReglages`), les groupes et les cases (`groupeReglages`, `champReglage`), Tout remettre |
| 1281–1813 | Outils, géographie | Calculs ; hauteur des cases et des villes, sommets (`sommetEn`), pistes de ski (`grilleSki`, `pisteSkiEn`, leur relief : `reliefSki`), neige (`neigeEn`), relief (`terrainNaturel`, `hauteurTerrain`), lieux, rues, réseau des routes (`NOEUDS`, `ROUTES`), dos d'âne (`dosH`, `dosV`, `dosRoute`, `dosDAneEn`) ; pistes de cascades (`PISTES`, `RAILS`, `pisteSous`) ; tracé des remontées (`remontee`, `TELESIEGES`, `pointCable`, `presDeRemontee`) |
| 1814–2107 | Moteur 3D, textures | Scène, lumières, ciel ; façades, sols, routes, pistes, fêlures, vitres brisées, panneaux, visages, marbre, tableaux, coffres, billets, tôle rouillée, dos d'âne dessinés par le programme ; enseignes dans la langue choisie (`enseigne`, `majEnseignes`) ; matières |
| 2108–3301 | Construction du pays | Morceaux, intérieurs (`interieurs`), boîtes, bâtiments visitables (`batiment`), immeubles où l'on entre (`immeubleI`, `meubler` et ses meubles, `cachettes`, `echelle`, `escalierDehors`), pâtés (`genererBloc`, dont les trois pâtés à braquer, le garagiste, les bornes des places et la station de ski), rues et dos d'âne, routes et ponts, pontons, pistes d'aéroport (avions et hélistations), pistes de cascades, terrain (et sa neige) et végétation (et les sapins givrés), remontées (gares, pylônes et poulies, câble, sièges et garde-corps, cabines), balisage des pistes de ski, panneaux et relief en neige (`pointPiste`, `bandeNeige`), eau, fusion (`fusionner`) ; bornes (`bornesSous`) et lampadaires qui tombent (`faucher`, `renverserLampadaire`, `majLampadaires`) ; ce qu'on dessine (`majMorceaux`) |
| 3302–3398 | Collisions et sol | `resoudre`, `hauteurSol`, ligne de vue (`voit`, `butee`, `traversee`), balles des ennemis arrêtées par les murs (`balleArrive`), rayons contre le terrain |
| 3399–3751 | Personnages | Corps articulés, bâtons de ski (`batons`), pièces des codes de triche (`accessoire` ; la cape et le blason de Superman : `GEO.cape`, `GEO.blason`), animations (dont la nage, les trois pas de la danse, la marche raide de Z6PO, le vol de Superman, les sauts, l'atterrissage sur un genou, la roulade et les chutes, les poses à ski, en snowboard et en luge, pousser, la main sur la neige ; `poserCorps`, `poseMort`, `hauteurCouche`), membres qui ont du poids (`MOUS`, `membresMous`), armes en 3D |
| 3752–4264 | Voitures, bateaux, avions | Outils pour fabriquer les pièces, coque des bateaux, forme des 24 modèles (`MODELES`, dont le fourgon blindé, la moto, le Segway, l'avion, l'hélicoptère, les skis, le snowboard et la luge), pièces qui partent, carrosserie, cabine, roues, pales (`rotors`), blindage Mad Max (`formesBlindage`, `estBlindee`), `pasDeTole`, `habillerVoiture` |
| 4265–4452 | Dégâts des voitures | `abimer` (et le feu quand c'est trop : `pireDegat`), formes découpées fin (`copieCabossable`), bosses (`bosseler`, `pli`), vitres, pièces qui partent (`detacher`), roues tordues, pneus crevés (`crever`), morceaux qui volent (`debris`) |
| 4453–4667 | Accidents | Forme pour les accidents (`coqueAccident`), poids (`masse`), départ (`commencerAccident`), coups (`vitesseEn`, `souple`, `pousser`, `toucher`, `heurter`, `souffler`), chaque image (`majAccident` : sol, murs, autres voitures, piétons), retour sur les roues (`finirAccident`) ; le feu (`allumer`, `eteindre`) |
| 4668–4774 | Sons | Moteurs (crépitement, changements de vitesse, claquements : `claquer`), roulement, sirène, sonnerie d'alarme, bruits et bips synthétisés, cri de la danse (`criMJ`) |
| 4775–5197 | Joueur, personnages, objets | Tenues, chapeau de la danse, aura de Goku, cape de Superman (`capeBJ`, `majCape`) ; la ligne d'`ENNEMIS` de chacun (`fiche`), vigiles, policiers d'élite (`creerElite`), gangs (`creerGang`), chiens (`creerChien`, `animerChien`) ; objets (dont les objets à voler et les bonus : `formeTresor`, `majCachettes`), explosions (la voiture blindée encaisse, le conducteur est tué, les personnages sont soufflés), roquettes, étincelles, éclats de verre ; prix des stands dans la langue choisie (`etiqueter`) ; impacts de balles sur les murs (`impactMur`, `impactVers`) et trous dans la tôle des voitures (`impactVoiture`, `collerImpact`, `recalerImpacts`) |
| 5198–5498 | Braquages | Masque à gaz, sac du butin, butin (`creerButin`), pièces qui bougent (`construireBraquage`), alarme (`declencherAlarme`), vol (`voler`), perceuse, explosif, fumée, lasers, mitrailleuses, coffre-fort (`majBraquages`) |
| 5499–5747 | Heavy robot | Le robot (`creerRobot`), une voiture écrasée (`aplatir`), sa marche (`bougerRobot` : il bute contre les murs et les autres robots, écrase les gens et les voitures), son chemin par les rues (`cheminRobot`), ses tirs, sa vitre et son pilote (`toucherRobot`), monter, descendre, piloter (`piloterRobot`), apparition |
| 5748–6289 | État, clavier, actions | État du jeu, skis, snowboards et luges des gares (`garnir`), clavier et souris, suite de touches de la danse, triches (`validerTriche`, `rhabillerBJ`, `parTriche`, `pouvoir`), danse (`danser`, `pasDeDanse`), Superman qui décolle (`decoller`) et accélère à chaque Maj, ascenseur, remontées (`telesiegeProche`, `horaire`, `siegeEn`, `siegeLibre`, `placerHumain`, `porter`, `monterTelesiege`, les sièges : `majTelesieges`, sauter du siège), chronomètre du boardercross (`majBoardercross`), garagiste (`payerBlindage`), achat, monter et descendre (`entrerVoiture`, `sortirVoiture`, en roulade si on roule), tir (`positionTir`, `tirer`, aussi depuis le robot ; les rayons des yeux laser : `majLaser`), blessures (`alerter`, `blesser`, et celles du conducteur d'une voiture : `blesserConducteur`), mort |
| 6290–6876 | Mise à jour du joueur | Marche (et vitesse des codes de triche), chutes (`retomber`) et chute qui écrase (`ecraser`, `dallesSous`, `trouer`, `fissurer`), roulade (`commencerRoulade`, `rouler`), vol de Superman (`superman`, qui tire aussi), échelles (`echelleProche`, `grimper`), nage, moonwalk, passants bousculés, conduite (plus lourde en voiture blindée, qui tire avec un pneu crevé), glisse (`glisser`, `poseGlisse`, `neigeSous` ; skis collés à la neige, kickers, réceptions et chutes dans `poserVoiture` et `atterrir`), chocs (contre le robot aussi, et ceux qui font partir en accident), lampadaires, bornes, dos d'âne, pentes, sauts et atterrissages des voitures ; la DeLorean à 88 miles à l'heure ; voitures qui coulent, bateaux, loopings (`entrerRail`, `roulerRail`) |
| 6877–6968 | Avions et hélicoptères | `piloterAeronef`, `pilotageAvion` (rouler, décoller, voler, se poser ou s'écraser), `pilotageHelico` (rotor, monter, avancer, se poser) |
| 6969–7439 | Intelligence | Piétons, nazis, vigiles et gangs, chiens (`majChien`), personnages projetés (`projeter`, `majVol`) qui se relèvent (`relever`), la moto qui penche, circulation sur le réseau des routes (qui ralentit aux dos d'âne, évite les rues bouchées et se laisse passer dans les carrefours : `choisirSuivant`, `devantDe`), voitures qui fument et brûlent, avions sans pilote, pales qui tournent, les autres skieurs (`creerSkieur`, `majSkieur`), pilote placé sur son véhicule une fois celui-ci posé, penché borné et mains hors de la neige à ski (`majVoiture`), chemin de la police, apparitions (`peupler`, autant que la foule choisie, et les gangs qui reviennent), police à 4 et 5 étoiles (fourgons blindés, heavy robot), chacun son tour (`aSonTour`) |
| 7440–7550 | Missions, caméra | Enchaînement des étapes, saut de mission (`sauterMission`), caméra qui s'arrête avant les murs (`placerCamera`), vues (dont le robot, en avion la souris qui vise, et à ski la caméra qui plonge avec la pente), tremblement des pas du robot (et de la chute qui écrase), zoom de la lunette |
| 7551–7750 | Écran | Repères, image du terrain, plan (avec le quartier des gangs, les pistes de ski et les remontées), mini-carte, grande carte et sa légende (`legendeCarte`), infos (vitesse et hauteur en vol, vitesse de Superman, chronomètre du boardercross), aides et voile de fumée |
| 7751–7903 | Boucle principale | Mise à jour et affichage de chaque image, objets à voler qui apparaissent près de B.J. (`majCachettes`), lampadaires qui tombent et se relèvent, garage qui répare, sonnerie d'alarme, aura qui tremble, cape qui flotte, rayons des yeux laser |

### À chaque image

1. Déplacer le joueur, à pied, sur une échelle, à la nage, en volant comme Superman, en voiture, en bateau, en avion, en hélicoptère, à ski, en snowboard, en luge, sur une remontée ou dans le heavy robot, et tirer si le bouton est enfoncé.
2. Faire réfléchir et bouger chaque personnage, puis chaque voiture (en accident, elle vole et tourne toute seule ; un avion ou un hélicoptère sans pilote tombe), et la poser sur le sol (ou sur l'eau), puis chaque heavy robot. Faire vivre les braquages : alarme, fumée, lasers, mitrailleuses, perceuse et explosif. Faire avancer les sièges et les cabines des remontées (et les autres skieurs avec eux), et tenir le chronomètre du boardercross.
3. Ramasser les objets touchés par le joueur.
4. Gérer la police, repeupler autour du joueur, vérifier la mission.
5. Placer la caméra, mettre à jour l'écran, poser les rayons des yeux laser sur les yeux de B.J., choisir les morceaux du pays à dessiner, dessiner la scène.

Le pas de temps est limité à 50 ms, pour qu'un ralentissement ne fasse pas traverser les murs.

Quand la grande carte est ouverte, ces étapes sont sautées : seule la carte est dessinée.

### Choix techniques

- **Rendu** : ciel physique avec nuages, tone mapping ACES (exposition 0,5), ombres douces, reflets du ciel sur les vitres et la carrosserie, brouillard. Le soleil suit le joueur pour garder des ombres nettes autour de lui. Les éclairs de tir, les traits des balles, les flammes et les boules de feu sont dessinés à pleine lumière, sans passer par l'exposition (`toneMapped: false`).
- **Textures** : chaque texture est dessinée deux fois plus fin qu'avant, sur 512 points de côté pour la plupart. Le même dessin sert de relief : le clair ressort, le foncé se creuse. Chaque façade a un second dessin, invisible, qui dit où ça brille : les murs sont mats, les vitres sont des miroirs.
- **Poses** : `animerHumain` refait toute la pose à chaque image à partir de ce qu'on lui dit (`saut`, `atterri`, `genou`, `roulade`, `bascule`, `plie`, `ecarte`, `agite`, `touche`, en plus de la marche, de la nage et de la danse) : rien ne reste collé. La pose en l'air se mélange à celle du sol selon `h.air`, qui va de 0 à 1 en un dixième de seconde. Pour basculer ou rouler, le corps entier tourne autour d'un point choisi (`poserCorps`) : les pieds pour tomber mort ou se relever, le bassin pour voler, le milieu de la boule pour une roulade. `poseMort` donne la pose d'un mort à chaque instant (les genoux, puis la bascule, qui accélère comme une chute). Couché, le corps est remonté de l'épaisseur du torse (`hauteurCouche`). Ensuite, `membresMous` peut donner du poids aux membres (voir « Membres mous »).
- **Personnages projetés** : `projeter` donne une vitesse et une rotation à un personnage (`p.vol`) ; `majVol` le fait voler : gravité, murs (`resoudre`), sol, rebond et frottement. Il tourne aussi un peu de côté (`r`, `wr`) ; tourné de plus d'un quart de tour sur le côté, on dit la même position autrement (retourné, et tourné en arrière dans l'autre sens), pour que `r` reste petit et qu'il se couche toujours à plat. Son bassin reste au-dessus du sol d'autant plus qu'il est debout (15 cm couché, 95 cm debout ou sur la tête), ce qui le fait culbuter en glissant. Arrêté, il pivote jusqu'à être à plat, puis on repart de ses pieds : `mort` (couché) ou `releve` (`relever`). B.J. qui roule (`J.roule`, `rouler`) est plus simple : une boule qui glisse et tourne, sans rebond ; à la fin, il se déplie (`r.fin` va de 0 à 1 en 0,25 s : la pose passe de la boule à l'accroupi, et le point autour duquel il tourne descend jusqu'à ses pieds).
- **Membres mous** : `membresMous` s'appelle après `animerHumain`, une fois le corps placé. Chaque morceau de `MOUS` (le buste, la tête, les deux morceaux de chaque bras et de chaque jambe) a un bout : un point dans le monde, avec sa vitesse. À chaque image, la vitesse du bout est freinée par rapport à celle de la pose (les muscles et les articulations freinent), un ressort le tire vers la pose (sa force est `raideur`², et le bout et la pose sont pris au même instant : sinon un corps rapide traîne ses membres d'une image de retard, 56 cm à 17 m/s), et il tombe. Puis il reste au bout de son morceau et au-dessus du sol (de son épaisseur), le morceau tourne vers lui sans dépasser les limites de l'articulation (`x`, `z`), et le bout est remis là où l'articulation l'arrête. Une main ou un pied qui reste sous le sol fait monter le coude ou le genou. Les bras qui tiennent une arme ou frappent (`h.brasPris`), et les jambes quand les pieds sont posés (`jambes: false`), suivent la pose. Sans `raideur`, le mou s'efface en 0,2 s ; un personnage qui n'a pas été mou à l'image d'avant repart de sa pose. Coût mesuré : 0,07 ms par personnage et par image ; 20 soldats soufflés d'un coup font passer une image de 8,5 à 12 ms.
- **Personnages** : le torse, les bras et les jambes sont des formes faites « au tour », comme des vases. Chaque morceau de bras ou de jambe finit par une boule de la taille de la boule du morceau suivant : le coude et le genou ne se voient pas. Le visage est une image dessinée sur la tête, une par couleur de peau. Un personnage compte une vingtaine de pièces.
- **Danse** : le jeu retient le nom des dernières touches enfoncées, bout à bout. Quand la fin de cette liste est trois fois `touchesDanse`, la danse commence, et les touches encore enfoncées sont oubliées. `J.danse` compte les secondes depuis le début de la danse (0 = il ne danse pas). À chaque image, `pasDeDanse` dit quel pas est en cours et tourne le corps ; `animerHumain` place les bras, les jambes, les pieds et la tête. Le moonwalk réutilise l'animation de la marche : c'est le corps qui recule. `animerHumain` remet les pieds, la tête, l'épaule droite et l'écart des jambes à zéro à chaque image, pour tous les personnages : la pose ne reste jamais collée. Les angles du bras droit ont été calculés pour que la main tombe juste sur le bord du chapeau, puis entre les jambes. Pour la pose, l'épaule droite descend de 10 cm : les bras du personnage sont trop courts pour ce geste. Le chapeau est accroché à la tête et tourne autour de son milieu, ce qui le rabat sur les yeux ; il est caché hors de la danse.
- **Codes de triche** : au chargement, le jeu retient la matière de chaque pièce de B.J. (`userData.habit`). `rhabillerBJ` la lui remet, rend visibles les pièces cachées, remet les tailles à 1 et enlève les pièces ajoutées par les codes (faites avec `accessoire`, reconnues à leur nom), puis applique les codes actifs. Un nouveau code n'a donc qu'à décrire son effet. Le pagne de Zeus est en trois pièces (`GEO.pagne`, `GEO.pagneCuisse`) : une jupe autour du bassin, et une autour de chaque cuisse, qui suit la jambe quand il marche ou s'assoit. Leur matière est une image de 64 brins de paille, de longueurs tirées au hasard : là où rien n'est dessiné, on voit à travers (`alphaTest`). Le V de la tige des santiags est découpé de la même façon. La bande du soutien-gorge est dessinée sur l'image du torse ; ses bretelles sont un ruban en relief qui suit le torse (`GEO.bretelle`), car une ligne dessinée sur l'image fait des zigzags sur les épaules, où le torse a peu de facettes. L'écusson de Superman n'est pas dessiné sur l'image du torse, qui l'étirerait (elle est plus serrée en haut de la poitrine qu'en bas) : c'est une pièce à part (`GEO.blason`), un morceau du devant du torse à peine plus gros que lui (4 mm), sur lequel l'image du « S » est posée à plat, vue de face ; autour de l'écusson, on voit à travers. Sa cape (`capeBJ`) est une feuille de 8 × 8 carreaux, plus large en bas, accrochée en haut du dos ; elle ne se plie pas, elle tourne autour de son bord du haut. `majCape` calcule à chaque image la vitesse du torse (sa place à cette image moins celle d'avant) : le vent est l'inverse de cette vitesse (à 10 m/s, il pousse autant que le poids de la cape, et jamais plus de 4 fois), et la cape se met dans le sens du vent et du poids, vus du torse, sans traverser le dos (de 0,08 à 2,7 radians) ; elle y va en un huitième de seconde, et bat un peu (un sinus). Mesuré : elle pend à 0,08 radian à l'arrêt, se soulève à 0,56 radian (32°) en courant, reste sur le dos en vol, et monte au-dessus de la tête pendant une chute. Les cheveux de Goku sont 13 cônes dorés posés sur la tête, penchés vers le ciel. L'aura est une forme faite au tour, de 2,5 m de haut, dont la lumière s'ajoute à l'image : son dessin, des traits clairs en bas et effacés en haut, glisse vers le haut à chaque image, et sa force tremble au hasard. Le robot arrondit l'avancée de la marche au huitième de pas, et l'angle de son corps à 0,2 radian près : c'est ce qui le fait bouger par à-coups. Dans la liste du menu, chaque code est dans une case `<th>` : `traduireMenu` ne traduit que les `<td>`, donc un code qui s'appelle comme une phrase de `TRADUCTIONS` (`POLICE`) ne change pas avec la langue.
- **Superman** : le jeu retient l'heure des 3 derniers appuis sur Maj (`tapesMaj`) ; si le premier et le dernier sont à moins de `tripleMaj` secondes, `decoller` fait décoller B.J. ou arrête le vol. `J.superman` garde sa vitesse à l'horizontale (`vx`, `vz`) ; la montée est dans `J.vy`, comme pour un saut : quand le vol s'arrête en l'air, B.J. garde sa vitesse, la gravité le reprend, et `retomber` mesure la chute. À chaque image, `superman` rapproche la vitesse de celle que demandent les touches (de 2 × dt : une demi-seconde environ), avance, pousse hors des murs (`resoudre`), puis le pose ou non sur le sol (`hauteurSol`, ou la surface de l'eau profonde). Chaque appui sur Maj en volant ajoute un cran (`J.superman.crans`), sauf celui qui complète un triple (il arrête le vol) ; la vitesse demandée est `vitesseVol + crans × vitesseVolMaj`, au plus `vitesseVolMax`, et les crans retombent à 0 quand aucune touche de déplacement n'est enfoncée. La bascule du corps est l'angle, avec la verticale, de sa vitesse vers l'avant du corps (négative s'il recule en tirant) et de sa montée, en ne comptant pas la descente (0 en montant tout droit, un quart de tour à l'horizontale), multipliée par un nombre qui va de 0 (sur place) à 1 (à 6 m/s et plus) ; `animerHumain` mélange de la même façon la pose « flotte » et la pose « lancé » (`superman`). Pour tirer, `superman` tourne le corps vers le viseur et passe `arme` et `leve` à `animerHumain` : la pose de l'arme à pied, les bras levés en plus de la bascule et du tangage de la caméra, pour qu'ils visent là où l'on regarde. Le roulis (`J.superman.roulis`) suit la vitesse à laquelle le corps tourne (`roulisVirage`), multipliée par le même nombre de 0 à 1, et vaut 0 quand il tire ; le corps est tourné dans l'ordre lacet, roulis, bascule (`YZX`), pour qu'il roule autour de sa route même couché, et non autour de son ventre.
- **Cri de la danse** : il est fabriqué par le programme, comme tous les sons, et non pris sur un disque : la voix de Michael Jackson appartient à ses ayants droit, et le jeu est publié sur Internet. La voix est une note avec ses harmoniques (la 3e, vers 3 000 Hz, donne le son « i »), et le souffle est un bruit filtré autour de 3 000 Hz.
- **Voitures** : la carrosserie est un profil vu de côté, avec un creux rond au-dessus de chaque roue, étiré sur toute la largeur. Tous ses bords sont arrondis. La cabine est une boîte arrondie, plus étroite et plus courte en haut ; les vitres sont des plaques posées dessus, visibles seulement de dehors, pour qu'on voie à travers en vue intérieure. Les pièces d'un modèle sont fabriquées une seule fois, puis fusionnées par matière : une voiture neuve compte 8 objets pour le corps et 2 par roue. Le tricycle est fait de pièces simples, sans profil ni cabine.
- **Dégâts** : au premier choc, la voiture reçoit sa propre copie des formes (sans les pièces qui peuvent partir), ses vitres une par une et ses pièces à part : elle passe à une vingtaine d'objets. Ces copies sont découpées en triangles de 25 cm au plus (`TessellateModifier` de Three.js) : une portière ou un capot, qui n'avaient des points qu'à leurs bords, peuvent alors se creuser au milieu. Une bosse (`bosseler`) est un bélier arrondi : on cherche d'abord le point de la tôle le plus avancé face au choc, puis chaque point qui dépasse du bout du bélier y est ramené, gondolé et plié (`pli` : des vagues régulières d'environ 70 cm, pas du bruit au hasard, qui donnait l'air de verre brisé). Les plis dépendent de la place de départ du point, donc deux points collés bougent pareil et la tôle ne se déchire pas. Une vitre brisée garde sa place, avec une image du trou sombre et des éclats restés dans le cadre (`TEX.brisee`). Les triangles qui ont bougé renvoient la lumière chacun à sa façon : c'est ce qui donne l'air froissé. Une pièce qui part est accrochée au monde, là où elle était, et tombe comme un débris. Le garage refait la voiture toute neuve (`habillerVoiture`).
- **Accidents** : `v.accident` garde le centre de gravité de la voiture (`c`), sa vitesse (`vel`) et sa rotation (`rot`, un axe dont la longueur dit combien de radians par seconde) ; `v.quat` dit comment elle est tournée. `majAccident` avance en 4 petits pas par image : la gravité, puis chaque point de `coqueAccident` (roues, coins de la caisse et du toit) qui est sous le sol reçoit une poussée vers le haut à cet endroit (`toucher`), avec rebond et frottement, calculée avec l'inertie d'une boîte de la taille de la voiture (`selonInertie`) : c'est ce qui la fait tourner. Les murs et les autres voitures sont vus du ciel, avec sa file de cercles. `heurter` donne un coup à n'importe quelle voiture et la fait partir en accident s'il dépasse 3 m/s ; `souffler`, le souffle d'une explosion. `finirAccident` la rend à la conduite normale (angle, pente et penchant tirés de `v.quat`).
- **Lampadaires et bornes** : ils sont dessinés en lots (un objet pour tous ceux d'un morceau). Un lampadaire renversé est caché dans son lot (taille 0), sa boîte de collision coupée, et une copie bascule autour de son pied. Une borne a une boîte de collision marquée `borne`, qui n'est ni un mur ni un sol : seule `bornesSous` la voit.
- **Terrain** : une grille de points tous les 9,25 m (8 par case), dont la hauteur est calculée une fois au chargement (`HT`), puis creusée sous les routes. Chaque carré est fait de deux triangles ; `hauteurTerrain` retrouve la hauteur exacte du triangle dessiné, pour que personne ne flotte ni ne s'enfonce. Les couleurs du sol sont posées sur chaque point, puis teintent un grain gris.
- **Hauteur du sol** : `hauteurSol(x, z, y)` prend la plus haute de ces surfaces : terrain, trottoir d'un pâté, rue, route ou pont de campagne. Si on lui donne la hauteur des pieds (`y`), elle compte aussi les planchers, marches, toits et meubles qui ne dépassent pas de plus de 60 cm : c'est ce qui fait marcher les escaliers. Un pont ne compte que si on est dessus, pas si on nage dessous.
- **Routes de campagne** : chaque suite de cases `=` ou `#` devient une ligne de points, arrondie trois fois (on coupe chaque coin au quart et aux trois quarts). Les routes et les rues forment un seul réseau de points reliés (`NOEUDS`) : les voitures qui roulent seules le suivent, et la police y cherche le chemin le plus court vers le joueur (algorithme de Dijkstra). Les morceaux de route sont rangés dans une grille de 25 m, pour trouver vite la route sous une voiture.
- **Circulation** : une voiture qui roule seule vise une « carotte », un point 6 m devant elle sur sa voie. Elle regarde vers cette carotte (`v.regard`), pas devant son capot : c'est là qu'elle cherche ce qui la bloque (`devantDe`). Pour un demi-tour, la route est inversée et la carotte passe sur l'autre voie, à côté de la voiture : elle regarde alors de côté, ne voit plus la voiture de devant, et peut tourner. Avant, elle regardait devant son capot : arrêtée derrière une autre, elle ne pouvait pas tourner (elle ne braque qu'en roulant), et inversait sa route toutes les 5 s sans bouger. Deux voitures qui se voient l'une l'autre se bloquaient aussi pour toujours dans les carrefours : maintenant, celle qui a la plus grande `v.priorite` (un nombre tiré au sort) ne tient pas compte de l'autre, sauf quand elles sont face à face (sinon elles se traverseraient). Au bout d'une rue, `choisirSuivant` écarte les rues où une voiture pilotée roule à moins de 1 m/s.
- **Bâtiments visitables** : une seule fonction, `batiment`, fabrique les murs, la porte, les planchers, l'escalier, le toit et les lampes. Les meubles se placent comme si la porte était au sud ; la fonction tourne le tout selon le côté de la porte. Tout est fait de boîtes, rangées avec les autres. Le mur de la porte est fait de 3 morceaux (à gauche, à droite et au-dessus de la porte) : le dessin de chacun reprend là où s'arrêtent celui de gauche et celui d'en dessous (`facade`), sinon les étages et les fenêtres sont décalés au-dessus de la porte. `bas` pose un bâtiment sur un autre (le haut d'une terrasse) ; `toit: 'dehors'` donne un toit avec garde-fou mais sans trou d'escalier. Ce qui est dedans (murs intérieurs, planchers, escalier, meubles, lampes : `dedans`, et `meuble`) est rangé à part, un groupe par bâtiment (`interieurs`), dessiné seulement à moins de 100 m de la caméra (`majMorceaux`) ; les murs, la dalle du toit et le toit restent dans les morceaux du pays. Rien de ce qui est dedans ne fait d'ombre (`fusionner(..., false)`) : le soleil n'y entre pas ; la dalle du toit, si (`dalle`, le même plâtre sous un autre nom). Les cloisons et les meubles hauts ne vont pas sur la mini-carte. La dalle de toit des immeubles pleins (60 cm) et celle des bâtiments sans accès au toit (40 cm), ainsi que les blocs de climatisation, ont une boîte de collision : avant, on se posait sur le haut des murs, 60 cm dans le toit dessiné (l'hélicoptère et B.J. s'y enfonçaient à moitié).
- **Meubles** : `meubler` tire la sorte de chaque étage avec son propre hasard (`graine`), nourri par deux tirages du hasard du pâté, comme l'ancien `meubler` : le reste du pays ne change pas. Tout est fait de boîtes (et d'une boule pour les plantes), placées par des petites fonctions (`lit`, `canape`, `tele`, `cuisine`, `bureau`...) qui prennent le milieu du meuble et le côté vers lequel il regarde (`pose`). Chaque meuble qui peut porter un objet le note (`cache`) ; on en tire un ou deux par étage, rangés dans `cachettes`. `majCachettes` ne crée l'objet (`creerObjet`) que quand B.J. est à moins de 60 m, et l'enlève au-delà de 90 m : il n'y a jamais plus de quelques dizaines d'objets à la fois.
- **Immeubles où l'on entre** : `immeubleI` tire au hasard (le hasard du pâté) si un immeuble se visite, puis sa sorte. `meubler` meuble chaque étage (voir « Meubles »). `echelle` pose les montants et les barreaux et note l'échelle dans `echelles` (où l'on se tient, vers le mur, le bas, le haut, où l'on arrive sur le toit) ; `grimper` fait monter B.J. sans gravité tant qu'il y est. `escalierDehors` pose des volées de 12 marches fines (des boîtes de 25 cm d'épaisseur, pas des blocs pleins, pour qu'on passe dessous), en zigzag sur deux bandes, un palier à chaque étage, puis une petite volée jusqu'au garde-fou.
- **Avions et hélicoptères** : ce sont des voitures du tableau `VOITURES` avec `vole`, comme les bateaux avec `bateau` : on les vole, on les voit, on les entend et on les fait exploser de la même façon. `pasDeTole` les tient à l'écart des bosses, des accidents et des bornes. `piloterAeronef` les fait voler, avec ou sans pilote (`pilotageAvion`, `pilotageHelico`) ; au sol, l'avion roule avec `bougerVoiture`. La fonction `roulisVirage` (dans les outils) donne le roulis voulu pour une vitesse de virage (bornée à 0,7 radian par seconde, multipliée par le réglage `roulisVirage`) ; elle sert à l'avion, à l'hélicoptère et à Superman, qui s'en rapprochent en un tiers de seconde environ. En l'air, rien ne les pose sur le sol (`poserVoiture` les laisse) ; `v.enVol` dit s'ils volent. Les pales de l'hélicoptère sont des groupes à part (`rotors`), qui tournent avec `v.rotor`. L'avion vérifie 4 points (le nez, le bout des ailes, la queue) contre les bâtiments et le terrain ; l'hélicoptère est un cercle de 2 m contre les murs (`resoudre`).
- **Dos d'âne** : `dosH` et `dosV` gardent les rues qui en ont un, tirées au hasard à partir de leur place ; `dosRoute`, les mêmes morceaux du réseau des routes (la circulation y ralentit). `dosDAneEn` donne la hauteur de la bosse en un point, ajoutée par `hauteurSol`. Pour le saut, `poserVoiture` prend la pente de la bosse sous le milieu de la voiture, et garde l'élan de la montée (`v.elanDos`) pour le lui rendre au sommet, même si elle a décollé un peu avant.
- **Gangs** : ce sont des personnages comme les vigiles (`VIGILES`) : ils restent dans leur pâté et n'attaquent que si on les provoque. `alerter` rend hostile un personnage, et tout son gang avec lui. `creerGang` les place en rond ; `peupler` refait un gang loin de B.J.
- **Performance** : le pays est découpé en morceaux de 8 × 8 cases (592 m). Dans chaque morceau, les bâtiments sont fusionnés en un objet par matière (`fusionner`), et chaque sorte d'arbre et les lampadaires sont dessinés en un seul lot. Seuls les morceaux à moins de `distanceVue` (plus leur demi-diagonale) sont dessinés, et l'intérieur des bâtiments à moins de 100 m. Les arbres de la campagne ont moins de facettes que ceux de la ville. Résultat mesuré en rendu logiciel : 150 à 450 appels de dessin et 250 000 à 550 000 triangles par image, ombres comprises. Mesuré sans la foule, à 4 endroits de Los Santos, les immeubles où l'on entre ont ajouté 6 à 14 % de triangles (de 420 000–550 000 à 447 000–628 000) et 1 à 6 % d'appels de dessin. Les personnages ne sont plus dessinés au-delà de 220 m, les voitures (et les avions) au-delà de 350 m. Dans les montagnes de l'est (mesuré de même) : à la station de ski, 78 appels de dessin et 166 000 triangles ; au milieu des pistes, en regardant la vallée, 554 appels et 232 000 triangles, car d'en haut on voit beaucoup de morceaux du pays, avec leurs arbres et leurs ombres. La carte est 50 % plus large, mais la construction du pays ne prend pas plus de temps mesurable (9 à 10 s ici, pour l'ancienne version comme pour la nouvelle, sur une machine chargée).
- **Chargement** : la construction du pays prend environ 2 s en rendu logiciel (relief 0,4 s, pâtés 0,2 s, terrain 0,9 s). Le plus long reste le dessin des textures et du ciel.
- **Collisions** : chaque mur, plancher, marche ou meuble est une boîte avec un bas et un haut, rangée dans une grille de cases de 25 m. On passe sous une boîte dont le bas est au-dessus de la tête, et on monte sur une boîte assez basse, sauf sur les murs des loopings (`mur`). Joueur et piétons sont des cercles repoussés hors des boîtes. Une voiture est une file de 2 à 4 cercles posés le long de son axe (2 pour la classique, 4 pour la limousine), un peu plus larges qu'elle. La même grille, et le terrain, servent à savoir si un ennemi voit le joueur : une colline cache aussi. `butee(a, b)` dit où le chemin tout droit de a à b bute (de 0, tout de suite, à 1, rien ne gêne) : pour chaque boîte, `traversee` calcule exactement où le chemin y entre et en sort ; pour le terrain, on regarde un point tous les 1,5 m. `voit` s'en sert d'yeux à yeux, et `balleArrive` pour chaque balle d'un ennemi, depuis le milieu du tireur (collé à un mur fin, le bout de son canon est déjà de l'autre côté). Avant, `voit` ne regardait qu'un point tous les 1,5 m, pour les boîtes aussi : il sautait par-dessus les murs de 30 cm des bâtiments où l'on entre (6 fois sur 10, mesuré sur les 104 immeubles), et une fois sur 3 par-dessus le mur du fort (1 m). La caméra en 3e personne cherche de la même façon (`traversee`) où le chemin de la tête de B.J. vers sa place voulue entre dans une de ces boîtes, grossie de 25 cm (`placerCamera`) ; avant, elle ne regardait que 20 points de ce chemin : elle pouvait sauter une cloison de 12 cm, ou s'arrêter à 11 cm d'un mur, et le bord de l'image passait à travers.
- **Impacts de balles** : une petite image carrée (`TEX.impact`, `TEX.trou` : des taches aux bords déchiquetés, dessinées par `tache`) posée à plat sur ce qui est touché, 1 cm devant, sans écrire dans la profondeur. Sur les murs, un seul objet dessine tous les impacts (`impactsMurs`, un `InstancedMesh` de `impactsMurs` places) : le suivant prend la place du plus vieux, et le tout coûte un appel de dessin. Les formes des bâtiments portent `userData.mur` (`fusionner`) : c'est là que `tirer` pose un impact, avec la direction de la face touchée. Chaque impact a sa couleur (`setColorAt`) : blanc, l'image telle quelle, ou presque noir pour la brûlure des yeux laser. Sur une voiture, chaque trou est un petit objet accroché à la pièce de tôle touchée (`collerImpact`), que les rayons ne voient pas ; `v.impacts` garde les trous de la voiture. Quand la tôle bouge (`bosseler`) ou que la voiture reçoit ses propres formes (`preparerDegats`), `recalerImpacts` relance pour chaque trou un rayon le long de sa direction et le recolle sur la tôle la plus proche de son ancienne place (pas sur le rétroviseur qui serait devant) : sans ça, après quelques balles au même endroit, les premiers trous flotteraient devant le creux. Un trou parti avec une pièce détachée est oublié. Pour les balles des ennemis, `balleArrive` connaît le point où la balle finit (les boîtes de collision), mais pas ce qui est dessiné là : un mur a une peau de 2 cm à l'intérieur, un panneau peint ou une télé devant lui. `impactVers` lance donc un vrai rayon de 1,2 m contre les formes des bâtiments proches seulement (environ 1,5 ms), et seulement à moins de 80 m de la caméra. Mesuré à 5 étoiles, 60 s : jusqu'à 300 impacts posés, sans différence de temps par image (2,9 à 4,4 ms, comme avant : 2,4 à 3,7 ms, selon le nombre de policiers).
- **Tir** : un rayon part de la caméra à travers le viseur et s'arrête sur le premier bâtiment, personnage ou voiture, ou sur le terrain (on avance le long du rayon mètre par mètre, sans regarder les triangles). Les balles des ennemis ne sont pas des rayons contre les formes dessinées : un tirage au sort dit si elles touchent, puis `balleArrive` les arrête sur la première boîte de collision ou sur le terrain (voir « Collisions ») ; une balle ratée continue 60 m au plus après le point visé, et s'arrête dans la voiture de B.J. s'il est dedans. La roquette du bazooka, elle, est un vrai objet qui vole (`lancerRoquette`, `majRoquettes`) : à chaque image, elle avance, laisse une bouffée de fumée qui grossit et s'efface en 1,2 s, et un petit rayon de la longueur de son pas cherche un mur ou une voiture devant elle. Les personnages sont faits de pièces fines : pour eux, on regarde plutôt si la roquette passe à moins de 1 m du milieu de leur corps. Une explosion est une boule de feu qui grossit et s'efface en 0,6 s, avec une lumière orange.
- **Yeux laser** : c'est une ligne du tableau `ARMES` comme les autres, avec `laser: true` : `tirer` lance le même rayon depuis la caméra et fait les mêmes dégâts. Seuls changent le son, l'absence d'éclair et de recul, et le dessin : au lieu d'un trait qui s'efface, deux rayons qui restent (`rayonsLaser`, un cylindre rouge dans un halo, la matière des lasers de la banque). Chaque tir note le point touché (`cibleLaser`) et rallume les rayons pour 0,1 s (`J.laser`), plus que le temps entre deux tirs (0,066 s) : ils ne clignotent pas. `majLaser`, appelée après la caméra, les repose à chaque image entre les yeux de B.J. (ou le bas de l'image en 1re personne, où ils sont 3 fois plus fins) et ce point : ils suivent B.J. même à 100 m/s. Les munitions sont `Infinity` : le compteur ne baisse jamais. `validerTriche` donne ou reprend les armes `laser` selon les codes allumés (`pouvoir('laser')`). Ailleurs, « une arme à feu à la main » (`armeEnMain`) exclut les yeux laser : pour la pose des bras, et pour ce que voient les vigiles et les gangs.
- **Chute qui écrase** : `retomber` rend `true` quand B.J. passe à travers une dalle, pour que la marche, la roulade ou le vol ne le posent pas dessus. `ecraser` blesse et projette les personnages, aplatit les voitures proches (`aplatir`, la fonction du heavy robot) et soulève les autres (`souffler`), puis cherche les dalles (`dallesSous`) : la boîte de collision dont le haut est sous ses pieds, mince et large, et celle qui est juste dessous si elle l'est aussi (le toit d'un magasin, sur son plafond), sans rien de plein dessous à trois hauteurs et en cinq points (sous lui et à 30 cm autour), avec un sol au moins 1,80 m plus bas. `trouer` remplace chacune de ces boîtes par quatre boîtes autour d'un trou carré (la boîte elle-même est raccourcie, ou coupée si le trou touche son bord) : le trou est donc vrai pour tout le monde, et pour de bon. Les pieds de B.J. sont alors mis 65 cm sous le haut de la dalle, sous ce que `hauteurSol` prend pour une marche, et il garde la moitié de sa vitesse. Le toit dessiné, lui, est fusionné avec tout son morceau du pays : on ne le perce pas. On pose dessus une forme noire aux bords déchiquetés, et la même sous le plafond, claire et jamais assombrie par le brouillard. `fissurer` fabrique un rond de 49 points, chacun à la hauteur du sol à cet endroit (`hauteurSol` ; au bord d'un toit, il reste à plat au lieu de plonger dans la rue), avec une image de fissures dessinée une fois pour toutes (13 traits en zigzag, reliés à leurs voisins) ; les plaques soulevées et les gravats sont la même boîte, à des tailles différentes. Le rond, les deux formes du trou et les fissures sont dessinés un peu en avant de ce qu'ils couvrent (`polygonOffset`), pour ne pas scintiller de loin. Le rond et ses plaques sont rangés dans `effets`, avec 120 s à vivre.
- **Lunette** : seul le champ de vision de la caméra change. Le rond et la croix sont un dessin posé sur l'image (`#lunette`, en CSS), sans rien de plus à calculer. La dispersion d'un tir se compte en part de l'écran : zoomer 5 fois rend donc le tir 5 fois plus précis, sans règle spéciale.
- **Cartes** : le terrain vu du ciel est une petite image, un point par point de la grille, colorée comme le sol et éclairée selon la pente. Une fonction dessine par-dessus les routes, les rues, les pistes et les bâtiments. La mini-carte garde une image toute faite du tout, à un point pour 2 m ; la grande carte redessine les routes et les bâtiments à chaque image, pour rester nette quel que soit le zoom.
- **Pays reproductible** : chaque pâté et chaque case de campagne tirent leurs nombres au hasard à partir de leur position, et les bosses du terrain viennent d'un bruit calculé. Le pays est donc le même à chaque partie.
- **Sons de moteur** : un moteur, c'est deux notes (celle du moteur et la même une octave plus bas) qui passent dans un filtre. Le filtre laisse passer plus d'aigus quand le moteur est rauque, tourne vite ou accélère. Il y a deux moteurs : celui du joueur et celui de la voiture la plus proche. Les premiers rapports sont plus courts que les derniers.
- **Pistes de cascades** : chaque morceau de `CASCADES` devient une ligne de points, tous les 1 à 2 m, avec pour chacun trois directions : devant, le haut de la piste, la gauche. Le dessus est un ruban de goudron, les côtés et le dessous des bandes de béton. Là où la piste n'est pas trop penchée (moins de 18°), elle compte comme un sol : `pisteSous` trouve le morceau sous la voiture, sa hauteur et sa pente, même relevée sur le côté. Les côtés des rampes sont des boîtes de collision, en 3 bandes sur la largeur, dont le haut est le bas de la piste à cet endroit : on roule dessus, mais on bute contre. Dans un looping ou un tire-bouchon, la voiture roule « sur des rails » : sa place, son haut et son devant viennent de la ligne de points, et la courbure calculée à chaque point dit si elle reste plaquée.
- **Sauts** : la voiture tombe toujours ; elle est « au sol » quand elle arrive plus bas que le sol, et prend alors la vitesse de montée du sol. Cette vitesse vient de la pente sous ses roues, ou de la pente de la piste de cascades sous son milieu : un trottoir ne la fait presque pas sauter, le bout d'un tremplin, si.
- **Braquages** : `genererBloc` construit les parties fixes d'un pâté à braquer (murs, vitrines, socles, couloir, mur du coffre, fusionnées avec le reste du morceau) et note le reste dans un objet « braquage » : gyrophares, zone de fumée, lasers, mitrailleuses, porte et grille, butin, vigiles et chiens. Ce qui bouge ou disparaît est construit plus tard (`construireBraquage`, `creerButin`), dans un groupe par bâtiment, caché au-delà de 300 m. Le lieu d'un pâté à braquer, pour les missions, est déplacé sur la place devant l'entrée. La porte du coffre et la grille sont des boîtes de collision qu'on coupe en mettant leur haut à `-Infinity` (`ajouterCollision` rend la boîte) ; la porte ouverte en a une autre, coupée au départ. Chaque image, `majBraquages` fait clignoter l'alarme, monter la fumée, bouger les lasers (et regarde s'ils passent à moins de 25 cm de B.J., 28 cm pour un laser debout, entre ses pieds et 1,75 m, ou 1,15 m accroupi), tirer les mitrailleuses et avancer la perceuse et l'explosif.
- **Vigiles et chiens** : ce sont des personnages comme les autres (`personnes`), avec un `braquage` et une zone. Un vigile a son arme à lui (`armeIdx`) et peut tirer en rafales (`rafale`). Le chien a son propre corps (`creerChien` : un corps en gélule, 4 pattes qui avancent en diagonale, une queue qui remue) et son propre comportement (`majChien`).
- **Voiture blindée** : `v.blindee` ajoute deux pièces au modèle, la tôle rouillée et l'acier (`formesBlindage`, calculées une fois par modèle à partir de sa forme : profil, cabine, longueur). Elles se cabossent comme le reste. `estBlindee` dit si une voiture est blindée, par le garagiste ou parce que c'est un fourgon de police.
- **Heavy robot** : un modèle articulé (bassin, torse, bras, hanches, genoux, pieds), comme les personnages, avec un policier assis dedans. Il est rangé à part (`robots`), avec sa propre marche, ses tirs et ses dégâts. Pour tirer depuis le robot, `tirer` reçoit l'arme du robot (`ARMES_ROBOT`) au lieu de celle de B.J. ; les balles partent de ses canons, et le rayon ignore le robot lui-même. Une roquette ignore le robot qui l'a tirée.
- **Langues** : le code du jeu est écrit en français, et la phrase française sert de clé : `tr('Il te faut {prix} $', { prix })` cherche la phrase dans `TRADUCTIONS`, prend la traduction dans la langue choisie (sinon le français), puis met les valeurs à la place des `{...}`. Les tableaux (`ARMES`, `VOITURES`, `MISSIONS`, `TRICHES`, `NOMS_LIEUX`...) gardent leurs noms français, qui servent aussi à les retrouver (`indexArme`, `typeNomme`) ; on ne les traduit qu'au moment de les afficher. Le menu est du HTML : chaque texte garde sa version française dans `data-fr` (`traduireMenu`). `LANGUES`, `TRADUCTIONS`, `tr` et les boutons sont dans un petit script à part, avant le module du jeu : il tourne tout de suite, sans attendre Three.js, et le module s'en sert. Les boutons de la foule y sont aussi, avec `FOULES` et le choix `foule`, que `peupler` relit toutes les demi-secondes ; le choix est gardé dans le `localStorage` (`foule-pietons`, `foule-voitures`). Un choix du premier lancement renommé ou enlevé de `FOULES` est remplacé par le premier du tableau. L'écran est réécrit à chaque image, donc il suit la langue tout seul ; les prix des stands et les enseignes sont dessinés dans des images, redessinées dans la nouvelle langue quand on quitte le menu (`etiqueter`, et `majEnseignes` : chaque enseigne est redessinée sur sa propre image, qui garde sa place dans les bâtiments fusionnés). La langue est gardée dans le `localStorage` du navigateur.
- **Écran des réglages** : juste après les tableaux, `TABLEAUX` les regroupe et `DU_CODE` en garde une copie (`structuredClone`) avant d'y remettre les nombres retenus par le navigateur, une clé par case (`"ARMES.3.degats": [22, 40]`, le nombre du code puis celui du menu). Les cases changent directement les objets du jeu : le code qui relit `R_.vitesseMarche`, `ARMES[i].degats`, `v.type.vitesse` ou `fiche(p).degats` à chaque fois voit le nouveau nombre tout de suite. L'écran est fabriqué à partir des tableaux eux-mêmes (`groupeReglages`, `champReglage`) : une valeur ajoutée dans le code y apparaît toute seule.
- **Garde-fous pour le bidouilleur** : une alerte s'affiche si une ligne de `CARTE` n'a pas la bonne longueur, si une mission vise un lieu absent de la carte, si une voiture demande un modèle qui n'existe pas, si une piste de cascades a un morceau inconnu, si un gang est posé ailleurs que sur un pâté, ou avec une arme qui n'existe pas, si un sommet est posé dans l'eau, s'il y a une station de ski (`Y`) sans aucun sommet, ou si une piste de ski a moins de 2 points (elle est alors ignorée). Une erreur pendant une image arrête la boucle du jeu : l'image se fige, et la console du navigateur (F12, onglet Console, sans recharger la page) la montre en rouge, avec la ligne fautive. Deux erreurs sont évitées d'avance : `bruit` et `bip` ignorent un volume impossible (`NaN`, quand une position est mal calculée), que le son du navigateur refuse en levant une erreur ; `lancerRoquette` ne tire pas une roquette qui part d'un point impossible, ou qui y va, et l'écrit en rouge dans la console, avec la liste des fonctions appelées, pour retrouver qui a tiré.
- **Deux-roues** : la moto et le Segway sont faits comme le tricycle (pas de carrosserie, tout dans `plus`, des `roues` données une à une). `deuxRoues` fait pencher la moto (`v.penche`, ajouté au roulis de la voiture entière) ; `debout` met le pilote debout, les mains au guidon (`tenir`). `deco` donne une couleur de plus à un modèle (les bandes rouges de la Quattro).
- **Sommets** : `sommetEn(x, z)` donne ce que les `SOMMETS` ajoutent en un point (le plus haut d'entre eux), deux fois : `lisse`, la montagne toute simple, et `h`, la même avec ses replats et ses murs (la distance au sommet est décalée d'un sinus, 5 vagues par rayon, de 35 % au plus : comme le décalage ne dépasse jamais 100 %, la pente ne remonte pas). Elle donne aussi la distance au sommet le plus proche, en part de son rayon. La hauteur de chaque case de terre (`alt`, avant les routes et les villes) prend `lisse` ; `terrainNaturel` ajoute, point par point, la différence entre `h` et `lisse`, les grandes arêtes (un `bruitDoux` de 260 m) et les petites bosses calculées sans les sommets : des vagues de 160 à 250 m ne survivraient pas au lissage des cases de 74 m. La neige (`neigeEn`) compare `h` à `neigeBas` et `neigeHaut`, avec un seuil qui change d'un endroit à l'autre (le bruit des bosses, trois fois plus serré) : ce sont les plaques. Elle colore le terrain et dit combien on glisse (`neigeSous`, de 0 à 1, qui écarte les routes et les villes, sauf la place de la station). Les bosses sont plafonnées à celles d'un terrain de 270 m : le reste du pays ne change pas.
- **Remontées** : leur tracé (`TELESIEGES`, fait par `remontee` pour chaque `Y` puis pour chaque ligne de `REMONTEES`) est calculé avec la géographie, juste après les pistes de cascades, parce qu'il met le terrain à plat autour des gares (dans `HT`, avant que le terrain soit dessiné). Les pylônes sont ajoutés un par un, là où le câble frôle le plus le terrain, jusqu'à ce qu'il passe partout (40 fois au plus). `pointCable` donne un point du câble montant ou descendant, à s mètres de la gare du bas. Les gares, les pylônes, les poulies et le câble sont des formes fusionnées avec leur morceau du pays ; les sièges d'une remontée (ou ses cabines, chacune de sa couleur), et leurs garde-corps, sont deux objets (`InstancedMesh`, jamais écartés par la caméra), replacés à chaque image par `majTelesieges` quand on est assez près. `horaire` calcule une fois, pas à pas, où en est un siège le long de sa boucle (la montée, le tour de la roue du haut, la descente, le tour de la roue du bas) toutes les 0,2 s, en ralentissant près des gares ; `siegeEn` y lit la place du siège numéro k à l'instant présent (chaque siège a le même horaire, décalé). Si on change `vitesseTelesiege` ou `vitesseGare` dans le menu, l'horaire est refait. B.J. s'assoit sur un de ces sièges : `J.telesiege` garde la remontée, le numéro du siège et la place (gauche ou droite), `siegeLibre` cherche le siège libre le plus proche du départ, et `porter` place chaque image celui qui est assis et son matériel (`placerHumain` pose un personnage dans le monde même s'il est accroché à ses skis) ; `monterTelesiege` remplace alors la marche ou la conduite (`majVoiture` laisse ses skis). Comme B.J. et son siège sont placés par le même calcul, aucun autre siège ne peut passer dans le sien. `garnir` remet les skis, les snowboards et les luges des gares.
- **Pistes de ski** : chaque ligne de `PISTES_SKI` devient une courbe (un point tous les 6 m, avec sa direction et son virage), rangée dans une grille de cases de 40 m (`grilleSki`). `pisteSkiEn` donne la piste la plus proche d'un point, à combien de mètres du départ et à combien du milieu : elle sert à la neige des pistes, aux arbres, au chronomètre et aux autres skieurs. Le relief des pistes (`reliefSki` : kickers, virages relevés, bosses et bourrelets du boardercross) est une formule, ajoutée à la hauteur du terrain dans `hauteurTerrain` (seules les cases de `grilleRelief` font le calcul) ; `bandeNeige` le dessine par-dessus le terrain, un point par mètre, toujours vers le haut (le terrain dessiné reste dessous). `majBoardercross` tient le chronomètre.
- **Autres skieurs** : ce sont des véhicules de glisse avec `conducteur: 'skieur'` et un pilote (`creerSkieur`). `majSkieur` les fait avancer sans physique de glisse : ils visent un point de leur piste 10 m devant eux, décalé en slalom, puis le départ d'une remontée, où `porter` les prend. `poserVoiture` les pose sur la neige, et un accident les éjecte comme n'importe quel pilote.
- **Glisse** : `glisser` remplace le moteur dans `conduire` (la pente, la neige, l'air, les virages, Z, S et Espace). Dans `poserVoiture`, les skis collent à la neige tant qu'elle passe à moins de 15 cm (plus 2 cm par m/s) sous leur milieu et qu'on n'a pas sauté (`v.saute`), et le sol descend sous eux de vitesse × tangente de la pente ; au bout d'un kicker, la pente est celle de l'arrière des skis, qui monte encore (l'avant est déjà dans le vide). Dans `atterrir`, on garde la vitesse de la chute le long de la pente, et on tombe si ce qui tape en travers dépasse `chuteGlisse`. `abimer` les laisse intacts, et `reglerMoteur` se tait (pas de `son` dans leur ligne de `VOITURES`). Les poses sont dans `animerHumain` (`glisse`, `pousse`, `main`), choisies par `poseGlisse` ; debout, B.J. ne suit pas la pente, seulement `v.penche` (celui de la moto, `deuxRoues`), qui fait aussi pencher les skis et que `majVoiture` borne à 0,9 radian de la pente de côté. Après l'avoir placé, `majVoiture` regarde où sont ses mains : sous la neige, le bras se relève (4 essais au plus par image). Les tenues (`TENUES_GLISSE`) sont appliquées par `rhabillerBJ`, comme les codes de triche, quand il monte ou descend.
- **Tests** : `window.jeu` donne accès à l'état du jeu. Des scripts hors dépôt pilotent Chromium sans écran pour vérifier la conduite de chaque véhicule, la circulation (en ville et à la campagne), les tirs, les explosions, la police, les triches, la mort, les escaliers, l'ascenseur, la nage, la voiture qui coule, le bateau, les pentes, le braquage, l'enchaînement des premières missions, le looping (réussi à 90 km/h, raté à 50 km/h), le tire-bouchon, le premier tremplin, un choc contre un immeuble, une balle dans le pare-brise et la réparation au garage, les accidents (choc de côté à 72 km/h contre une Porsche garée, mur à 100 km/h, explosion, pneu crevé à 90 km/h, voiture lâchée sur le toit qui brûle puis explose, lampadaire, rangée de bornes), le conducteur tué par balle (passant, policier, rien à travers un fourgon blindé, en plein accident) ou par une explosion (avec et sans étoile), la voiture trop abîmée qui brûle puis explose (vide, avec B.J. dedans, éteinte au garage) et le nombre de balles qu'il faut et des photos des dégâts, les codes `IDKFA` (et ses autres noms `ARMES`, `WAFFEN`, `WEAPONS`), `MISSION` et `RICHE`, les codes `GOKU` et `Z6PO` (vitesse du robot, balles, alias `C3PO`, annulation), le code `DIEU` et ses autres noms (une balle, une explosion et la fumée de la bijouterie sans masque, avec et sans le code), le blindage chez le garagiste (sans et avec assez d'argent), la voiture blindée sous les balles et les roquettes, les trois braquages de bout en bout (butin, alarme, vigiles et chiens, fumée avec et sans masque, lasers et mitrailleuses, perceuse, explosif, planque avec et sans police), les fourgons blindés à 4 étoiles, le heavy robot à 5 étoiles (il tire, sa vitre casse, on éjecte le pilote, on le pilote, on tire, on descend), la foule (boutons, choix gardé après un rechargement, nombre de piétons et de voitures pour chaque choix, à l'arrêt et en traversant la ville à 90 km/h), les langues (boutons pendant le chargement, menu, objectif, arme, aide devant un stand, codes de triche, garagiste, argent, prix des stands, enseignes redessinées en quittant le menu, grande carte et sa légende, langue gardée après un rechargement ; et une vérification du tableau `TRADUCTIONS` : chaque `tr(...)` a sa ligne, chaque ligne a ses trois langues), la voiture en toupie contre une voiture garée et un piéton (avant la correction, ni l'une ni l'autre ne bougeait), le choc de côté à 72 km/h tracé image par image (0,49 de dégâts de chaque côté, sans tourner pour rien), la voiture posée sur une borne qui repart et celle qui bute doucement puis recule, les dos d'âne (combien, profil, saut à 30, 60 et 100 km/h, la circulation qui ralentit), l'avion (décollage, virage, atterrissage sur la piste, descendre, crash en piqué), l'hélicoptère (rotor, montée, avancer, se poser, descendre ; lâché sans pilote), les gangs (calmes devant les poings, attaque au pistolet, butin sans étoile, calmes de loin, retour au complet), les immeubles (B.J. monte à pied, touche par touche, sur le toit ou la terrasse de chaque sorte, et redescend l'échelle), le coût du rendu avant et après, et pour prendre des vues du pays avec une caméra libre. Les sons de moteur sont fabriqués hors ligne puis mesurés (note, volume). Le 30 septembre 2026 : l'écart entre le toit dessiné et le toit où l'on se pose sur 14 immeubles pleins et tours (0,40 à 0,60 m avant, 0 après), les chutes de 3, 9 et 20 m, la chute en courant (roulade), la sortie de voiture à 36, 72 et 108 km/h, un piéton renversé à 15 et 60 km/h, un piéton tué par balle (pose à chaque instant), trois soldats soufflés par une explosion, un passant bousculé en courant, le nombre d'étages de chaque sorte et de cachettes, le vol d'un objet et chaque bonus, l'escalier de chaque sorte d'immeuble à travers les meubles, chaque nouveau véhicule (vitesse, virage, sortie en roulade), la moto qui penche, la DeLorean à 88 miles à l'heure, la moto qui éjecte B.J. dans un choc, la mort sur une moto lancée suivie du réveil à l'hôpital (sans roulade), le pilote qui penche avec la moto, une roulade qui tombe de 9 m, la vraie boucle du jeu (caméra et écran) à moto, dans un appartement et sur un Segway, et des photos des pièces, des poses et des véhicules. La caméra en 3e personne dans 4 appartements, à 2 016 places et 24 directions : avant, 2 280 fois sur 48 384 elle était derrière un mur et 13 788 fois un coin de l'image était dans un mur ou derrière ; après, jamais. Des photos, avant et après, de la façade au-dessus d'une porte, de la porte d'une salle de bain et de la caméra dans un appartement. Les sons de moteur sont fabriqués hors ligne puis mesurés (note, volume). Pour les membres mous : des photos « stroboscopiques » (plusieurs instants sur une image, dans un décor vide avec des ombres) d'un piéton renversé à 15 km/h (il se relève) et à 47 km/h, de piétons tués par balle, de soldats soufflés, de B.J. qui saute, tombe de 9 m et sort en roulade à 72 km/h ; la hauteur des mains, des pieds et de la tête d'un mort couché (avant la correction, ses pieds étaient 10 cm sous le sol) ; l'écart des bras pendant une chute (avant la correction, 0,35 au lieu de 1,1) ; un coup encaissé ; le coût du calcul ; les distances des personnages renversés et soufflés, comparées à celles de la version d'avant, dans la même rue. Pour la circulation : 3 min de jeu, foule Énorme, B.J. immobile en ville, avant et après (voitures arrêtées, plus gros bouchon, vitesse moyenne, voitures qui se chevauchent, demi-tours, et ce qui bloque chaque voiture arrêtée) ; la même chose dans une rue fermée par deux voitures garées ; la circulation à la campagne, et les voitures de police qui arrivent jusqu'à B.J. à 2 étoiles. Pour les montagnes : la hauteur du terrain et des sommets, des photos du massif de loin et de près, le tracé du télésiège (pylônes et câble au-dessus du terrain), le trajet à pied et avec les skis (95 s), le saut du siège, la descente à ski depuis la gare du haut suivie image par image (hauteur, vitesse, en l'air ou sur la neige : avant les corrections, B.J. passait plus de la moitié du temps en l'air et tombait au bout de 14 s ; après, il descend de 820 à 113 m en 40 s sans quitter la neige, sauf au rebord de la gare), le frein, un virage, le snowboard et la luge sur la même pente, un choc contre un pylône, et la vraie boucle du jeu à la station (aide, mini-carte, sièges). Pour le bouton des codes de triche : une ligne par code, les autres noms, la liste fermée au départ, le clic qui la déplie sans lancer le jeu, le titre, la phrase et les textes dans les quatre langues (les codes, eux, ne changent pas), ⚙ Réglages toujours traduit, pas de défilement de côté, Entrée qui ouvre toujours la saisie, et deux photos de la liste dépliée. Pour les murs qui arrêtent la vue et les balles des ennemis : `voit` comparé à un vrai rayon contre les murs dessinés, sur 2 496 paires (un point dans un immeuble où l'on entre, un point à moins de 40 m) : avant, 717 fois « vu » malgré un mur ; après, 2, à travers des objets de décor sans boîte de collision. B.J. au milieu d'un étage des 104 immeubles et des observateurs tout autour : plus jamais vu à travers un mur de côté ou la façade, ni depuis la rue quand il est à l'étage ; derrière la porte, il est vu par celui qui est devant (104 fois sur 104). 3 étoiles dans un immeuble, sur son toit, et le tour du fort par dehors, avec un juge qui cherche, à chaque balle reçue, un ennemi sans mur dessiné devant lui : avant, toutes les balles reçues traversaient un mur ; après, aucune. À découvert, autant de dégâts qu'avant (soldats, heavy robot seul), et jamais caché sans mur dessiné (1 769 mesures à 5 étoiles). Les mitrailleuses de la banque : celle de la salle du coffre ne tire plus dans le couloir à travers le mur du coffre. La caméra : 16 200 positions dans 15 immeubles, les mêmes avant et après. Pour `SUPERMAN`, les yeux laser et la chute qui écrase (1er octobre 2026, avec un petit programme qui pilote Chromium sans écran par son tuyau de débogage) : des photos du costume de face, de dos, de près et de profil, en courant et en vol, avec `DIEU`, `SLIP` et `Z6PO` par-dessus, et après annulation ; l'angle de la cape à l'arrêt, en courant et en vol ; l'arme n° 9 donnée par `SUPERMAN` et par `GOD`, gardée tant qu'un des deux codes reste allumé, reprise ensuite (retour aux poings), jamais donnée par `IDKFA` ni par la touche 9 sans code ; les rayons allumés pendant le tir et éteints après, en 3e et en 1re personne, et dans la vraie boucle du jeu (nom de l'arme à l'écran, pas de compteur de munitions) ; le temps pour tuer un policier, un soldat, le Kommandant et Hitler, et pour enflammer une voiture ; une chute de 25 m sur une place avec 4 piétons et 2 voitures (vie intacte, genou, étoiles, voiture aplatie qui explose, voiture soulevée, photos des fissures), de 3 m (rien), de 6 m (un petit rond) ; sur le toit d'un immeuble de 4 étages, de 8, 12, 40 et 200 m, puis à pied vers le trou ; dans un coin du toit, à 45 cm du garde-fou ; sur le toit d'une supérette, de 15 m, à 7 endroits (B.J. traverse le toit et le plafond et tombe dans le magasin, sauf au-dessus d'un rayon) ; sur le toit plein de l'hôpital, au milieu et tout au bord (il se fissure, sans casser) ; dans l'eau profonde (rien) ; à 3 m d'un heavy robot (sa vitre passe de 350 à 25) ; la cape pendant une chute (2,7 radians) ; un piqué en vol avec deux appuis sur Maj (il écrase) et une descente à la vitesse normale (il se pose) ; sans aucun code, une chute de 9 m (50 points perdus, comme avant) et un piqué en vol (rien) ; les trois nouveaux textes et leurs trois traductions, et la liste du menu en français et en allemand. Pour le numéro de version (avec une fausse réponse de GitHub) : rien à la première visite si GitHub refuse ; le numéro affiché et gardé quand il répond ; le même numéro, affiché tout de suite, quand il refuse ensuite ou que le réseau est coupé ; le numéro suivant dès qu'il le donne ; une seule demande par ouverture du jeu ; puis une vraie demande à GitHub. Pour le domaine skiable : chaque remontée (longueur, hauteurs, pylônes, câble à 3,2 m au moins du terrain et sous le toit des gares, nombre de sièges, durée du trajet), chaque piste (longueur, pente, rien qui remonte, remontée au départ et à l'arrivée), la part de neige selon la distance au sommet, B.J. suivi toutes les 3 s sur son siège (toujours à 30 cm du même siège, jamais d'autre siège à moins de 2 m), le saut à 85 km/h dans une pente de 35° et sur le plat, les kickers à 43, 54, 72 et 90 km/h, une chute de 8 m et de 25 m, un virage à fond dans une pente de 50° à ski et en snowboard (le point le plus bas du corps, image par image), les pieds et le matériel sur le siège, le pied avant et le pied arrière du snowboard quand il pousse, le boardercross descendu au chronomètre, la télécabine, 6 minutes de vie des 30 skieurs (où ils sont, aucun bloqué), le coût d'une image à la station (0,25 ms pour les skieurs, 0,5 ms pour les 308 sièges), et des photos de chaque nouveauté. Pour les impacts de balles : 12 tirs sur une façade (12 impacts, à 1 cm du mur), 16 tirs sur le flanc d'une voiture (les trous à 4 mm de la tôle, même après 6 balles au même endroit, puis après un gros choc de chaque côté ; plus aucun après l'explosion), un tir dans une vitre (pas de trou), des trous sur un pare-chocs qui tombe, les balles ratées de 6 soldats (83 impacts sur la façade derrière B.J. en 30 s ; dans le bunker, 42 impacts sur la peau du mur du fond, 3 cm devant sa boîte de collision), B.J. en voiture sous le feu (17 à 20 trous), 6 tirs des yeux laser (6 marques noires, à côté de 6 impacts clairs de pistolet), un avion et un bateau (6 trous pour 6 balles), un fourgon blindé (aucun trou), et des photos de chaque cas. Les dégâts reçus n'ont pas changé (soldats, heavy robot seul, mitrailleuses de la banque, murs qui protègent).

## Limites connues et pistes

Le jeu est complet et jouable, mais la fluidité sur une vraie carte graphique et le son n'ont pas encore été vérifiés : les tests ont tourné en rendu logiciel. Le pays, bien plus grand, fait dessiner jusqu'à deux fois plus de triangles qu'avant : si le jeu rame, baisser `distanceVue` (500) ou couper les ombres (`ombres: false`). Les bruits de moteur ont été mesurés, pas écoutés : les réglages du tableau `VOITURES` sont à ajuster à l'oreille. Le crépitement, les claquements et l'effet Doppler aussi : leur volume est le même qu'avant à fond (à 13 % près), mais leur force (2,5 et 0,6, dans `reglerMoteur` et `claquer`) n'a pas été écoutée. Le cri de la danse aussi : ses notes et sa force ont été mesurées, mais personne ne l'a encore écouté.

### Limites actuelles

- Il n'y a pas de sauvegarde : recharger la page fait tout recommencer.
- Écran des réglages : il ne montre pas les commentaires du code (une case `rauque` ou `seuilAccident` ne dit pas ce qu'elle fait), et on n'y ajoute rien (une arme, une voiture, des `couleurs` à une voiture qui n'en a pas) : ça se fait dans le code. Un nombre impossible (une arme numéro 99, une voiture à 0 rapport) peut encore faire planter le jeu ; Tout remettre répare.
- Les tours, les maisons et 4 immeubles sur 5 restent pleins. Les intérieurs sont faits de boîtes, sans fenêtres percées : la lumière vient du ciel et des lampes du plafond, qui brillent sans éclairer. Dans les immeubles, les pièces n'ont pas de portes (des passages), les meubles sont des boîtes, et on ne peut ni s'asseoir, ni allumer la télé, ni ouvrir le frigo. Il n'y a personne dans les appartements. De plus de 100 m, on ne voit plus l'intérieur des bâtiments (même par une grande porte, comme celle d'un hangar).
- Les échelles n'ont pas d'arceaux, et on ne peut pas tirer en grimpant. La police et les gangs ne savent pas suivre B.J. dans les escaliers : ils vont tout droit vers lui et butent contre les murs.
- En 3e personne, la caméra est à l'étroit dans les petites pièces (la caravane de Trevor) : la vue à la 1re personne (V) y est plus confortable.
- La route du château est raide (environ 30 %) : la carte n'a pas la place pour des lacets. Les pentes autour des villes perchées sont des falaises de roche.
- Les rambardes des ponts de campagne ne retiennent pas les voitures. B.J. ne prend rien quand sa voiture s'écrase (sauf sur une moto, un Segway ou un tricycle, qui l'éjectent). Il n'y a pas de parachute : sauter du gratte-ciel ou d'un avion tue.
- Avions et hélicoptères : seul le fuselage cogne (les ailes, la queue et les pales traversent les murs, les arbres et les gens). Les balles ne leur font rien, seules les roquettes. On ne descend qu'une fois posé : pas de parachute. L'avion ne recule pas, et peut décoller de n'importe quelle route assez longue. Personne d'autre ne vole, la police ne les poursuit pas, et un appareil détruit ne revient pas. Le bord du monde est à 300 m de la carte ; on y glisse le long d'un mur invisible.
- Gangs : ils restent en rond à leur place tant qu'on ne les provoque pas (pas de balade, pas de voitures), ne quittent jamais leur pâté et ne se battent pas entre eux. La police ne s'en mêle pas.
- Dos d'âne : seulement en ville. La police ne ralentit pas devant, et ils ne gênent ni les piétons ni le heavy robot.
- Les voitures ne dérapent pas : elles tournent aussi bien à toute vitesse. Un virage relevé penche, mais ne permet pas d'aller plus vite. Elles ne glissent de côté que pendant un accident.
- Accidents : vue du ciel, une voiture accidentée reste une file de cercles le long de son axe, même dressée sur le nez ; contre un mur, elle ne se renverse donc pas par-dessus. Elle ne voit pas les bornes, et les voitures qui roulent toutes seules ne la voient pas non plus (elles s'arrêtent derrière, puis font demi-tour). Elle pousse B.J. à pied sans le blesser, et traverse le heavy robot. Pendant l'accident, la souris ne tourne pas la caméra. Rien ne blesse B.J. dans les tonneaux : seule l'explosion d'une voiture retournée le touche.
- Les piétons et B.J. traversent les bornes en béton. Un lampadaire tombé ne gêne personne, et les voitures qui roulent toutes seules ne renversent pas les lampadaires.
- Dans un looping ou un tire-bouchon, la voiture ne peut ni accélérer ni tourner, et reste à la même place dans la largeur de la piste.
- Une piste de cascades est à une seule hauteur : sur un terrain en pente, elle creuse ou remblaie beaucoup. Rien n'empêche deux morceaux de se croiser, et une piste peut passer dans une ville ou dans l'eau.
- Les pièces tombées et les éclats de vitre traversent les voitures. Les voitures qui roulent toutes seules ne vont pas sur les pistes, et ne s'abîment que si on les tape.
- On ne nage pas dans la piscine de Michael, et on ne peut pas plonger sous l'eau.
- Pas de piétons ni de policiers à pied à la campagne : seules les voitures y circulent.
- Foule : baisser la foule pendant une pause n'enlève personne d'un coup : les piétons et les voitures en trop disparaissent en s'éloignant (200 m et 280 m). Après avoir roulé vite, un demi-tour montre une rue vide : ceux qui étaient derrière ont disparu. Avec Énorme, un vieil ordinateur peut ramer : chaque piéton est fait d'une vingtaine de pièces.
- Les bateaux ne circulent pas tout seuls, et la police ne va pas sur l'eau : en bateau, on la sème facilement.
- Le soleil est fixe : il n'y a ni nuit ni météo.
- Les balles ne détruisent une voiture qu'à force de l'abîmer du même côté (50 balles de pistolet), on ne peut pas tirer depuis une voiture ou un bateau, et la police (65 km/h) ne rattrape aucun véhicule lancé à fond, pas même le tricycle (72 km/h). Seuls les fourgons blindés (122 km/h, à partir de 4 étoiles) rattrapent les voitures lentes ; ils ne foncent pas dans la voiture de B.J. pour l'arrêter, et il n'y a pas de barrages.
- Les voitures qui roulent toutes seules ne regardent que le milieu des autres : une limousine peut couper un virage et mordre sur le trottoir.
- Circulation : il n'y a pas de feux rouges, et la priorité est tirée au sort, pas « à droite ». Trois voitures ou plus qui se bloquent en rond dans un carrefour, ou deux voitures face à face, attendent 5 s, puis l'une fait demi-tour. Une voiture ne contourne pas une voiture garée sur sa voie : elle attend 5 s derrière, puis fait demi-tour. Elle ne voit un bouchon que dans la rue juste après le carrefour ; à la campagne, où la route est coupée en petits morceaux, elle ne le voit presque jamais (de toute façon, il y a rarement un autre chemin).
- Sur un tricycle ou un bateau, B.J. garde son arme à la main.
- Codes de triche : Goku garde les yeux et les sourcils de B.J. (pas les yeux verts du Super Saiyan), et le chapeau de la danse passe à travers ses cheveux. Z6PO nage, alors que le vrai robot coulerait. Zeus garde les yeux et les sourcils foncés de B.J. ; son pagne et sa barbe sont raides (ils ne flottent pas au vent), une cuisse levée haut passe à travers la jupe du bassin, et la barbe entre dans la poitrine quand il baisse la tête. Les brins de paille sont retirés au hasard chaque fois qu'on tape un code. La liste du menu ne montre pas quels codes sont allumés, et ne décrit un code que par son annonce (« Bébé ! »).
- Le numéro de version est celui de `main` sur GitHub au moment où l'on ouvre la page, pas forcément celui du fichier chargé : juste après une mise en ligne, le navigateur peut garder l'ancien jeu une dizaine de minutes (cache de GitHub Pages) en montrant déjà le nouveau numéro. Une copie modifiée sur son ordinateur montre aussi le numéro de `main`. GitHub ne répond qu'à 60 demandes par heure et par connexion (toute la maison compte pour une seule connexion, et chaque ouverture du jeu pour une demande) : au-delà, ou hors ligne, le jeu montre le dernier numéro que ce navigateur a reçu, qui peut être en retard. La toute première fois, s'il n'en a encore jamais reçu, le numéro ne s'affiche pas.
- Code `SUPERMAN` : il garde les yeux et les sourcils de B.J. La cape est une feuille raide qui tourne autour des épaules : elle ne se plie pas, passe à travers ses jambes quand il les lève haut, à travers les sièges, les murs et le sol (accroupi, en roulade, couché). Le gilet pare-balles cache l'écusson. Superman n'est pas invincible : une voiture qu'il vient d'écraser explose 5 s plus tard, et le blesse s'il est resté à côté.
- Yeux laser : la tête de B.J. ne se tourne pas vers ce qu'il vise (les rayons partent de ses yeux, mais de travers s'il vise haut ou bas), et ses yeux ne brillent pas. Les rayons ne laissent pas de trace, ne coupent ni les lampadaires ni les arbres, et ne mettent le feu qu'aux voitures, à force de les abîmer. À 60 comme à 30 images par seconde, ils tirent 15 fois par seconde. Le texte des codes dit « touche 9 » : si on ajoute une arme après les yeux laser dans `ARMES`, ils restent la 9e, mais si on en ajoute une avant, ils passent sur une autre touche (au-delà de 9, il ne reste que la molette).
- Chute qui écrase : le sol n'est pas vraiment creusé (des fissures dessinées à plat et des plaques posées dessus), et les plaques et les gravats ne gênent ni B.J. ni les voitures. Les fissures s'effacent d'un coup au bout de 2 minutes. Un trou dans un toit reste jusqu'au rechargement de la page, mais il est dessiné, pas percé : d'en haut on ne voit pas la pièce, d'en dessous on ne voit pas le vrai ciel, et B.J. disparaît dans le noir. Les fissures autour du trou, elles, s'effacent. Le trou est carré, ses bords dessinés sont cabossés : au bord, on peut tomber un peu avant le noir, ou marcher un peu dessus. Seuls les bâtiments où l'on entre ont un toit qui casse ; les tours, les maisons et les immeubles pleins se fissurent seulement, comme les ponts et les pistes de cascades. Un toit de maison est en pente, mais B.J. se pose dedans, à plat : les fissures y sont cachées. Les lampadaires, les arbres et les bornes ne tombent pas. Le rayon et les dégâts ont été choisis sur des essais, pas en jouant : à ajuster (`rayonEcrase`, `degatsEcrase`, `hauteurCasseToit`).
- Superman : en volant, B.J. passe à travers les plafonds et les planchers, et à travers les voitures et les personnages. À grande vitesse (jusqu'à 100 m/s, plus de 3 m par image quand le jeu tourne à 30 images par seconde), il peut traverser un mur fin, ou un petit bâtiment. Comme Maj sert aussi à accélérer, taper Maj trop vite (3 fois en moins de 0,6 s) arrête le vol et le fait tomber : il faut espacer les appuis. Les poings et le couteau ne frappent pas en l'air. Avec le code `SUPERMAN` ou `DIEU`, un piqué un peu rapide vers le sol (plus de 12 m/s vers le bas) écrase tout et donne des étoiles, même quand on voulait seulement se poser.
- La danse passe en 3e personne et n'en revient pas toute seule : il faut appuyer sur V. Pendant le moonwalk, les pieds glissent un peu au lieu de rester posés, et les ennemis continuent de tirer. Comme la suite de touches n'a pas de temps limite, on peut lancer la danse sans le vouloir, en esquivant à gauche, en arrière, à droite trois fois.
- Les missions sont linéaires : une seule à la fois, dans l'ordre. Les braquages ne se font qu'après Hitler ; le code `MISSION` permet d'y sauter.
- Chaque braquage ne se fait qu'une fois : le butin volé ne revient pas, et les vigiles et les chiens tués non plus. Le butin n'a de valeur qu'avec la mission (il n'y a pas de receleur).
- Les vigiles ne font pas de rondes : ils attendent à leur place. Vigiles et chiens restent dans leur pâté : on les sème en sortant de la place. Les lasers ne voient que B.J. (pas les policiers), et le robot ne passe pas les portes : il ne peut pas entrer dans la banque.
- La fumée toxique est faite de 26 nuages plats, qui ne sortent pas de la boutique ; les vigiles et les policiers ne la craignent pas.
- Impacts de balles : rien sur le sol dehors, les arbres, les lampadaires, les personnages et le heavy robot. Les balles des ennemis ne trouent que la voiture de B.J., pas les autres voitures sur leur chemin, et n'y fêlent pas les vitres. Un trou peut se poser sur un gyrophare ou une pale d'hélicoptère. Sur une façade en verre, l'impact a quand même du plâtre autour. Les impacts des murs ne s'effacent pas avec le temps : seulement quand il y en a plus de 300. Les trous d'une pièce tombée restent sur elle, mais ne comptent plus.
- Vue et balles des ennemis : seuls les murs, les planchers, les meubles, les arbres, les lampadaires et le terrain les arrêtent ; pas les voitures ni les autres personnages. Un ennemi voit de ses yeux (1,5 m), mais vise la poitrine de B.J. (1,2 m, ou 0,8 m accroupi) : derrière un muret, il continue à tirer dans le muret. Un policier qui ne voit plus B.J. marche droit vers lui et reste contre le mur : il ne cherche pas la porte, et se cacher dans un immeuble suffit souvent à semer la police. Une explosion (roquette, voiture) blesse encore à travers un mur.
- Chacun son tour : le tour va aux policiers les plus proches, même à celui qui vient d'être projeté ou qui se relève (il le garde quelques instants sans tirer). Un policier sans tour rate toujours, même tout près.
- Le heavy robot ne peut pas être détruit : seule la vitre de sa cabine casse. Il ne monte pas les escaliers ni sur les voitures qu'il écrase (ses jambes passent à travers l'épave), et suit les rues quand il ne voit pas B.J. : il peut rester coincé derrière un pâté. Une fois pris, on ne peut pas recharger ses munitions.
- La lumière rouge de l'alarme est une vraie lumière de plus, allumée en permanence (éteinte quand il n'y a pas d'alarme) : elle coûte un peu de calcul à chaque image, partout.
- Hitler ne meurt qu'une fois : le bazooka n'a que ses 10 roquettes, et on ne peut pas en racheter.
- Les roquettes volent tout droit : elles ne suivent pas leur cible.
- Le jeu s'est figé une fois sous Firefox (29 septembre 2026) : une roquette a explosé à une position impossible (`NaN`), et son bruit a levé une erreur. La cause n'est pas trouvée : les essais dans Chromium (bazooka sur des voitures, à bout portant, vers le sol et le ciel, roquettes de Hitler sur B.J. en voiture, heavy robot) ne la reproduisent pas. Le jeu ne se fige plus ; si ça revient, la console dira qui a tiré.
- Le fusil de sniper porte à 250 m, mais les personnages ne sont plus dessinés au-delà de 220 m. Les murs du bunker et du château cachent leurs occupants : il faut viser par l'entrée.
- Langues : les traductions n'ont pas été relues par quelqu'un dont c'est la langue, surtout le züritüütsch, qui n'a pas d'orthographe officielle. Un texte ajouté dans le code sans sa ligne dans `TRADUCTIONS` reste en français dans toutes les langues. Les annonces déjà à l'écran ne changent pas de langue. Les enseignes et les prix des stands ne changent qu'en quittant le menu : derrière le menu, on voit encore l'ancienne langue.
- Personnages projetés et roulades : ce n'est pas un vrai pantin. Le corps (le bassin) suit un vol calculé à part : seuls les membres ont du poids, et ils ne le poussent pas. Les membres ne se cognent ni au corps (un bras peut passer un peu dans le torse), ni aux murs, ni aux voitures, ni aux autres personnages, et le sol qu'ils touchent est plat, à la hauteur des pieds : sur une pente ou un escalier, une main peut flotter ou s'enfoncer. Un personnage ne se couche jamais sur le côté. Le corps traverse les voitures, et peut finir couché les pieds dans un mur. B.J. qui roule traverse les voitures et les personnages ; presque arrêté, il finit son tour sur place, sans avancer. Un personnage qui retombe dans l'eau profonde coule au fond. Les `raideur` ont été choisies sur des photos, pas en jouant : à ajuster (`membresMous`, et ses appels).
- Objets des immeubles : on peut en prendre un à travers une cloison, s'il est à moins de 1,6 m. Aucun compteur n'affiche le temps qui reste à la boisson énergisante. Le butin des immeubles ne se revend pas : il rapporte tout de suite.
- Motos : elles ne font ni roue arrière ni dérapage, et tiennent debout toutes seules à l'arrêt. Le Segway ne penche pas en avant quand il accélère.
- Montagnes : le brouillard (`distanceVue`, 900 m) cache les très hautes montagnes de loin ; de Grapeseed, on ne voit du mont Gordo qu'une silhouette pâle, et on ne le découvre vraiment qu'en approchant. Les sommets sont des cônes, sans falaises ni rochers, avec des replats et des murs. Le terrain est fait de carrés de 9,25 m : les plaques de neige et le bord des pistes ont des contours en escalier.
- Glisse : comme les voitures, les skis ne dérapent jamais : ils vont là où ils pointent, même en travers d'une pente à 50°, et un virage relevé du boardercross ne fait pas tourner tout seul. Ils collent à la neige : hors des kickers et du saut (Espace), on ne décolle pas, même au sommet d'un mur. Pas de figures en l'air (B.J. garde sa pose), et on ne peut pas tirer. Les pentes sont très raides (45° de moyenne sur les pistes rouges) : les couleurs des pistes disent seulement laquelle est la plus facile. Le bout d'un kicker est dessiné en pente raide, pas à pic. La main de B.J. touche la neige, mais ses bâtons peuvent passer dessous.
- Remontées : elles ne font que monter (on redescend à ski ou à pied), et on y monte avec des skis, un snowboard ou une luge, pas avec une voiture. Dans la télécabine, on voit B.J. par les côtés ouverts : pas de vitres, pas de porte. Le siège passe à travers les poulies des pylônes. Sans `vitesseGare`, il faut parfois attendre qu'une cabine soit en gare.
- Autres skieurs : ils avancent sur des rails (une piste, puis une remontée), passent à travers les arbres, les pylônes et les uns des autres, ne tombent pas tout seuls et ne sautent pas les kickers exprès. Ils ne font pas la queue : ils attendent tous au même endroit. Un skieur tombé ne rechausse pas : il part à pied, et un autre apparaît ailleurs.
- Il faut Internet, même pour jouer depuis le fichier.
- Ctrl+W ferme l'onglet dans certains navigateurs : C est plus sûr pour s'accroupir.

### Pistes pour la suite

- Tir par la fenêtre, klaxon.
- Des impacts différents selon la matière (verre, bois, métal), sur le sol, et des vitres de voiture trouées avant de se briser.
- Des policiers qui cherchent la porte pour entrer dans l'immeuble où B.J. se cache, et des murs qui protègent des explosions.
- Chrono et records sur les pistes de cascades, une mission de cascades.
- Des blessures pour B.J. dans les gros accidents, un pare-brise qu'on traverse.
- Des dérapages dans les virages pris trop vite : les virages relevés serviraient alors vraiment.
- Roquettes à acheter à l'armurerie.
- Sauvegarde de l'argent, des armes et des missions dans le navigateur.
- Une bulle d'aide sur chaque case de l'écran des réglages, avec le commentaire du code ; un bouton pour remettre une seule case.
- Pour les montagnes : un tremplin de saut à ski, un slalom avec des portes, des figures en snowboard, une course de boardercross contre les autres skieurs, des records gardés par le navigateur, une dameuse, des flocons qui tombent, des canons à neige, un téléski, redescendre par la télécabine, et les montagnes visibles de loin (une silhouette qui échappe au brouillard).
- Des missions qui utilisent la grande carte : courses de bateau, livraisons à Paleto Bay.
- Des braquages à refaire, avec un receleur qui rachète le butin, et des coéquipiers (un chauffeur, un pirate informatique) ; la police qui barre les routes et fonce dans la voiture du joueur.
- Des étages visitables dans les tours, des portes qui s'ouvrent et des habitants dans les appartements, des fenêtres percées ; un receleur qui rachète le butin des immeubles.
- Un parachute pour sauter du gratte-ciel ou d'un avion, un hélicoptère sur l'hélistation du gratte-ciel Maze Bank, des missions en avion (une livraison à Sandy Shores) et une course d'hélicoptère.
- Des guerres de gangs, des gangs en voiture, une mission pour nettoyer un quartier.
- La grande roue de Del Perro et le panneau Vinewood.
- Cycle jour et nuit, avec les lampadaires allumés.
- Effets d'image (halo autour des lumières, coins assombris) : essayés puis retirés. En plein jour, le halo délave toute l'image et les coins assombris ne se voient presque pas, pour un coût élevé. À retenter avec la nuit.
- Missions au choix, avec des marqueurs sur la carte.
- Des policiers qui mettent un moment à viser : ceux qui descendent d'un fourgon rateraient leurs premières balles, le temps de courir se cacher.

## Journal des modifications

Ce qui a été ajouté ou changé dans le jeu, jour par jour, le plus récent en premier. Les règles et les chiffres eux-mêmes sont dans les chapitres plus haut.

### 1er octobre 2026

- Les balles laissent des impacts : un trou entouré de plâtre arraché sur les murs, les planchers et les meubles, un trou dans la tôle des voitures. Les balles ratées des ennemis continuent jusqu'au mur derrière B.J. Réglages `impactsMurs`, `impactsVoiture` et `tailleImpacts`.
- La station de ski devient un vrai domaine skiable : une télécabine et deux autres télésièges (tableau `REMONTEES`), des sièges débrayables qui ralentissent dans les gares, avec un garde-corps qui se baisse, des poulies sur les pylônes, huit pistes balisées (tableau `PISTES_SKI`) avec des kickers, un boardercross chronométré, et d'autres skieurs sur les pistes et les remontées.
- Une tenue de glisse pour B.J. (tableau `TENUES_GLISSE`), des bâtons de ski, une neige qui s'en va par plaques en descendant, et des pentes qui varient.
- À ski, le saut ne monte plus qu'à 1 m, on ne déchausse plus qu'en tombant de très haut, B.J. ne s'enfonce plus dans la pente en tournant, ses skis sont à ses pieds sur le télésiège, et son siège est un vrai siège de la remontée.
- Le numéro de version ne disparaît plus quand GitHub ne répond pas (trop de demandes dans l'heure, ou pas d'Internet) : le navigateur garde le dernier numéro reçu et l'affiche.
- Code de triche `SUPERMAN` : le costume de Superman (collant bleu, slip et bottes rouges, ceinture jaune, le « S » sur la poitrine, cheveux noirs), avec une cape rouge qui flotte au vent.
- Avec les codes `SUPERMAN` et `DIEU`, une 9e arme, les yeux laser (touche 9) : deux rayons rouges qui partent des yeux, 15 tirs par seconde, sans munitions.
- Avec les codes `SUPERMAN` et `DIEU`, tomber de haut ne fait plus mal : B.J. se reçoit sur un genou, les gens et les voitures autour de lui sont écrasés, le sol se fissure, et de plus de 10 m il passe à travers le toit et les planchers des bâtiments où l'on entre (réglages `rayonEcrase`, `rayonEcraseMax`, `degatsEcrase`, `hauteurCasseToit`).
- Les ennemis ne voient plus B.J. et ne le touchent plus à travers les murs : un mur, un plancher ou un meuble arrête la vue et les balles, même un mur de 30 cm.
- Le code `DIEU` habille B.J. en Zeus : cheveux et barbe blancs, tout nu avec juste un pagne en paille et des santiags.
- Le soutien-gorge du code `SOUTIF` est refait : deux bonnets bordés de dentelle, une bande, une agrafe et deux bretelles.
- Bouton 🎮 Codes de triche dans le menu : la liste de tous les codes, faite à partir du tableau `TRICHES`.
- Ce qui vole penche dans ses virages : l'hélicoptère et Superman comme l'avion, jusqu'à 36°, réglage `roulisVirage`.

### 30 septembre 2026

- De très hautes montagnes enneigées à l'est, le mont Gordo et le San Chianski (tableau `SOMMETS`), avec une station de ski (`Y`), son télésiège, et des skis, un snowboard et une luge.
- La carte passe de 48 à 74 colonnes.
- Plus de gros bouchons : les voitures qui circulent regardent là où elles vont, font vraiment demi-tour quand elles restent bloquées, se laissent passer quand elles se croisent dans un carrefour, et prennent une autre rue quand la leur est bouchée.
- Numéro de version sous le titre du menu : le nombre de commits du jeu sur GitHub.
- Superman tire en volant, et chaque appui sur Maj le fait voler plus vite, jusqu'à 360 km/h.
- Le heavy robot écrase les gens et les voitures sur son chemin, et deux robots ne passent plus l'un à travers l'autre.
- Une voiture qui explose après un long accident retombe par terre au lieu de rester figée en l'air.
- Maj 3 fois de suite fait voler B.J. comme Superman.
- Le code `IDDQD` rend invincible, comme `DIEU`.
- Les membres des personnages ont du poids : ils traînent quand le corps tourne, pendent, claquent par terre et y restent, sans plier à l'envers.
- Les morts s'effondrent tout mous, les personnages renversés ou soufflés tournent aussi de côté, et un coup fait partir le buste et la tête.
- B.J. garde sa pose en l'air pendant tout le saut, son buste et ses bras continuent sur leur lancée quand il atterrit, ses bras et ses jambes battent quand il sort très vite d'une voiture, et il se déplie à la fin d'une roulade.
- La caméra ne voit plus à travers les murs, les cloisons et les plafonds.
- Les étages de la façade continuent au-dessus des portes.
- Le carrelage de la salle de bain ne barre plus sa porte.
- Chacun son tour : seuls les 2 policiers les plus proches qui voient B.J. peuvent le toucher, les autres tirent à côté, pour qu'on ne meure plus en 4 s quand un fourgon blindé arrive à 4 ou 5 étoiles.
- Le son des moteurs : crépitement, petit silence à chaque changement de vitesse, claquements d'échappement quand on lâche l'accélérateur.
- La voiture qui passe s'entend de son côté, plus aiguë quand elle approche (effet Doppler) et plus sourde de loin.
- Le nom du véhicule s'affiche quand on monte dedans.
- Tomber de haut fait mal.
- Sauts, chutes, atterrissages sur un genou et roulades de B.J.
- Sauter d'une voiture lancée le fait rouler par terre.
- Les personnages s'effondrent en mourant, volent quand une voiture les renverse ou qu'une explosion les souffle, vacillent ou tombent quand B.J. les bouscule, et se relèvent.
- Des meubles dans les immeubles où l'on entre : appartements, lofts et bureaux.
- Des objets à voler et des bonus.
- Moto, Segway, DeLorean, Coccinelle, Skoda Kodiaq, Audi TT, Lamborghini, Rolls-Royce, Audi Quattro de rallye et Austin Mini.
- On se pose sur le toit des immeubles pleins, et plus 60 cm dedans.
- Écran des réglages ⚙ dans le menu, pour changer `REGLAGES`, `ARMES`, `ARMES_ROBOT`, `VOITURES` et `ENNEMIS` sans toucher au code.
- Nouveau tableau `ENNEMIS` : la vie, l'arme, les dégâts, la précision, la vue, la cadence de tir et la vitesse de chaque ennemi.
- Codes de triche `ARMES`, `WAFFEN` et `WEAPONS`, d'autres noms pour `IDKFA`.
- `DIEU`, `GOD` ou `GOTT` rend invincible.

### 29 septembre 2026

- Immeubles où l'on entre : des étages, et le toit par l'escalier, une échelle ou un escalier de secours, ou une terrasse.
- Avions et hélicoptères à piloter à l'aéroport.
- Dos d'âne dans les rues.
- Gangs dans leur quartier.
- Roquettes un peu plus rapides.
- Une voiture en toupie renverse les piétons et pousse les autres voitures.
- Une borne restée sous la voiture ne la bloque plus.
- Codes de triche `RICHE` (100 000 $), `GOKU`, Super Saiyan, et `Z6PO` ou `C3PO`, un robot doré plus lent et plus solide.
- Menu des langues : français, allemand, anglais et züritüütsch, enseignes comprises.
- Légende de la grande carte.
- Foule au choix dans le menu, piétons et voitures : Peu, Normal, Beaucoup ou Énorme, Beaucoup au départ.
- Accidents : tonneaux, tête-à-queue et voitures qui décollent selon la force du choc, voiture couchée qui brûle puis explose, carrosserie qui s'écrase là où ça tape et d'autant plus que c'est fort, vitres brisées sombres avec des éclats, lampadaires qui tombent, bornes en béton autour des places, pneus qui crèvent sous les balles.
- Tirer sur une voiture touche celui qui la conduit, et le tuer donne une étoile.
- Une voiture trop abîmée prend feu, puis explose.
- Un son au volume impossible ne fige plus le jeu.

### 28 septembre 2026

- Braquages : voiture blindée façon Mad Max, musée, bijouterie Vangelico, banque Pacific Standard.
- Police en force à 4 et 5 étoiles, heavy robot pilotable.
- Codes de triche `IDKFA` et `MISSION` + numéro.
