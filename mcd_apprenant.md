# Retour sur un MCD d’un.e apprenant.e

La réalisation d'un MCD demande une attention particulière quant à la définition des règles de gestion métier, qui est
une étape clé de la méthode `MERISE`.
J'insiste sur ce point, car il y a une erreur sur le MCD que tu as réalisé.

Afin que la correction soit explicite, je vais comparer les règles de gestion métier qui sont à couvrir, avec ce que
tu as réalisé et voir si elles concordent.

### Règles de gestion métier :

1. *Un utilisateur peut créer sur son compte une ou plusieurs adresses de livraison.*<br>
   *Une adresse de livraison est créé par un seul utilisateur.*
2. <span style="color:red">Un utilisateur peut liker zéro ou plusieurs produits.<br>
   Un produit peut être liké par zéro ou plusieurs utilisateurs.</span>
3. *Un utilisateur peut passer zéro ou plusieurs commandes.*<br>
   *Une commande est passée par un seul utilisateur.*
4. *Une commande contient un ou plusieurs produits.*<br>
   *Un produit peut être dans zéro ou plusieurs commandes.*

Sur ton MCD, tu as donc fait une erreur sur la relation entre l'entité `User` et l'entité Product`.
En effet, lorsqu'on lit le schéma, ça nous dit :
- *Un utilisateur peut liker qu'un seul produit*
- *Un produit peut être liké par un seul utilisateur*

Il faut donc changer les cardinalités, et voici la correction ;

> |User| (0,n) <---LIKE---> (o,n) |Product|

<hr>
   
>Pour la réalisation de MCD, plusieurs outils (gratuit ou payant) sont disponibles, comme Lucidchart, diagram.io, GitMind, Visual Paradigm, etc...
Me concernant, j'utilise JMerise, certes il date un peu, mais me convient parfaitement grâce à sa facilité d'utilisation.

[RETOUR](/README.md)
