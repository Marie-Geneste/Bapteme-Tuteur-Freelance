## Correction MCD

Tout d'abord, voici les ressources utiles et nécessaires pour créer un MCD sans failles : 

- MCD : 
        https://kourou.oclock.io/ressources/fiche-recap/mcd-modele-conceptuel-de-donnees/
- MLD : 
        https://kourou.oclock.io/ressources/fiche-recap/mld/
- Mocodo : 
        https://kourou.oclock.io/ressources/fiche-recap/mocodo/
  
J'ai mis aussi la fiche récap du MLD parce que les 3 règles évoquées dans cette fiche aide énormément à la compréhension des cardinalités.

Mocodo est un excellent outil pour faire un mcd car il fait le design du schéma automatiquement, on a juste à rentrer la logique de nos table dans l'encadré prévu à cet effet. Il faut juste prendre en main la façon dont on transcrit cette logique et pour cela, il y a la fiche récap o'clock Mocodo ou bien une explication directement sur leur site https://www.mocodo.net/

Revenons à ton MCD, la principale erreur est au niveau des cardinalités de la relation que tu as bien identifié de Many-to-Many. Un user peut like plusieurs produits donc N en cardinalité max côté user. Un produit peut être aimé par plusieurs utilisateurs, là aussi N en max. Inversement, je pense qu'un user peut exister sans favori et un produit peut être aimer de personne donc là aussi des deux côté la cardinalité minimale est de 0 et non 1.

Comme cité dans la fiche récap du MLD : "Attention : Si les deux cardinalités max. valent 1, il est possible qu’il y ai une erreur de conception et que les 2 entités n’en soit en fait qu’une.". Bon là c'était soit une erreur d'interprétation soit une erreur de frappe pour les 1 en max des 2 côtés qui sont en fait des N.

Ton MCD a donc 2 relations Many to Many :
- User Like Product
- Order Contain Product

Après ça, il y a encore quelques détails à régler  :

- attention à ne pas mettre de snake case dans un MCD comme dit dans la fiche récap du MCD : "De plus, on écrit les attributs en langue naturelle (avec des espaces et sans underscores), Nom ville, Date emprunt, Age du capitaine : pas de snake_case 🐍"
- "Le déterminant qui identifiera l’entité, est souligné (premier champ)."
- On ne parle pas encore d'id dans le mcd, le déterminant peut être un nom, un code (l'isbn du livre) ou si on veut lui donner un id fabriquer sur le coup on peut l'appeler CodeUser par exemple.
- Je vois un champs Mug Type dans l'entité Product. Il serait peut-être intéressant d'en faire une entité à part entière comme un tag ou une catégorie propre à chaque mug. Product Belongs To MugType ?

Voici ton mcd corrigé sur Mocodo et le code que j'ai utilisé pour le générer : 

    HAS, 11 Address, 0N User
    Address: CodeAdresse, Adress, City, Postal Code

    User: CodeUser, Email, Password
    LIKE, 0N Product, 0N User

    GENERATE, 0N User, 11 Order
    Product: CodeProduct, Name, Description, Mug Type, Amount

    Order: CodeOrder, Total Amount, Status
    CONTAIN, 1N Order, 0N Product

[![Image](https://i.goopics.net/v8f4gr.jpg)](https://goopics.net/i/v8f4gr)
