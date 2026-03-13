# Cours : Logiciels Sûrs et Méthodes Formelles

Ce cours porte sur la conception de logiciels dont on peut garantir mathématiquement le bon fonctionnement, particulièrement pour les systèmes critiques (ferroviaire, aéronautique, médical).

## 1. Correction des Programmes : De la Simulation à la Preuve Formelle

Le passage d'un programme vers un logiciel "sûr" suit une hiérarchie de vérification :

*   **Simulation / Tests** : On exécute le programme avec un ensemble de données d'entrée et on vérifie si la sortie est correcte. 
    *   *Limite* : Le test peut montrer la présence de bugs, mais jamais leur absence totale (Dijkstra). On ne peut pas tester toutes les combinaisons possibles.
*   **Vérification Formelle** : On utilise des méthodes mathématiques pour prouver que le programme respecte sa spécification pour *toutes* les entrées possibles.
    *   *Approche* : On ne "teste" plus, on "démontre".

## 2. Outils Formelles et Modélisation

Pour prouver un logiciel, il faut des outils capables de manipuler des concepts mathématiques :

*   **Modélisation des Données** : En méthode B, on utilise la **théorie des ensembles** (ensembles, relations, fonctions) et la **logique des prédicats** pour décrire l'état du système et ses invariants (ce qui doit toujours être vrai).
*   **Substitution Générale** : C'est le concept central du langage B pour décrire les opérations. 
    *   Une substitution est un "transformateur de prédicat". 
    *   Au lieu de voir une instruction comme un changement de valeur en mémoire, on la voit comme une transformation mathématique qui garantit le passage d'un état valide à un autre état valide.
    *   Elle permet de gérer le non-déterminisme et l'abstraction.

## 3. La Méthode B : Fondements

La méthode B n'est pas seulement un langage, c'est une approche globale de l'ingénierie logicielle. Elle se définit par trois piliers :
*   **Une Méthode Formelle** : Basée sur des preuves mathématiques plutôt que sur des tests.
*   **Un Langage de Spécification** : Le langage B (ou notation B), qui permet d'écrire des modèles mathématiques précis.
*   **Une Méthode de Développement** : Basée sur le raffinement successif.

Ses fondements mathématiques reposent sur :
*   **La Théorie des Ensembles** : Pour modéliser les types de données et les relations.
*   **La Logique du Premier Ordre** : Pour exprimer les propriétés (prédicats).
*   **La Substitution Générale** : Pour modéliser les changements d'état.

## 4. La Machine Abstraite (MA) : Description Complète

La Machine Abstraite est l'unité de base de la méthode B. Elle agit comme un contrat formel : elle garantit des services (opérations) tout en protégeant l'intégrité des données (invariant).

### Constituants et Clauses d'une MA

Une machine respecte une structure stricte. Voici l'ordre et le rôle de chaque clause :

1.  **MACHINE** : Identifiant unique du module.
2.  **CONSTRAINTS** : Contraintes sur les paramètres de la machine (si elle est paramétrée).
3.  **SETS** : Définit les types de données.
    *   *Énumérés* : `COULEURS = {rouge, vert, bleu}`.
    *   *Différés* : `PILES` (le détail est reporté au raffinement).
4.  **CONSTANTS** : Valeurs fixes (paramètres de configuration).
5.  **PROPERTIES** : Prédicats définissant les constantes (ex: `vitesse_max : NAT1`).
6.  **VARIABLES** : L'état interne du système (ex: `vitesse`, `position`).
7.  **INVARIANT** : 
    *   **Typage** : `vitesse : 0..vitesse_max`.
    *   **Sécurité** : `vitesse > 0 => signal = vert`.
    *   *Note* : L'invariant est une conjonction ($\land$) de tous les prédicats.
    *   Il restreint l'espace d'état aux seuls comportements autorisés.
8.  **ASSERTIONS** : Propriétés déduites de l'invariant (aide à la preuve).
9.  **INITIALISATION** : Établit l'état initial. Utilise une substitution (ex: `vitesse := 0`).
    *   **Règle d'or** : L'invariant doit être établi par l'initialisation et préservé par chaque opération.
10. **OPERATIONS** : Services exportés.

### Anatomie d'une Opération

Une opération définit une transition d'état. Elle se compose de trois parties :

1.  **L'Interface (Signature)** :
    *   `res <-- NomOperation(param)` : définit le nom, les paramètres d'entrée et les valeurs de retour.
2.  **La Précondition (PRE)** :
    *   C'est une condition sur les paramètres et l'état actuel.
    *   **Rôle** : Elle définit le domaine de validité de l'opération. C'est à l'appelant de garantir que la précondition est remplie.
    *   Syntaxe : `PRE P THEN ... END`.
3.  **Le Corps (Body / Substitution)** :
    *   C'est l'action réalisée par l'opération.
    *   En B, on utilise des **substitutions** pour décrire comment l'état change.
    *   *Déterministe* : `x := E` (devenir égal).
    *   *Non-déterministe* : `x :: S` (devenir un élément de S).
    *   Le corps est exécuté *uniquement* si la précondition est satisfaite.

### Exemple Récapitulatif : Un Compteur Borné

```b
MACHINE Compteur(max_val)
CONSTRAINTS max_val : NAT1
VARIABLES val
INVARIANT val : 0..max_val
INITIALISATION val := 0
OPERATIONS
  Incrementer = 
    PRE val < max_val THEN 
      val := val + 1 
    END;
  
  v <-- LireValeur = 
    BEGIN v := val END
END
```

### Exemple : Système de Réservation de Places

Cet exemple illustre la manipulation d'ensembles et le typage par sous-ensemble.

