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
4. Si la modification change les touches, les armes, la carte ou les missions, mets aussi à jour `README.md`.

Une modification n'est pas terminée tant que `DESIGN.md` ne correspond pas au code.
