# Définition de la notion de fetch

> C'est une bonne chose que tu veuilles en savoir plus sur la notion de `fetch`, et bien accroches toi, car je vais dans cet exemple te montrer comment l'implémenter, en faisant une petite évolution directement dans ton code. 

## Qu'est que c'est `fetch` ?

`fetch` est une fonction JavasScript native qui permet de faire des requêtes Ajax.
Les requêtes Ajax sont des requêtes HTTP qui sont envoyées directement depuis le navigateur vers le serveur.
L'avantage de passer par une telle méthode, c'est de pouvoir effectuer une action sans avoir à recharger la page.
De plus, `fetch` permet de travailler avec les promesses (promises), ce qui permet de travailler de manière asynchrone.
L'asynchrone nous permet par conséquent d'exécuter une succession d'opérations les unes après les autres.
Ce qu'il faut comprendre, c'est qu'une opération sera lancée que si celle qui la précède est réussie.
Dans le cas où une opération n'est pas réussie, nous pourrons catcher l'erreur et la retourner dans les logs où dans une popup qui s'affichera et qui donnera la raison de l'erreur à l'utilisateur.

> Bon c'est bien beau tout ça, mais je vais t'expliciter cette notion en détaillant de manière concise les étapes à réaliser

## Use case : Suppression d'un étudiant

Dans cet exemple, nous allons supprimer un étudiant grâce au `fetch`, et donc depuis le navigateur.
Plusieurs étapes à réaliser seront nécessaires pour réaliser cette évolution.

### Steps :

1. Création d'un endpoint (c'est-à-dire d'une url) et donc une méthode directement dans le controller qui aura pour but d'intercepter la requête est de traiter la demande
2. Création de la logique en javascript permettant de supprimer un étudiant, et qui sera exécutée dans la vue qui affiche la liste des utilisateurs
   1. Il faudra tout d'abord créer une fonction, qui interceptera le click sur le bouton de suppression, et qui enverra ensuite l'id de l'étudiant à supprimer à notre endpoint nouvellement créé
   2. On traitera ensuite le retour la promesse
      1. Si c'est un succès, il faudra supprimer la ligne du tableau correspondant à l'utilisateur supprimé, et on affichera un message de succès
      2. Si c'est une erreur, on affichera un message d'erreur dans un console log

I. **Création du endpoint :**
1. *Création d'une nouvelle route pour ne pas écraser l'ancienne*
    ```php
    $router->map(
        'GET',
        '/student/[i:studentId]/delete-form-fetch',
        [
            'method' => 'studentDeleteFormFetch',
            'controller' => StudentController::class
        ],
        'student_delete_from_fetch'
    );
    ```
2. *Création de la méthode `studentDeleteFormFetch()`*
    ```php
    /**
     * Allow to delete a student
     * @param $studentId
     * @return false|string
     */
    public function studentDeleteFormFetch($studentId)
    {
        header('Content-Type: application/json');

        $result = Student::delete($studentId);RETOUR

        if ($result) {
            $message = "Utilisateur supprimé avec succès";
        } else {
            $message = "Erreur lors de la suppression de l'étudiant";
        }

        echo json_encode([
            "message"  => $message
        ]);
    }
    ```

II. **Création de la logique de suppression en js :**
1. *Adaptation de la vue `student_list.tpl.php` du code html :*
   ```php
      <tbody>
        <?php foreach($viewData["students"] as $student): ?>
        <tr id="student-row-<?= $student->getId() ?>">
            <th scope="row"><?= $student->getId() ?></th>
            <td><?= $student->getFirstname() ?></td>
            <td><?= $student->getLastname() ?></td>
            <td class="text-right">
                <a href="<?= $router->generate('student_update_get', [ "studentid" => $student->getId() ]) ?>" class="btn btn-sm btn-warning">
                    <i class="fa fa-pencil-square-o" aria-hidden="true"></i>
                </a>
                <div class="btn-group">
                    <button type="button" class="btn btn-sm btn-danger dropdown-toggle" data-toggle="dropdown"
                        aria-haspopup="true" aria-expanded="false">
                        <i class="fa fa-trash-o" aria-hidden="true"></i>
                    </button>
                    <div class="dropdown-menu">
                        <a class="dropdown-item"
                            onclick="deleteStudent(<?= $student->getId() ?>)"
                        >
                            Oui, je veux supprimer
                        </a>
                        <a class="dropdown-item" href="#" data-toggle="dropdown">Oups !</a>
                    </div>
                </div>
            </td>
        </tr>
        <?php endforeach; ?>
      </tbody>
   ```
   Ici on modifie la row, en lui affectant un id dynamique ` <tr id="student-row-<?= $student->getId() ?>">`, afin de pouvoir supprimer la ligne du tableau.<br>
   Ensuite on ajoute l'attribut `onclick` en renseignant la méthode javascript liée à la suppression d'un étudiant.
2. *Création de la méthode javascript `deleteStudent()` qui prend en paramètre l'id de l'étudiant à supprimer :*
   ```js
   const deleteStudent = (studentId) => {
           fetch(`http://localhost:5551/student/${studentId}/delete-form-fetch`)
               .then(response => response.json()) // Ici on reçoit la réponse du serveur, et on utilise la méthode json() pour analyser la réponse au format JSON et enregistrer les données dans la console.
               .then(data => {
                   // Affichage d'une popup de confirmation de suppression
                   Toastify({
                       text: data.message, // Ici on récupère le message de succès envoyé par la réponse
                       duration: 3000
                   }).showToast();
   
                   // Suppression de la ligne du tableau concernant l'étudiant supprimé
                   document.getElementById(`student-row-${studentId}`).remove();
               })
               .catch((error) => {
                   console.log(error) // Ici on affiche le message d'erreur
               });
       }
   ```
   > J'utilise la librairie [Tostify JS](/https://apvarun.github.io/toastify-js/) pour l'affichage des popup
   
J'espère qu'avec cet exemple, tu seras en mesure de comprendre l'intérêt de l'utilisation de fetch. N'hésite pas à revenir vers moi si tu as des questions.

[RETOUR](/README.md)