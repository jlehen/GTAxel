# Consignes pour les agents

GTAxel est un jeu 3D dans le navigateur, entièrement contenu dans `index.html`. Il est fait pour qu'un enfant de 10 à 13 ans puisse le bidouiller : le code et les commentaires sont en français.

## Modifier le jeu

1. **Avant de toucher au code, lis `DESIGN.md`.** Il décrit le jeu tel qu'il est : piliers de design, règles, chiffres d'équilibrage et plan du fichier. Respecte les piliers, surtout « pardonnant » et « bidouillable ».
2. **Implémente la modification** dans `index.html`, dans le même style que le code autour. Les valeurs qu'un enfant voudra changer vont dans les zones en haut du fichier (`REGLAGES`, `ARMES`, `CARTE`, `MISSIONS`).
3. **Mets ensuite `DESIGN.md` à jour** pour qu'il décrive le jeu après ta modification :
   - les règles et les chiffres qui ont changé (tableaux, vitesses, dégâts, etc.) ;
   - le plan du fichier, si des lignes ont bougé ;
   - les limites connues et les pistes, si ta modification en règle une ou en crée une ;
   - la date de mise à jour, en haut du document (la date seule, sans résumé) ;
   - le « Journal des modifications », tout à la fin : une puce par changement, en tête du jour concerné, le jour le plus récent en premier.
4. Si la modification change les touches, les armes, la carte ou les missions, mets aussi à jour `README.md`. Il parle des missions à plusieurs endroits, qui doivent suivre le code :
   - « Les missions du chapitre 1 » : une ligne par mission de `MISSIONS`, dans le même ordre, avec son `nom` et ce qu'il faut faire ;
   - « Malibu (chapitre 2) » : la liste numérotée des missions de `MISSIONS_MALIBU`, dans le même ordre, avec leur `nom` en gras, puis `DELOREAN_MANDARIN` en dernier ;
   - « Gotham (chapitre 3) » : la liste numérotée des missions de `MISSIONS_GOTHAM`, dans le même ordre, avec leur `nom` en gras, puis `DELOREAN_SPHINX` en dernier ;
   - « Metropolis (chapitre 4) » : la liste numérotée des missions de `MISSIONS_METROPOLIS`, dans le même ordre, avec leur `nom` en gras, puis `RETROUVER_DELOREAN` (« La DeLorean a disparu ») en dernier ; et la kryptonite (« La kryptonite », après « La super-force »), si ses règles ou ses réglages changent ;
   - les nombres de missions : « B.J. (les 11 missions) » dans le tableau des chapitres, « Malibu a ses 12 missions d'Iron Man », « Gotham, ses 12 missions de Batman » et « Metropolis, ses 8 premières missions de Superman » juste en dessous, et « C'est la 11e mission » au camp militaire ;
   - les exemples du code `MISSION` (`MISSION8` : le musée ; `MISSION11` : le camp militaire), dans « Les codes de triche » ;
   - les noms de mission cités ailleurs (la mission « Hulkbuster », au magasin de Stark Industries) ;
   - dans « Modifier le jeu », `MISSIONS` : les tableaux des étapes (dont « Et pour Iron Man », « Et pour Batman » et « Et pour Superman »), la liste des ennemis de `eliminer` (à Gotham, `homme`, `pingouin`, `bandit`, `doubleFace`, `mercenaire`, `bane`, `clown`, `joker`, `acolyte` et `sphinx` ; à Metropolis, `luthor` et `brainiac`) et les lieux (à Gotham et à Metropolis, `point`), si tu ajoutes un type d'étape, un ennemi ou un lieu ; et le tableau `DEVINETTES`, si tu changes sa forme ;
   - quand un autre chapitre reçoit ses missions (New York) : une section comme celles de Malibu, de Gotham et de Metropolis, et la phrase « New York n'a pour l'instant qu'une mission » à corriger ; quand Metropolis reçoit les suivantes, sa liste, son nombre (« ses 8 premières missions ») et la phrase « Les missions suivantes (...) arrivent bientôt ! », à la fin de sa liste.

   Pour n'en oublier aucun : `grep -n -i mission README.md`.

Une modification n'est pas terminée tant que `DESIGN.md` ne correspond pas au code.
