## Feedback 1

Bravo, le code est très bien et ton organisation est logique. Tu as mis la méthode pour renvoyer vers une card dans le bon controller malgré la consigne qui évoque le mainController, tu as su résister et utiliser ta logique pour la mettre dans le cardController.

Ensuite, je tiens à te féliciter pour tes noms de méthodes qui sont très claires : des noms clairs = un code compréhensible et réutilisable par d'autres personnes donc un très bon point pour la vie pro !

Attention, pour les commentaires explicatifs tu en as mis dans le cardController et dans le router mais pas dans le reste du code. N'hésite pas à en glisser plus par ci, par là.

`(searchedElement === 'null' ? ' sans élément' : + searchedElement)`
C'est très bien d'avoir essayer de faire un ternaire, très bon réflexe.
En revanche, pour afficher une variable il faut utiliser un littéral de gabarit (tu sais le ``${}``) et le + était de trop :D
`searchedElement === null ? '' : ``${searchedElement``}`

J'ai vu que tu as essayé de faire avec un searchByElementNull() pour la recherche par élément. Tu t'es corrigé et l'a commenté dans le controller. En revanche, attention il est toujours présent dans le dataMapper.

Pour la recherche par valeur, tu as utilisé un regex, c'est très ingénieux mais tu as inséré une variable directement dans la requête : attention aux injections SQL même si là ce sont des inputs qui ne permettent pas d'écrire ce que l'on veut. Je te laisse voir la correction pour une approche différente.

Pour conclure, c'est de l'excellent travail : tout fonctionne avec les bonus. Un grand bravo pour la clarté du code, il manque encore quelques commentaires et des touts petits détails à régler mais tout est bien assimilé et la logique du code est là.


