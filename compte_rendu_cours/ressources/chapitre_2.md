Outillage Formel

        LOS
      Chapitre 2
Détails du Chapitre 2

     Introduction



   Langages des données


     Langage pour la dynamique
 Introduction

 Un programme est muni de 2 concepts
    Syntaxe : séquence de mots du langage de programmation
    Sémantique : relative au sens du programme, ce que le programme fait ou l’action
     qu’il réalise (a trait au comportement)
    Exemple :
          Syntaxe : z:= x; x:= y; y:=z : formé de 3 instructions séparées par des ;
          Sémantique : échanger des variables x et y en utilisant une variable intermédiaire

    Pourquoi la sémantique?
          Afin de permettre de cerner très précisément ce que réalise le programme
          Afin de réaliser des traducteurs (compilateurs) et des optimiseurs
          Afin de pouvoir appliquer des méthodes formelles de vérification

    Ce qui garantit la production de logiciels sûrs
          Transports, Télécommunications, Transactions commerciales, ….
Introduction
 La sémantique peut être vue comme une fonction :



 Dans toute la suite, on distinguera :
     Les données et structures de données manipulées par le programme (entiers, …)
           Représentent le vecteur d’état d’un programme, le contexte, l’environnement
            d’exécution ou l’état de mémoire, …..
           Permettent donc de décrire les états du système
           La formalisation du contexte nécessite l’introduction d’outils formels.

     Les différentes opérations permettant de calculer le résultat d’un programme
                                          Programme
                     Entrées                                         Résultat
                                          (Opérations)
Introduction

 Dans toute la suite, on distinguera :
     Les données et structures de données manipulées par le programme (entiers, …)
     Les différentes opérations permettant de calculer le résultat d’un programme

                                 Programme
                Entrées                               Résultat
                                 (Opérations)
Langage des Données
Langage des données



 Ensembles
   Notations :
        A, B, C, … des ensembles
        a, b, c, … des éléments d’ensembles
        Ensemble vide : ø,      Ensemble singleton : {a}
        Opérations ensemblistes : voir Tableau 1 ci-dessous
Langage des données


Opérateur      Syntaxe    Condition            Définition

   Union        𝐴∪𝐵      𝐴 ⊆𝑆 ∧𝐵 ⊆𝑆   {𝑎 | 𝑎 ∈ 𝑆 ∧ (𝑎 ∈ 𝐴 ∨ 𝑎 ∈ 𝐵) }

Intersection    𝐴∩𝐵      𝐴 ⊆𝑆 ∧𝐵 ⊆𝑆   {𝑎 | 𝑎 ∈ 𝑆 ∧ (𝑎 ∈ 𝐴 ∧ 𝑎 ∈ 𝐵) }

Différence      𝐴−𝐵      𝐴 ⊆𝑆 ∧𝐵 ⊆𝑆   {𝑎 | 𝑎 ∈ 𝑆 ∧ (𝑎 ∈ 𝐴 ∧ 𝑎 ∉ 𝐵) }

Ensemble
                ℙ(𝐴)                      Puissance de A (2 𝐴 )
des parties

Ensemble
des parties     ℙ1 (𝐴)                         ℙ(𝐴) − {∅}
non vides

Ensemble
des parties     𝔽(𝐴)
  finies

Ensembles
des parties
                𝔽1 (𝐴)                         𝔽(𝐴) − {∅}
finies non
    vide
Langage des données
 Ensembles
    Exemple :
           𝐴 = 1, 2, 4     et   𝐵 = 2, 4, 6 , 8
           𝐴 − 𝐵 = {1}
           ℙ(𝐴) = {∅, {1}, {2}, {4}, {1,2}, {1,4}, {2,4}, {1,2,4}}
    Représentation : 2 manières
           En extension : 𝐴 = 1, 2, 4
           En compréhension : 𝐴 = 𝑎 ∈ 𝑆 | 𝑃 𝑎            où P(a) désigne un prédicat ou une propriété.
    Paire ordonnée :               qui signifie la paire             , notée aussi <x, y>
     Produit cartésien : 𝐴 × 𝐵 =     𝑎 ⟼𝑏|𝑎 ∈𝐴 ∧ 𝑏 ∈𝐵


 .Abstraction / .Notation
                  x.(x  s | E) = {x, y | x, y  s  t  y = E}
                  x.(x  s  P| E) = {x, y | x, y  s  t  P  y = E}
        Exemple :             x.(x  0  3 | 3 - x ) = { 0  3, 1  2, 2  1, 3  0 }
