## Fetch

Le fetch c'est une histoire de promesses...

Il n'y en a pas une à tenir mais 2 !

- *Tout d'abord, qu'est ce que c'est ?*
  
  C'est une méthode pour faire des requêtes HTTP pour obtenir (GET), créer (POST), supprimer (DELETE), et mettre à jour (PUT/PATCH) des données.

- *à quoi ça sert ?*

    Elle est utilisée pour accéder à des ressources sur le Web ou pour interagir avec des APIs.

- *2 promesses ?*
   - La première promesse est retournée par fetch() lui-même. Cette promesse résout un objet Response qui contient les détails de la réponse HTTP, tels que le statut de la réponse, les en-têtes, etc. Cependant, cet objet Response ne contient pas directement les données de la réponse. Pour accéder aux données de la réponse, vous devez utiliser une méthode comme .json() ou .text(), en fonction du format des données.
    - La deuxième promesse est celle renvoyée par les méthodes comme .json() ou .text(). Cette promesse résout les données de la réponse dans le format spécifié. C'est pourquoi vous devez utiliser await une deuxième fois, ou utiliser une autre méthode .then(), pour attendre que cette deuxième promesse soit résolue.

Donc, pour obtenir les données de la réponse d'une requête fetch(), on doit gérer deux promesses successivement. La première est pour obtenir l'objet Response, et la deuxième est pour obtenir les données réelles de la réponse.

- *Comment ?*
  
   - Soit par un try/catch async/await (ma version préférée) : 

```js
// On va utiliser try...catch pour gérer les erreurs de façon élégante.
try {
  // On fait une requête fetch à une URL spécifique. Dans ce cas, j'ai pris comme exemple la route card/:id de ton parcours 'http://localhost:1234/card/:id'.
  // La méthode par défaut est 'GET', c'est pourquoi il n'y a  pas besoin de spécifier la méthode ou le corps de la requête (body) en second argument.
  // Si tu voulais faire une requête 'POST', nous pourrions décommenter ce second argument que je t'ai laissé ci-après à titre d'exemple, attention ici c'est un get donc pas de récupération de données dans le body !
  const response = await fetch('http://localhost:1234/card/${id}'); 
  //{
    //method: 'POST',
    //body: formData
  //});

  // Vérifier si la réponse est OK (c'est-à-dire si le statut HTTP est entre 200 et 299).
  // Si la réponse n'est pas OK, nous lançons une erreur.
  if(!response.ok) {
    throw new Error('Erreur de chargement des données');
  }

  // À ce stade, nous avons reçu la réponse de la requête, mais nous devons encore obtenir les données réelles de la réponse.
  // Nous utilisons la méthode .json() pour transformer la réponse en JSON. Cette méthode retourne une promesse, donc nous utilisons un second 'await' pour attendre que cette promesse soit résolue.
  // Enfin, nous assignons les données JSON à la variable 'oneCard' par exemple.
  const oneCard = await response.json();
      
} catch(error) {
  // Si une erreur est survenue à n'importe quel moment pendant le processus ci-dessus, on gère l'erreur ici.
  // Dans ce cas, on va simplement afficher l'erreur dans la console ainsi qu'une alerte avec l'erreur.
  console.error('Erreur :', error);
  alert(error);
}
```
C'est une bonne pratique de toujours gérer les erreurs lors de l'utilisation de fetch(), car il y a plusieurs points où les choses peuvent mal se passer (par exemple, si le serveur ne répond pas, ou si le JSON reçu est mal formé). Utiliser try/catch et vérifier response.ok sont deux points importants pour gérer ces potentielles erreurs.

- Soit avec les .then, avec un then par promesse (on peut aussi d'englober cette façon de faire par un try catch) :

    ```js
    fetch(`http://localhost:1234/card/${id}`)
        .then(response => {
            if (!response.ok) {
            throw new Error("Erreur HTTP: " + response.status);
            }
            return response.json();
        })
        .then(data => {
            console.log(data);
            // Ici, vous pouvez utiliser 'data' pour afficher les détails de la carte dans votre interface utilisateur
        })
        .catch(function(error) {
            console.log('Erreur :', error);
        });
    ```



Voilà j'espère t'avoir éclairer sur les fetch, n'hésite pas à revenir sur une de mes explications si elle n'était pas assez clair.
