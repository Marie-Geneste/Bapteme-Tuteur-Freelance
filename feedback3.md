## Feedback 3

Il y a des choses intéressantes dans le code que tu as fournis mais il y a quelques problèmes de logiques et de compréhensions. 

Je vais essayer de te guider au mieux à travers les éléments à revoir :

- Les vues ejs : 
  - cardList : attention le lien "a" ligne 11 était déjà fermé ligne 16. Le fait de l'avoir fermer ligne 11 fait sortir l'image et le nom du lien, ce qui est fort dommage car on ne peut plus cliquer grossièrement sur l'image d'une carte pour atterrir sur son détail.
  - cardDetails : quand tu as fait le controller correspondant tu as nommé la carte trouvée via l'id oneCard. Cette variable est envoyée à ta vue ejs avec ce nom là. Or dans la vue ejs, tu as copié la variable présente dans cardList, ce qui ne fonctionne pas. D'ailleurs, l'erreur te le dit bien : "card is not defined". Il ne trouve pas de variable nommé "card", ce qui est normal car tu lui as envoyé "oneCard". Mais même en réglant cette erreur de nom, un autre problème va survenir.
  En effet, tu fais une boucle sur une variable qui renvoie UN seul élément et non pas un tableau. Il faut se rappeler que dans le controller, tu as cherché la carte correspondante à un id précis. Donc dans la vue ejs, pas besoin de se compliquer la vie avec une boucle, tu as déjà la carte que tu veux. 

- La notion de middleware : 
  - C'est vrai que ce n'est pas facile de savoir quand next (et je ne parle pas de l'émission). Dans tes controllers, tu fais globalement "si je n'ai pas le résultat attendu, je next". La logique est bonne mais il ne faut pas toujours next. En effet, parfois ce que l'on veut ce n'est pas de passer au middleware suivant mais au contraire d'avoir un message d'erreur disant que le problème est ici. Donc par exemple : `res.status(500).send('impossible d\'enregistrer l\'élément...');`.
  En revanche si le middleware suivant est une erreur 404, il peut être intéressant de next si le res.statut de l'erreur est bien 404.
  - Dans l'index.js à la racine, tu as appelé cardPage avant le notFound alors qu'il est déjà appelé dans le router (donc quand tu fais une action précise). Si tu l'appelles ici, le middleware sera en attente dans la liste des choses à effectuer avant de passer au middleware suivant. De ce fait, ton notFound ne pourra jamais fonctionné.

- La notion de query/params : 
  - Pour commencer un peu de doc officiel mais en anglais (always!) : https://expressjs.com/en/api.html#req.params
  https://expressjs.com/en/api.html#req.query
  En gros : params permet de récupérer ce qu'il y a après les ":" dans un url et query permet de récupérer les valeurs après le "?"
  - Pour récupérer l'élément dans ta méthode searchElement du controller, tu utilises req.params au lieu de req.query. En effet, si tu remarques l'url ressemble à ça quand tu sélectionnes une valeur dans l'input : http://localhost:1234/search/element?element=tonnerre
  - Il faut donc penser à mettre des console.log pour voir quelle valeur tu récupères et ainsi pouvoir te corriger facilement.
  - Malgré cette confusion, tu as oublié d'envoyer l'élément récupéré dans le dataMapper en argument de la méthode "getCardByElement". Ainsi tu aurais pu indiquer de quel élément il s'agit pour la requête avec un "WHERE element=$1", [element]. Le IS NOT NULL n'est pas une mauvaise idée mais pour l'inverse : c'est-à-dire pour la selection "aucun élément" la requête était bien "WHERE element IS NULL".

  Voilà les différents éléments à travailler que j'ai pu voir dans ton code. Maintenant je te conseille de suivre attentivement un élève ECP pour voir la logique utilisée en plus de la correction d'O'Clock. Tu peux aussi refaire le parcours à tête reposée et avec la correction sous les yeux, c'est un excellent exercice.

  Je vais finir sur des notes positives : il n'y a pas de failles au niveau des injections SQL, le code est clair au niveau des noms choisis et il y a quelques commentaires, ce qui est bien.
