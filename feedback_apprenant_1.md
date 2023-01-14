# FEEDBACK APPRENANT 1

### Points à améliorer

- **Gestion des routes**
  - La gestion des routes doit être exportée dans une autre classe, afin de ne pas surcharger le fichier `index.php`.
- **Model**
  - Tu as pu remarquer que les models `Teacher` et `Student` ont une propriété commune `status`, et au lieu de la définir à deux endroits différent, il est mieux de la définir dans la classe parente `CoreModel`
- **Controller**
  - _UserController_ :
    - Liste des utilisateurs :
      - Le nom de la méthode doit être plus explicite, car en la nommant `user` on ne sait pas trop si elle affiche un ou plusieurs utilisateurs
    - Authentification :
      - Dans la méthode `signin`, il faudrait envoyer des données à la vue, avec notamment le token anti-csrf
      - Dans la méthode `signinPost`, il faut mettre en place une validation des données sur l'email et le password de façon séparée, afin de donner une information claire à l'utilisateur sur la nature des erreurs d'authentification. <br/>
        Concernant la redirection lors d'une authentification réussie, tu aurais pu exporter cette logique dans le `CoreController`, avec par exemple une méthode appelée `redirectToRoute`, ce qui permet d'éviter la duplication, et d'améliorer l'évolutivité et la maintenabilité de ton code. 
  - _CoreController_ :
    - Constructeur :
      - Concernant la logique des acces control, la bonne pratique est de créer un fichier à part listant toutes les règles d'accès.
    - Gestion des autorisations :
      - L'utilisation du router est nécessaire que dans la condition où l'internaute n'est pas connecté à un compte, il est donc préférable de charger le routeur seulement dans cette condition afin d'améliorer la performance lors de la compilation du code.
      - Concernant l'affichage de la page d'erreur, tu aurais pu appeler la méthode `error403()` présente dans la classe `ErrorController` afin de ne pas dupliquer cette logique.
  - _StudentController_ :
    - Liste des étudiants :
      - Tu peux faire appel à la méthode statique `findAll` de cette manière `Student::findAll()`, cela te permet d'éviter d'instancier la classe `Student` et donc de gagner en performance.
    - Ajout d'un étudiant :
      - Plusieurs erreurs sont à noter :
        - La première étape est de tout d'abord vérifier la validation des champs et de s'assurer que les champs ne sont pas vides.
        - Ensuite, et seulement à ce moment-là tu instancies le model. Cela te permet d'éviter d'instancier un objet alors que des erreurs sont présentes.
        - Fais attention à la propreté de ton code, en respectant l'indentation, en supprimant les commentaires non pertinent. Pense aussi à documenter de façon plus exhaustive ton code.
        - Tu seras amené à travailler en équipe, et tu devras respecter des conventions et t'assurer que ton code est clair et compréhensible par tous !
    - Édition d'un étudiant :
      - Il ne faut pas instancier un nouvel étudiant ou un nouveau professeur. Ces deux instanciations sont inutiles, car tu récupères l'étudiant par son id et la liste de tous les professeurs.
      - Il te faut aussi passer l'id de l'étudiant à éditer dans la vue, car tu en auras besoin lors de la soumission du formulaire pour pointer sur le bon étudiant à modifier.
    - Suppression d'un étudiant :
      - Tu n'as pas besoin d'initialiser un tableau contenant les erreurs, car lors de la suppression, il n'y a pas de validation à mettre en place.
      - Il te faut aussi, vérifier que l'étudiant à supprimer et bien en base avant d'envoyer la requête.
  - _TeacherController_ :
    - Les remarques sur ce controller sont identiques à celui du StudentController.

### Points positifs :
  - C'est un travail complet, certes il y a encore des choses à améliorer, mais tu peux être fier de ta réalisation, car en trois heures ce n'était pas évident de couvrir l'intégralité du sujet.
  