## Feedback 4

Bon je vois que tu as eu du mal pour ce parcours, pas de panique : avec du travail, tu surpasseras toutes les difficultés.

Je vais te guider sur la première étape que tu as essayé de faire, point par point en suivant la consigne "avec aide".

- La méthode getCard dans le dataMapper: tu as pensé à mettre en argument l'id, ce qui est très bien. L'id sera récupéré grâce au controller (que l'on verra juste après) donc tu as bien fait de commenter la ligne du "targetID" ici mais c'est dommage que tu ne l'aies pas mis dans le controller parce qu'elle est parfaite !
TU as juste fait un petit oubli dans cette méthode : tu as bien protéger ta requête contre les injection SQL en mettant un $1 mais il ne faut pas oublié dire à quoi ce $1 correspond : 
```js
const query =
    `
      SELECT *
      FROM "card"
      WHERE "id" = $1
    `;
    const result = await database.query(query, [id]);
```
- La méthode getCard dans le controller : comme dit plus haut, il manque la ligne de code parfait pour récupérer l'id donc : `const targetId = Number(request.params.id);`. 
Tu mets cette id en argument de la méthode getCard du dataMapper : `const card = await dataMapper.getCard(targetId);`
Et ensuite il faut mettre la variable card dans la vue ejs comme suivant : `res.render('card',{card});`
Ainsi on pourra l'utiliser dans la view ejs card.ejs.

- Les vues ejs : 
  - tu as copié collé le card.list.ejs dans la vue card.ejs. C'est une idée mais il faut modifier des points importants : 
    - attention à ne pas laisser la boucle. La valeur envoyer dans cette vue ejs est une seule carte récupérée par un seul ID donc dans la variable card il n'y a pas un tableau sur lequel on peut boucler mais qu'un seul élément. Donc on peut directement utiliser "card.name" ou bien "card.id" sans boucle for.
    - faire aussi attention au nom de la variable que tu récupère du controller getCard, ici le nom est card et non cards.
  - le href de la vue cardList.ejs est à changer si tu veux diriger vers la route correspondant à /card/:id comme par exemple : /card/<%= card.id %> comme cela la route est bien paramétré avec l'id correspondant à la carte.

- La route paramétrée dans le router : il ne reste plus qu'à déclarer dans le router la route paramétrée (avec un /:id après le /card) avec l'appel à la méthode du controller correspondant et le tour est joué !

N'hésite pas à me demander plus de clarifications sur un des points ci-dessus.

Je te conseille vivement de faire cette étape 1 maintenant, après mes explications, pour voir jusqu'où tu peux aller. N'hésite pas à tester tes variables avec un console.log si tu as le moindre doute et analyse bien les erreurs de code pour te débloquer.
Ensuite, essaye de suivre la correction d'un élève ECP pour voir sa logique de code. 
Puis tu peux faire le reste du parcours avec la correction sous les yeux, c'est un excellent exercice.