Langage des données
 Relations
    Une relation de A vers B est un sous ensemble du produit cartésien A x B. Les
     éléments de cette relation sont notés                   où          et      ,
          b est l’image de a , a est l’image réciproque (antécédent) de b
          𝐴 = 1, 2, 4     et   𝐵 = 2, 4, 6 , 8
          𝐴 − 𝐵 = {1}
          ℙ(𝐴) = {∅, {1}, {2}, {4}, {1,2}, {1,4}, {2,4}, {1,2,4}}


    L’ensemble de toutes les relations entre A et B, noté                      , est tel que :

                                        A    1
                                                       r      4
                                                                     B
                                             2                7

                                             3                8

                                             5



         𝒓 ∈ 𝑨 ⟷ 𝑩 = {𝟏 ⟼ 𝟒,          𝟏 ⟼ 𝟖,        𝟐 ⟼ 𝟖,        𝟑 ⟼ 𝟒,      𝟑 ⟼ 𝟕}
Langage des données
 Relations
    Une relation R est :
           Réflexive sur A si ∀𝑎, 𝑎𝑅𝑎
           Symétrique si ∀ 𝑎, 𝑏 ∈ 𝐴, 𝑎𝑅𝑏 ⟹ 𝑏𝑅𝑎
           Anti symétrique si ∀ 𝑎, 𝑏 ∈ 𝐴, 𝑎𝑅𝑏 ∧ 𝑏𝑅𝑎 ⟹ 𝑎 = 𝑏
           Transitive ∀ 𝑎, 𝑏, 𝑐 ∈ 𝐴, 𝑎𝑅𝑏 ∧ 𝑏𝑅𝑐 ⟹ 𝑎𝑅𝑐
                 (1) + (2) + (4) : R est une relation d’équivalence
                 (1) + (3) + (4) : R est une relation d’ordre
    Ordre Total : ∀   𝑎, 𝑏 ∈ 𝐴, 𝑎 𝑅 𝑏 𝑜𝑢 𝑏 𝑅 𝑎        sinon : ordre partiel
    Relation inverse 𝑟     : 𝑟    = 𝑎 ⟼𝑏|𝑏 ⟼𝑎 ∈𝑟
    Domaine de r : 𝑟 ∈ 𝐴 ⟷ 𝐵        𝑑𝑜𝑚 𝑟 = 𝑎 | 𝑎 ∈ 𝐴 ∧ ∃𝑏 . (𝑏 ∈ 𝐵 ∧ 𝑎 ⟼ 𝑏 ∈ 𝑟
    Codomaine (range) de r :      𝑟𝑎𝑛 𝑟 = 𝑏 | 𝑏 ∈ 𝐵 ∧ ∃𝑎 . (𝑎 ∈ 𝐴 ∧ 𝑎 ⟼ 𝑏 ∈ 𝑟
    Composition des relations :
           𝑟∈𝐴⟷𝐵 ∧ 𝑞∈𝐵⟷𝐶
         𝑟 ; 𝑞 = 𝑞 𝐨 𝑟 = {𝑎, 𝑐 |𝑎 ⟼ 𝑐 ∈ 𝐴 × 𝐶 ∧ ∃𝑏 . ( 𝑏 ∈ 𝐵 ∧ 𝑎 ⟼ 𝑏 ∈ 𝑟 ∧ 𝑏 ⟼ 𝑐 ∈ 𝑞}
    Identité : 𝐼𝑑   𝐴 = 𝑎, 𝑏 | 𝑎 ⟼ 𝑏 ∈ 𝐴 × 𝐴 ∧ 𝑎 = 𝑏
Langage des données
 Relations
    Opérations avancées :
           Restriction sur le domaine :
                        𝑟 ∈ 𝐴 ⟷ 𝐵 et 𝐸 ⊆ 𝐴, 𝐸 ⊲ 𝑟 = 𝑎, 𝑏 | 𝑎 ⟼ 𝑏 ∈ 𝑟 ∧ 𝑎 ∈ 𝐸
           Restriction sur le co-domaine :
                        𝑟 ∈ 𝐴 ⟷ 𝐵 et F ⊆ 𝐵, 𝑟 ⊳ 𝐹 = 𝑎, 𝑏 | 𝑎 ⟼ 𝑏 ∈ 𝑟 ∧ 𝑏 ∈ 𝐹


    Exemple :




 Voir l’Annexe jointe au Poly pour plus de détails sur l’ensemble des opérations utilisées
                                      dans ce cours.
Langage des données
 Fonctions
   Une fonction f de A vers B est une relation pour laquelle chaque élément du
     domaine possède au plus une image, c'est-à-dire :

                    𝟏   𝟐               𝟏      𝟐            𝟏         𝟐

   Type de fonction :
         Fonction partielle :
                  𝐴 ↛ 𝐵 = 𝑓 | 𝑓 ∈ 𝐴 ⟷ 𝐵 ∧ ∀𝑎, 𝑏, 𝑐 . ((𝑎, 𝑏) ∈ 𝑓 ∧ (𝑎, 𝑐) ∈ 𝑓 ⟹ 𝑏 = 𝑐)

       Fonction Totale : fonction partielle où tous les éléments de A possèdent une image dans
      B

       Injective :  𝐴 ↣𝐵 =𝑓|𝑓 ∈𝐴 ↛𝐵 ∧𝑓             ∈ 𝐵 ↛ 𝐴 : Chaque élément de B possède au
      plus un antécédent dans A.
       Injective totale :   𝐴↣𝐵=𝐴↣𝐵          𝐴 → 𝐵 : tous les élément de A sont impliqués dans la
      fonction
       Surjective, bijective, ….. : voir Annexe.
Langage des données


 Opérations
   Une opération * sur l’ensemble A est une application (fonction totale) de A x A dans A.
   Une opération * peut être
         Commutative : a * b = b * a
         Associative : (a * b) * c = a * (b * c)
         Admet un élément neutre à droite si a, a * e = a et à gauche si a, e * a = a
         Admet un élément absorbant à droite si a, a * x = x et à gauche si x, x * a = x
         Un élément a pour inverse à droite si a, a * a’ = e et à gauche si a, a’ * a = e
         Un élément a est idempotent si a, a * a =a
         Une opération * est idempotente si tout élément de A est idempotent par cette opération
Langage des données
 Morphismes
   Soit les ensembles :
          E munit d’une fonction f, d’une opération * et d’une relation R
          E’ munit d’une fonction f’, d’une opération *’ et d’une relation R’
   Le quadruplet noté <E, f, *, R> (resp. <E', f', *', R'>) est une structure.
   Un morphisme de <E, f, *, R> vers <E’, f’, *’, R’> est une fonction de E vers E’ telle
     que si

   Alors on a :
          Préservation de la fonction : si y = f(x) alors y’ = f’(x’), i.e., (y) = f'((x))
          Préservation de l’opération : si z = x * y alors z’ = x’ *’ y’, i.e., (z) = (x) *' (y)
        Préservation de la relation : si x R y alors x’ R’ y’, i.e., (x) R' (y)
   Un isomorphisme est un morphisme bijectif.
   Deux structures sont isomorphes si elles sont reliées par un isomorphisme.

        Cette notion est utilisée pour transposer une représentation (par exemple, un
     programme) dans une autre représentation sur laquelle il est possible de raisonner
Langage des données
 Logique des propositions
    P et Q deux propositions logiques. Le tableau suivant résume les différents connecteurs
      logiques :


                     Symbole                                Nom

                                                            Non

                                                              Et

                                                             Ou

                                                           Implique

                                                           Equivaut

                                                         Quelque soit

                                                           Il existe
Langage des données


 Logique des propositions
    La formule                  signifie que tout x vérifiant P vérifie aussi Q. Si aucun
     x ne vérifie P alors                est vraie.
    De nombreuses propriétés logiques peuvent s’écrire sous forme d’équivalence
     logique :


                                    

                                           , 
Langage pour la Dynamique
Langage pour la dynamique
 C’est   un langage de spécification et de description des opérations :
   Substitutions Généralisées (SG). Ces substitutions sont issues de la théorie
   des transformateurs des prédicats.
 Le langage SG est généralement utilisé pour décrire les changements d’états.
   En effet, une substitution est un moyen de représenter une transition.

Logiciel (ou machine) :




Etat : est représenté par une combinaison particulière des valeurs de ses variables.
Langage pour la dynamique

 Substitutions SG
    Ne    sont pas nécessairement déterministes : une SG spécifie un ensemble de
      transitions potentielles.
    Lors de l’implantation, une seule transition sera effectivement réalisée (peu importe
      laquelle)
    L’indéterminisme est appréciable quand il s’agit de spécifier ou de raffiner

 On distingue un ensemble de substitutions primitives à partir des quelles
   d’autres constructeurs sont définis.

 Dans une notation mathématique, les substitutions primitives se résument
   comme suit (avec e, f : expression; p : prédicat; S,T : substitutions) :
Langage pour la dynamique
                                Notation                                    Nom

                                                                     Substitution simple

                                                                Substitution multiple simple

                                  Skip (*)                         Substitution sans effet

                                   P|S                         Substitution pré conditionnée

                                                                    Substitution gardée

                                  ST                             Substitution choix borné

                                  @z.S                         Substitution choix non bornée

                                   S ;T                                Séquencement

                 While P do S Invariant I variant e end(#)          Substitution itération

(*) : aboutit à un état Post identique à l’état Pré
(#) : Invariant I : un prédicat : propriété toujours vérifiée par l’ensemble des variables décrivant le système.

                   Variant e : une expression
Langage pour la dynamique

 Typologie des SG
    P|S  : permet de donner des contraintes sur les entrées (variables d’état et
     paramètres). L’opération ne peut être invoquée que dans sa précondition. (en
     dehors de P, le logiciel ou système est non prédictible)
                                                              𝒙 𝟏
                Exemple : PRE :
                                                               𝟐

              : permet de donner des hypothèses sous lesquelles la substitution S sera
     utilisée (si P n’est pas vérifié, la substitution n’est pas exécutée, elle est prohibée
     dans les implémentations)
                Exemple :
    S  T : permet de décrire des spécifications non déterministes : x := 1  x := 2
     décrit l’affectation d’une des valeurs (1 ou 2) à la variable x. Le programmeur est
     libre d’implanter l’une ou l’autre substitution ou encore selon le contexte.
Langage pour la dynamique

 Typologie des SG
    @z.S : étend le non déterminisme
       Exemple : @z.(z < x  x := z) a pour effet d’affecter à la variable x une valeur
                                     strictement supérieure à la précédente.
    Substitution iteration:
                WHILE P do S INVARIANT I VARIANT e END
    Correspond à une exécution itérative de S tant que le prédicat P est satisfait.

    - Le variant e :
                (i) une variable entière qui se trouve initialisée à la première exécution ;
                (ii) décroit ensuite strictement à chaque itération de la boucle ;
                (iii) garantit la terminaison de la boucle et interdit par conséquent les
                      boucles infinies.
 Langage pour la dynamique

 Notations syntaxique des SG
                       Syntaxe                                Définition
                 (pseudo programme)
                     BEGIN S END
                                                                   S
                        (Bloc)
                  PRE P THEN S END
                                                                  P|S
                   (Pré-conditionnée)
               IF P THEN S ELSE T END                     𝑃 ⟹ 𝑆  (𝑃  𝑇)
                   IF P THEN S END                    IF P THEN S ELSE Skip END
                    𝒙≔𝑬∥𝒚≔𝑭
          (symbole de parallélisme, substitution              x, y := E, F
                       multiple)
              Choice S OR …. OR T END                         S  ….  T
            ANY x WHERE P THEN S END                         @x.(P  S)
                         𝒙: ∈ 𝑼
                                                   ANY y WHERE y ∈ U THEN x:=y END
               (choix dans un ensemble)
                        Let x BE                            ANY x WHERE
                          x=E                                    x=E
                           IN                                   THEN
                            S                                     S
                          END                                    END
 Langage pour la dynamique


 Sémantique des SG
   La   notation [x := e] R (avec e une expression et R un prédicat) : traduit la
     substitution uniforme de x par e dans R (sachant que x est une variable libre dans R


   Remarque : x est une variable non libre (ou liée) dans un prédicat P :
      Si elle n’est pas présente dans P,
      ou
      Elle est seulement présente dans la portée de certains quantificateurs.

      Dans l’expression                      : x est libre, n et y sont liés
 Langage pour la dynamique
 Sémantique des SG

         Cas de substitution         Réduction                       Condition

            [x, y := e, f] R   [z := f][x := e][y := z] R   z | e, f, R (z n’est pas libre
                                                                      dans e,f ,R)

               [Skip] R                    R

               [P|S] R

              [S  T] R

              [P  S]R                P  [S] R

              [@z.S] R                                                   Z\R

               [S ; T] R             [S] ( [T] R )
Langage pour la dynamique
 Sémantique des SG : Exemples
    Substitution multiple
                [x, y := y, x] (x < y)
                [z := x][x := y][y := z] (x < y)
                [z := x][x := y] (x < z)
                [z := x] (y < z)
                 (y < x)
    Substitution pré-conditionnée :
                  [x > 0 | x := x-1] (-1  x  1)
                   (x > 0)  [x := x-1] (-1  x  1)
                   (x > 0)  (-1  x-1  1)
                   (x > 0)  (0  x  2)
                   (0 < x  2)
    Substitution choix non borné : [@z . (z > 0  x := x+z)] (x > 3)
                z . (z > 0  [x := x+z] (x > 3)
                z . (z > 0  x+z > 3)
Langage pour la dynamique
 Sémantique des SG : Cas de la boucle
     [WHILE P DO S INVARIANT I VARIANT V END] R
      Équivaut :
      I                                    -- l’invariant est vrai avant la boucle
                                           -- l’invariant est conservé dans la boucle
                                           -- le variant est un entier naturel
                                           -- le variant décroit à chaque pas
                                           -- la sortie de la boucle implique R



Remarque : Une des difficultés de programmer avec les boucles est d’exhiber l’invariant
et de justifier sa terminaison.
Langage pour la dynamique
 Syntaxe des opérations


               Paramètres de sortie     nom opérations (paramètres d’entrées) =
                         G
                ;


    Les paramètres entrées/sorties sont optionnels
    Le passage de paramètre se fait par valeur
    Dans une opération, la substitution G est en général une substitution pré-
     conditionnée
Langage pour la dynamique
 Syntaxe des opérations
    Exemple 1 : division euclidienne
         /*qq et rr correspondent au quotient et au reste */
         /*aa et bb qui correspondent au dividende et au diviseur */


    MACHINE
       DIVISION
    OPERATIONS
    qq , rr divi(aa,bb) =
    PRE

    THEN
      ANY ss, tt WHERE

    THEN
      qq, rr := ss, tt
    END
    END;
 Langage pour la dynamique



 Syntaxe des opérations
    Exemple 2 : Un ascenseur qui a une porte à chaque étage et on ne distingue pas
     les appels intérieurs de ceux extérieurs ; pas de pannes.
    Modélisation des ensembles et de l’état :
Langage pour la dynamique
 SETS
 MODE = {stop, moving}
                      -- état de l’ascenseur
 CONSTANTS
 max_floors, FLOORS
 PROPERTIES
 max_floors    NAT1     FLOORS = 0..max_floors    -- ensemble d’étages
 VARIABLES
 openf , callf , pos, mode
 INVARIANT
 openf    FLOORS                -- ensemble portes ouvertes
 callf   FLOORS                 -- ensemble d’appels faits
 pos     FLOORS                 -- position courante
 mode     MODE                  -- mode courant