```b
MACHINE Reservation
SETS 
  SIEGES // Ensemble différé des sièges possibles
VARIABLES 
  reserves
INVARIANT 
  reserves <: SIEGES // 'reserves' est un sous-ensemble de 'SIEGES'
INITIALISATION 
  reserves := {}    // Au départ, aucune place n'est réservée
OPERATIONS
  Reserver(s) =
    PRE s : SIEGES \ reserves THEN
      reserves := reserves \/ {s}
    END;

  Annuler(s) =
    PRE s : reserves THEN
      reserves := reserves - {s}
    END;

  dispo <-- EstDisponible(s) =
    PRE s : SIEGES THEN
      IF s : reserves THEN dispo := FALSE ELSE dispo := TRUE END
    END
END
```

## 5. Les Obligations de Preuve (OP) : Le Coeur de la Vérification

Les OP sont des lemmes mathématiques générés automatiquement par l'Atelier B. Si toutes sont prouvées, le système est mathématiquement correct vis-à-vis de son invariant.

### Les 3 types principaux d'OP

#### 1. Établissement de l'Invariant (Initialisation)
L'initialisation doit garantir que l'état de départ du système respecte l'invariant.
*   **Formule** : `[Initialisation] Invariant`
*   *Signification* : Après l'exécution de l'initialisation, le prédicat de l'invariant doit être vrai.

#### 2. Préservation de l'Invariant (Opérations)
Chaque opération doit garantir que, si elle est appelée dans de bonnes conditions, elle ne "casse" pas l'invariant.
*   **Formule** : `Invariant ∧ Précondition => [Corps_Opération] Invariant`
*   *Signification* : Si l'invariant est vrai au départ ET que la précondition est respectée, alors après l'exécution du corps de l'opération, l'invariant doit rester vrai.

#### 3. Preuve de Raffinement (Simulation)
On doit prouver que le raffinement (le modèle concret) se comporte exactement comme la spécification (le modèle abstrait).
*   On utilise un **Invariant de Liaison** qui fait le pont entre les variables abstraites et concrètes.
*   On prouve que chaque opération concrète "simule" son opération abstraite correspondante.

### Statistiques de Preuve
Dans un projet industriel B (ex: Météor) :
*   **~90% des OP** sont prouvées automatiquement par les prouveurs de l'outil.
*   **~10% des OP** restantes (les plus complexes) nécessitent une **preuve manuelle assistée** par un ingénieur (utilisation de règles mathématiques, tactiques de preuve).

## 6. Limites et Concurrence : Le Cas des Threads

Votre intuition sur le problème `x != y` est fondamentale. La méthode B classique repose sur des hypothèses strictes :

*   **Hypothèse Monotâche** : Le modèle suppose une exécution **séquentielle**. Une opération B est **atomique** (indivisible).
*   **Le problème de la concurrence** : Si l'implémentation utilise des threads (concurrence réelle), une autre tâche peut modifier `x` ou `y` *pendant* l'exécution d'une opération, invalidant la précondition ou l'invariant.
    *   *Exemple* : Un thread teste `x != y` (Vrai), est interrompu, un autre thread modifie `y`, le premier reprend et exécute une action désormais invalide.
*   **La Solution** :
    *   **Architecture** : Le code appelant (le "main" ou l'OS) doit garantir l'exclusion mutuelle (ex: **Mutex**) autour des appels aux opérations B.
    *   **Modélisation** : Pour des systèmes distribués intrinsèques, on utilise une variante appelée **Event-B**, conçue pour gérer des événements concurrents et asynchrones.

## 7. Raffinement et Implémentation

Le raffinement est le processus itératif qui permet de combler le fossé entre une spécification mathématique et un programme exécutable.

### A. Le Principe du Raffinement
Un composant **R** (Raffinement) raffine un composant **A** (Abstrait) s'il respecte strictement le contrat de **A** tout en étant plus précis.
*   **Réduction du non-déterminisme** : On remplace des choix abstraits (`ANY x WHERE...`) par des calculs déterministes.
*   **Raffinement de données** : On remplace des structures mathématiques (ensembles, fonctions, relations) par des structures informatiques (tableaux, entiers, booléens).

### B. L'Invariant de Liaison (Gluing Invariant)
C'est le pont mathématique entre l'abstraction et le concret. Il est déclaré dans la clause `INVARIANT` du raffinement.
*   Il lie les variables abstraites ($v_a$) aux variables concrètes ($v_c$).
*   *Exemple* : Si l'abstrait utilise un ensemble `reserves` et le raffinement un tableau de booléens `table`, l'invariant de liaison sera : `∀i . (table(i) = TRUE ⇔ i ∈ reserves)`.

### C. L'Implémentation (B0)
Le dernier niveau de raffinement est appelé l'**Implémentation**. Pour être traduisible en code, elle doit être écrite dans un sous-ensemble strict du langage B appelé **B0**.
*   **Déterminisme total** : Aucune ambiguïté n'est autorisée.
*   **Structures de contrôle** : Utilisation de boucles (`WHILE`), de conditions (`IF`, `CASE`) et d'instructions séquentielles (`;`).
*   **Types machine** : Utilisation d'entiers bornés (ex: `0..65535`) et de tableaux de taille fixe.

### D. Vers le Code Exécutable
L'étape finale est la **génération automatique de code**.
*   L'outil (Atelier B) traduit l'implémentation B0 en langage **C** ou **Ada**.
*   **Garantie** : Si les OP de raffinement ont été prouvées, le code généré est garanti conforme à la spécification abstraite initiale. On élimine ainsi toute une classe d'erreurs d'implémentation.
