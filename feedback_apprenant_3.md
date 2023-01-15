# FEEDBACK APPRENANT 3

### Points à améliorer

- **Gestion des routes**
  - Beaucoup de routes sont manquantes.
  - La gestion des routes doit être exportée dans une autre classe, afin de ne pas surcharger le fichier `index.php`.
- **Model**
  - Il manque le model AppUser, qui permet aux utilisateurs du backoffice de s'authentifier
  - Tu ne profites pas de l'héritage, car tu as une généralisation du model `Teacher` et `Student` vers la classe `CoreModel`. Cette généralisation te permet d'extraire certaines propriétés redondantes, afin de les définir qu'une seule fois.
  - Il manque quelques méthodes te permettant de faire un `CRUD` complet. Il faudra que tu prennes le temps de comparer avec la correction, pour trouver les méthodes manquantes.
- **Controller**
    - _CoreController_ :
      - Le `CoreController` est manquant, c'est une classe importante dans ce projet, car elle a la responsabilité de regrouper les fonctionnalités qui ne sont pas liées au métier.
    - _MainController_ :
      - Ce controller a pour seul but de rediriger l'utilisateur vers la page d'accueil, et donc il aurait fallu extraire la méthode `show()` et la placer dans le `CoreController`.
    - _StudentController_ :
        - Ajout d'un étudiant :
            - Plusieurs erreurs sont à noter :
                - La première étape est de tout d'abord vérifier la validation des champs et de s'assurer que les champs ne sont pas vides.
                - Ensuite, et seulement à ce moment-là tu instancies le model. Cela te permet d'éviter d'instancier un objet alors que des erreurs sont présentes.
                - Il te manque la propriété `teacherId`, d'où l'erreur ` General error: 1364 Field 'teacher_id' doesn't have a default value in /var/www/app/Models/Student.php on line 39
                - Fais attention à la propreté de ton code, en respectant l'indentation, en supprimant les commentaires non pertinent. Pense aussi à documenter de façon plus exhaustive ton code.
                - Tu seras amené à travailler en équipe, et tu devras respecter des conventions et t'assurer que ton code est clair et compréhensible par tous !
        - Ce controller n'est pas complet, car il te manque toutes les autres méthodes te permettant de couvrir le CRUD du use case Student.
    - _TeacherController_ :
        - Les remarques sur ce controller sont identiques à celui du StudentController.
        - Concernant la méthode `studentAdd()`, une erreur majeure est présente, car tu initialises la variable `$newTeacher` sans l'utiliser ensuite, mais en utilisant une variable indéfini à la place...

### Points positifs :
- Le contrat n'est malheureusement pas rempli pour ce TP, néanmoins, tu peux toujours rattraper.
- N'hésite pas à revoir la `POO` et toutes les notions concernant l'héritage et l'encapsulation.
- N'hésite pas à revenir vers moi si tu as d'autre question

[RETOUR](/README.md)