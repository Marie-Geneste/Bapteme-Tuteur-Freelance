## Feedback 2

Bravo pour ta persévérance, tu n'as rien lâché et tu as continué pour au moins essayer de réussir le deck. C'est un très bon état d'esprit qui est essentiel et qui te permettra d'aller très loin.

Je te met un gros warning pour la requête sql dans le dataMapper: attention aux injections ! Il faut vraiment éviter de mettre une variable dans une requête. Pour ce faire, on utilise un paramètre avec des $1, $2, $3... Comme suit :

`const query = ``SELECT * FROM "card" WHERE "id" = $1``;`
`const result = await database.query(query, [id])`

Je te laisse voir la construction de toutes les autres requêtes du DataMapper dans la correction. Tu peux t'entraîner à faire ce que tu n'as pas fais avec la correction sous les yeux et avec de la pratique ça va venir tout seul !

Il faut aussi faire un effort pour le nom des méthodes dans ton controller. Ne pas mettre de commentaires est une chose (qu'il faudra aussi travailler :D) mais avoir des noms peu clair est encore moins convenable. Il faut penser à ton futur toi (et aux autres accessoirement, très important pour travailler en équipe et donc en entreprise) qui relira ton code dans un différent état d'esprit et ne comprendra plus ce que tu voulais dire par "item" ou encore "getSearchResults" (quels résultats ?). Encore une fois je te laisse t'inspirer des noms en correction.

Dans les views ejs, attention à l'oubli du alt des images qui est très important pour le référencement et l'accessibilité.

Pour le deck, on doit ajouter une carte à la session si elle n'y est pas déjà et pouvoir la retirer (je te laisse voir ce dernier point dans la correction). Comme on veut une méthode qui ajoute une carte au deck (et non pas un deck) le nom le plus approprié serait : addCard dans le deckController. D'ailleurs, tu peux fusionner les fichiers card et deckController. 
L'ajout de cartes est réussi, et cela mérite mes félicitations !
Deux petits détails à revoir : c'est toujours mieux de créer la session dans un middleware à part pour facilité sa réutilisation.
Le deuxième point c'est qu'un deck est censé s'arrêter à 5 cartes, il faut gérer ce détail dans ton controller.

Pour aller plus loin, tu peux essayer dorénavant d'utiliser des console.log pour voir ce que ton code fais à chaque instant et ainsi pouvoir adapter ta logique et pour voir ce qu'il te manque pour avancer.

Dans l'ensemble c'est bien, il y a ,certes, des choses à revoir mais je suis sûre que tu as toutes les ressources pour te perfectionner.

