## Feedback 2

Bravo pour ta persévérance, tu n'as rien lâché et tu as continué pour au moins essayer de réussir le deck. C'est un très bon état d'esprit qui est essentiel et qui te permettra d'aller très loin.

Bravo pour le travail accompli : on peut cliquer sur une card et afficher son détail (même si la view ejs mériterait un peu plus de travail) et on peut ajouter des cards au deck.

Je vais maintenant reprendre point par point en suivant le plan du parcours pour les éléments à revoir :

- Le DataMapper :  
Je te met un warning pour ta requête sql : attention aux injections ! Il faut vraiment éviter de mettre une variable dans une requête. Pour ce faire, on utilise un paramètre avec des $1, $2, $3... Comme suit :

`const query = ``SELECT * FROM "card" WHERE "id" = $1``;`
`const result = await database.query(query, [id])`

Je te laisse voir la construction de toutes les autres requêtes du DataMapper dans la correction. Tu peux t'entraîner à faire ce que tu n'as pas fais avec la correction sous les yeux et avec de la pratique ça va venir tout seul !
Voici le lien vers la fiche récap pour les injection sql : https://kourou.oclock.io/ressources/fiche-recap/injections-sql/

- Les noms des variable/méthodes :
  Ne pas mettre de commentaires est une chose (qu'il faudra aussi travailler :D) mais avoir des noms peu clair est encore moins convenable. Il faut penser à ton futur toi (et aux autres accessoirement, très important pour travailler en équipe et donc en entreprise) qui relira ton code dans un différent état d'esprit et ne comprendra plus ce que tu voulais dire par "item" ou encore "getSearchResults" (quels résultats ?). Encore une fois je te laisse t'inspirer des noms en correction.

- Alt des images :
Dans les views ejs, attention à l'oubli du alt des images qui est très important pour le référencement et l'accessibilité.

- Conseils pour le deck :
    - On ajoute une carte au deck donc le nom de la méthode la plus approprié serait addCard.
    - Il y aurait pu avoir fusion du cardControlller et du deckController.
    - C'est toujours mieux de créer la session dans un middleware à part pour faciliter sa réutilisation.
    - Un deck est censé s'arrêter à 5 cartes, il faut gérer ce détail dans ton controller.

Pour aller plus loin, tu peux essayer dorénavant d'utiliser des console.log pour voir ce que ton code fais à chaque instant et ainsi pouvoir adapter ta logique par rapport aux résultats attendus.

Dans l'ensemble c'est bien, il y a des choses à revoir mais je suis sûre que tu as toutes les ressources pour te perfectionner.

