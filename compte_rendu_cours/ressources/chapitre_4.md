Vérification Formelle
     de Logiciels
          LOS
        Chapitre 4
Détails du Chapitre 4


     Introduction

    Sémantique Opérationnelle

     Sémantique Axiomatique
 Introduction

 Par  vérification formelle d’un logiciel, on entend la vérification mathématique «
   exhaustive » de sa correction.
      On cherche à prouver au sens mathématique que l’implantation (vue comme un
       modèle logique) satisfait à sa spécification (vue par exemple comme un ensemble de
       formules logiques).


 Notons que la vérification du logiciel peut être traitée sous les angles suivants :
     Test : techniques et environnement de test pour le logiciel (voir chapitre 5)
     Preuve : prouver qu’un logiciel satisfait à ses spécifications par la           preuve de
       programme (objet de ce chapitre)
     Model checking : modéliser le logiciel par des techniques à base d’automate et vérifier
       automatiquement des propriétés exprimées en logique temporelle (voir chapitre 6)
 Introduction


 La vérification formelle est une activité complexe. Il faudrait d’abord
  procéder à l’extraction d’un modèle depuis un programme ou de
  formules logiques depuis des spécifications (souvent semi-
  formelles).

 La sémantique permet de répondre à ces questions et préparer le
  terrain pour la preuve des programmes et pour la correction des
  propriétés des logiciels.
  Introduction

 La sémantique concerne l’aspect sens et signification à attribuer aux
   programmes :
    Ce qu’ils calculent
    Comment ils le calculent
    Les objets mathématiques qu’ils représentent

 La sémantique permet, notamment, de :
    Décider ce que doit faire un programme dans des cas complexes
    Calculer si des programmes sont équivalents, ce qui permet à    un compilateur de
      remplacer l’un par l’autre.
    Dériver la plupart des analyses de programmes
Introduction


La  sémantique formelle (SF) concerne l’aspect dynamique
 (exécution) et elle comprend 3 approches :
  Sémantique opérationnelle (SO)
  Sémantique dénotationnelle (SD)
  Sémantique axiomatique (SA)
Introduction


 Sémantique Opérationnelle (SO) : Vision impérative
   décrit    le comportement exact de la machine lors de l’exécution du
     programme ;

   décrit l’évolution des états de la machine en cours d’exécution, ainsi que les
     transitions entre elles.

   Cette sémantique est orientée développeur de compilateur, ou interpréteur.


  Remarque : Adaptée à la vérification formelle de propriétés sémantiques
Introduction

 Sémantique Dénotationnelle (SD) : vision fonctionnelle
   le   programme est représenté par une fonction ; traduction des expressions
     du langage en un ensemble de dénotations sous forme de constantes ou de
     fonctions mathématiques.

   Elle   s’intéresse à l’effet du programme et non à la manière avec laquelle il
     est exécuté.

   Elle est orientée concepteur de langages de programmation.
  Remarque : Permet de définir des sémantiques plus abstraites
 Introduction


 Sémantique Axiomatique (SA) : vision déclarative

   elle   permet de prouver des propriétés des programmes sous forme
     d’assertions logiques.

    orientée programmeur pour vérifier la correction du programme.
Sémantique Opérationnelle
Sémantique Opérationnelle

 Domaines et fonctions sémantiques :
    Pour illustrer les diverses formes sémantiques, on considère un mini-langage
    impératif simple :
    Catégories syntaxiques
          NUM : l’ensemble des numéraux
          VAR : l’ensemble des variables (de noms)
          AEXP : l’ensemble des expressions arithmétiques
          BEXP : l’ensemble des expressions booléennes
          STM : l’ensemble des assertions (statements) (ensemble des commandes du langage)

    Méta – variables
          𝑛 ∈ 𝑁𝑈𝑀 , 𝑥 ∈ 𝑉𝐴𝑅      x : variable du programme, emplacement mémoire.
          𝑎 ∈ 𝐴𝐸𝑋𝑃, 𝑏 ∈ 𝐵𝐸𝑋𝑃, 𝑠 ∈ 𝑆𝑇𝑀
Sémantique Opérationnelle

 Domaines et fonctions sémantiques :
    Pour illustrer les diverses formes sémantiques, on considère un mini-langage
    impératif simple :
    Syntaxe abstraite
         Définir les catégories syntaxiques :
                          (les numéraux sont définis dans le système binaire)




         Exemple :
Sémantique Opérationnelle
 Sémantique des numéraux
   Domaine sémantique : l’ensemble des entiers
   Fonction sémantique :
      Exemple :
                          ,
   Définition inductive de   :
                                  ,
                                           ,
      Exemple :

                                      =2       (2   =2   (2 1) + 1 = 5
Sémantique Opérationnelle
 Sémantique des expressions arithmétiques
  L’interprétation des expressions arithmétiques dépend des valeurs associées aux
  variables présentent dans les expressions.

  Un état est l’association d’une valeur (du bon type) à chaque variable. Si les
  variables sont toutes de type entier, un état s est une fonction définie par :

                                         (STATE = VAR         )

  Pour chaque variable x de VAR, l’état S spécifie une valeur pour x, notée Sx (ou
  S(x))
  Par exemple, si Sx = 3 alors la valeur de x+1 dans S est 4

  Remarque :
  Autre notation :                           : on veut spécifier que l'état est juste
  concerné par les variables x, y et z. Les autres variables sont indifférentes.
Sémantique Opérationnelle
 Sémantique des expressions arithmétiques
  Fonction sémantique : interprète les expressions arithmétiques

  Elle est de la forme

  Avec




                                                                   (Idem pour – et *)




  Exemple :
Sémantique Opérationnelle
 Sémantique des expressions booléennes
La fonction sémantique est définie comme suit :


Avec




Exemple :
Si Sx=3
Sémantique Opérationnelle
 Sémantique des expressions booléennes
La fonction sémantique est définie comme suit :


Avec




Exemple :
Si Sx=3
Sémantique Opérationnelle
 Règles d’évaluation des expressions
  On note par :            l’évaluation de l’expression arithmétique a dans l’état S.
                  : exprime le fait que l’expression a s’évalue en n, dans l’état S.


  Règles : (prémisse au numérateur, conclusion au dénominateur)

           𝒏 ,𝑺 ⟶𝒏


           𝒙 ,𝑺 ⟶𝑺𝒙

           𝒂𝟏 ,𝑺 ⟶𝒏𝟏 𝒂𝟐 ,𝑺 ⟶𝒏𝟐
              𝒂𝟏 𝒂𝟐 ,𝑺 ⟶𝒏𝟏 𝒏𝟐

           𝒂𝟏 ,𝑺 ⟶𝒏𝟏 𝒂𝟐 ,𝑺 ⟶𝒏𝟐
               𝒂𝟏∗𝒂𝟐 ,𝑺 ⟶𝒏𝟏∗𝒏𝟐

           𝒂𝟏 ,𝑺 ⟶𝒏𝟏 𝒂𝟐 ,𝑺 ⟶𝒏𝟐
              𝒂𝟏 𝒂𝟐 ,𝑺 ⟶𝒏𝟏 𝒏𝟐
Sémantique Opérationnelle
 Règles d’évaluation des expressions
    Exemple :
    Supposons que Sx = 2
    Prouver que
    But : construire un arbre de dérivation en utilisant le système d’inférence (A1)-(A5) où
    l’expression cible est la racine.




<(2 * 3) + x, s>  8 est un théorème pour la sémantique donnée.
<3+2, s>  1 n'est pas un théorème, il s'agit d'un jugement syntaxiquement correct mais sémantiquement
erroné.
Sémantique Opérationnelle


 Règles d’évaluation des expressions

     Proposition 1 :

              a1, a2 : deux expressions arithmétiques
Sémantique Opérationnelle


 Evaluation des commandes

  Effet d’une expression : ne change pas l’état courant de la mémoire, elle
  l’inspecte.
  (état avant)                                          (état après) === Même état
  Effet d’une instruction (cmd) : réalise des affectations, les valeurs des variables
  en mémoire sont modifiées.
  (état avant)                                               (état après) ==== Etat
  différent
Sémantique Opérationnelle

 Evaluation des commandes

Le rôle d’un programme (ou cmd) est de modifier l’état courant S1 de la mémoire en
un état S2 :

          est appelée configuration

                 : transition (qui exécute la cmd c à partir de l'état S1, cette cmd se
termine, et à la terminaison on se trouve dans l'état S2)
Le changement d’état, suite à une exécution de cmd, est noté :




Exprime l’état obtenu à partir de S en remplaçant x par m.
On peut écrire maintenant
Sémantique Opérationnelle

 Evaluation des commandes

Les règles de transition :

                                                          (Instruction vide)
                    ,       ⟶

                        ,    ⟶
                                                          (Affectation)
                ≔ ,         ⟶ [ ⟵ ]

                ,       ⟶            ,       ⟶
                                                          (Séquencement)
                         ;       ,   ⟶

                             ,       ⟶
                                         ,   ⟶




                                                 (C4 à C5 représentent l’alternative)
Sémantique Opérationnelle

 Evaluation des commandes

Les règles de transition :


                             ,   ⟶




                                 (C6 à C7 représentent la boucle)
Sémantique Opérationnelle

 Evaluation des commandes

Exemple :
Soit la cmd qui calcule le factoriel :


Si dans l’état initial S, on a Sx=3
                            Alors                                     (*)
Pour montrer (*), il faut construire un arbre de dérivation à l’aide des règles (C1)-(C7)
avec (*) comme racine.

Posons                          B=
Sémantique Opérationnelle
 Evaluation des commandes
< 𝑦 ≔ 𝑦 ∗ 𝑥 , 𝑆[𝑦 ⟶ 3, 𝑥 ⟶ 2] > ⟶ 𝑆[𝑦 ⟶ 6, 𝑥 ⟶ 2] < 𝑥 ≔ 𝑥 − 1 , 𝑆[𝑦 ⟶ 6, 𝑥 ⟶ 2] > ⟶ 𝑆[𝑦 ⟶ 6, 𝑥 ⟶ 1]
                                     < 𝐵 , 𝑆[𝑦 ⟶ 3, 𝑥 ⟶ 2] > ⟶ 𝑆′


                    < 𝐵 , 𝑆[𝑦 ⟶ 3, 𝑥 ⟶ 2] > ⟶ 𝑆[𝑦 ⟶ 6, 𝑥 ⟶ 1] < 𝑊 , 𝑆′ > ⟶ 𝑆′
                                     < 𝑊 , 𝑆[𝑦 ⟶ 3, 𝑥 ⟶ 2] > ⟶ 𝑆′




              < 𝐵 , 𝑆[𝑦 ⟶ 1] > ⟶ 𝑆[𝑦 ⟶ 3, 𝑥 ⟶ 2] < 𝑊 , 𝑆[𝑦 ⟶ 3, 𝑥 ⟶ 2] > ⟶ 𝑆′
                                    < 𝑊 , 𝑆[𝑦 ⟶ 1] > ⟶ 𝑆′



                          < 𝑦 ≔ 1 , 𝑆 > ⟶ 𝑆[𝑦 ⟶ 1] < 𝑊 , 𝑆[𝑦 ⟶ 1] > ⟶ 𝑆′
                     𝐶3
                                          < 𝐹𝑎𝑐𝑡 , 𝑆 > ⟶ 𝑆′
Sémantique Axiomatique
Sémantique Axiomatique (SA)
 Par  SA (ou sémantique à base d’état explicite), on considère les sémantiques
   dans lesquelles l’état d’un programme est décrit par des assertions logiques.

 La    SA permet d’extraire des propriétés logiques des programmes à partir
   d’informations sur leurs états et sur l’évolution de l’état à la suite de l’exécution
   d’une instruction.

 La  SA rend compte par le biais d’un assertion logique (AL), des changements
   causés par une instruction sur l’état d’un programme.

                      SO                                      SA
        Manipule explicitement l’état du     AL qui exprime le changement suite à
                 programme                               une évolution

 La SA se fonde sur l’association de sens logique aux constructeurs (du langage
   de programmation) : « assigning meaning to programs » dont les bases ont été
   définies par Hoare et Dijkstra.
Sémantique Axiomatique


Logiques de Hoare et Dijkstra

  La SA permet :
   D’associer des expressions logiques décrivant l’état du programme
   De définir par des propriétés logiques les changements apportés à un état à la
     suite de l’exécution d’une instruction.

  On obtient ainsi un calcul (formel) sur les AL à partir des différentes opérations
  réalisées. Ce calcul est différent du calcul définit dans la SO. Il est destiné à la
  preuve des propriétés logiques sur les programmes.
Sémantique Axiomatique
Logiques de Hoare et Dijkstra

  Deux types de calcul (raisonnement) ont été définis :

  Un   calcul descendant (raisonnement déductif). Les AL associées à un état
    sont transformées par l’exécution d’une instruction jusqu'à la fin du programme.
    Hoare adopte cette méthode.

  Un   calcul ascendant (raisonnement abductif). En partant de la conclusion (à
    prouver), un calcul permet, à partir de l’instruction exécutée, de retrouver les
    prémisses (AL vraies). Dijkstra a suivi cette approche.
Sémantique Axiomatique
 Logique de Hoare




                               La LH se base sur la définition de deux AL
                               appelées Précondtion et Postccondition.
  Une action (ou programme) S est complètement
  spécifiée par la donnée de ses deux AL :


  P : précondition ; Q : postcondition
  P indique les conditions logiques qui doivent être satisfaites avant l’exécution de S
  Q indique, après l’exécution de S, les conditions logiques établies par S sachant que P est
  vérifié.
Sémantique Axiomatique
 Logique de Hoare

Interprétation du triplet de Hoare :




Si la propriété P est vraie pour les valeurs des variables du programme S avant son
exécution et si l’exécution de S se termine alors la propriété Q est vraie après
l’exécution de S.


                                     S
    Entrée E                    (Programme)          Sortie S
    Précondtion P(E)                                 Postcondtion Q(E,S)
Sémantique Axiomatique

 Logique de Hoare

    Exemple :
                                   Programme Divide

           E = {x, y}                a: = 0; b := x;                 O = {a, b}
                                     while (b >= y) do
                                        b :=: b –y;
                                        a := a + 1;
     P(E)  y > 0  x > 0             done                  Q(E, O)  x = ay + b  b < y




     Triplet de Hoare :
                            {y > 0  x > 0} Divide {x = a*y + b  b < y}
Sémantique Axiomatique
 Logique de Hoare
   Un triple de Hoare peut être vrai ou faux, exactement comme une formule logique
        Triplet vrai : {x = 2} x := x+1 {x = 3}

        Triplet faux : {x = 2} x := x+1 {x = 5}

   Définition 1 : Plus faible condition
       Soit un programme A et Q une postcondition.

       On dit que P est la plus faible précondition (wp : weakest pre-condition) qui conduit à
       Q en exécutant A si P est un prédicat qui définit le plus grand ensemble de valeurs
       des variables du programme A permettant toutes de passer dans un état qui satisfait
     Q, quand A est exécuté.
   Exemple:
                {x > 5} x := x + 1 {x > 6}, P = {x > 5} est la wp
                Par contre, {x > 6} n'est pas la wp (bien qu'elle conduit à x > 6)
Sémantique Axiomatique


 Logique de Hoare
   Définition 2 : (Plus forte condition)
   On dit que Q est la plus forte condition (sp : strongest condition) qui est atteinte
   en partant de P et en exécutant A, si Q est un prédicat définissant le plus petit
   ensemble de valeurs des variables du programme A qui sont atteintes à partir
   d'un état qui satisfait P, quand A est exécuté.

   Exemple :


                       sp : {x > 6}, par contre {x > 3} n’est pas une sp
Sémantique Axiomatique

 Sémantique axiomatique de Hoare
   Correction  des règles de Hoare : Etant donné un triplet t, s’il existe un arbre de
     déduction de Hoare complet ayant t à sa racine, alors le triplet est vrai. Les feuilles
     correspondent aux axiomes (règles sans prémisses).
   Construire  un arbre de déduction nécessite la définition de la sémantique de chaque
     construction de base du langage de programmation :
        Interprétation de SKIP : instruction neutre
        Interprétation de l’affectation :


                                                                         ⟵     ≔

    L’axiome (Aff) se lit : pour que P soit vraie pour x, après l’exécution de x := E, il fallait
    qu’elle soit vraie pour E avant l’exécution.
Sémantique Axiomatique

 Sémantique axiomatique de Hoare
   Interprétation de l’affectation :

                                                                         ⟵     ≔

     L’axiome (Aff) se lit : pour que P soit vraie pour x, après l’exécution de x := E, il
     fallait qu’elle soit vraie pour E avant l’exécution.

   Exemple

                (Aff)
                        𝒙 𝟏 𝟑 𝒙≔𝒙 𝟏 {𝒙 𝟑}
Sémantique Axiomatique
 Sémantique axiomatique de Hoare
   Construire   un arbre de déduction nécessite la définition de la sémantique de chaque
     construction de base du langage de programmation :

        Interprétation de la séquence : la séquence ou la composition séquentielle est
           l’opération de base permettant de composer des programmes. Elle décrit
           l’enchaînement des instructions.




        Exemple
                                 𝟎 𝒙 𝟎 𝒂≔𝟎 𝒂 𝒙 𝟎 ; 𝒂 𝒙 𝟎 𝒃≔𝒙 {𝒂 𝒃 𝟎}
                                        𝟎 𝒙 𝟎 𝒂≔𝟎 ;𝒃≔𝒙 {𝒂 𝒃 𝟎}
       
Sémantique Axiomatique
 Sémantique axiomatique de Hoare
   Construire   un arbre de déduction nécessite la définition de la sémantique de chaque
     construction de base du langage de programmation :

        Interprétation de la conditionnelle




        Exemple
Sémantique Axiomatique
 Sémantique axiomatique de Hoare
   Construire   un arbre de déduction nécessite la définition de la sémantique de chaque
     construction de base du langage de programmation :

        Interprétation de la répétition
Sémantique Axiomatique
 Sémantique axiomatique de Hoare
   Construire   un arbre de déduction nécessite la définition de la sémantique de chaque
     construction de base du langage de programmation :

        Interprétation de la répétition




                     : Typage

                                 : Terminaison
Sémantique Axiomatique
 Sémantique axiomatique de Hoare
   Règle  de conséquence : Deux règles particulières sont souvent utilisées lors de la
     preuve de programme.
          Renforcement de la précondition




        Affaiblissement de la postcondition




          Règle de conséquence

                  𝑷 ⟹ 𝑷′    𝑷 𝑺 𝑸     𝑸′ ⟹ 𝑸
           𝒄𝒐𝒏𝒔                                ∶ 𝒓è𝒈𝒍𝒆 𝒅𝒆 𝒄𝒐𝒏𝒔é𝒒𝒖𝒆𝒏𝒄𝒆
                            𝑷 𝑺 𝑸
Sémantique Axiomatique


Sémantique axiomatique de Hoare

  Exemple :

                 𝟎 𝒙 𝟎 𝒂≔𝟎 𝒂 𝒙 𝟎 ; 𝒂 𝒙 𝟎 𝒃≔𝒙 {𝒂 𝒃 𝟎}

                       𝟎 𝒙 𝟎 𝒂≔𝟎 ;𝒃≔𝒙 {𝒂 𝒃 𝟎}
Sémantique Axiomatique


Logique de Dijkstra
   A et B deux assertions.
      A   B : on dit que A est plus fort que B (et inversement, B est plus faible
     que A)

           Plus une formule contient une précondition faible et une post
             condition forte, plus elle est informative et intéressante.
Sémantique Axiomatique

 Logique de Dijkstra (LD)




    La logique de Dijkstra (LD) a été développée après celle de Hoare.

    Dijkstra propose un calcul, sur les assertions, de type ascendant. Il propose donc, en
      partant d'une post condition, de trouver la précondition la plus faible, qui vérifie le triplet
      de Hoare.

    Ainsi, on raisonne toujours sur des triplets, mais les règles sont établies dans l'autre
      sens.
Sémantique Axiomatique

LD : Concept de plus faible précondition
   Hypothèse :
        S : un programme (commande ou spécification)

        Q : une post condition (assertion logique)

   But :
           Calculer la plus faible précondition P telle que {P} S {Q} est vérifié.

   Cette plus faible précondition est notée : Wp(S,Q)
                           Par définition, on écrit : {P} S {Q}  Wp(S,Q)

   Wp(S,Q) : dénote la plus faible précondition telle que S termine et l’état satisfait
     Q après exécution de S.
Sémantique Axiomatique


LD : Concept de plus faible précondition
   Exemple :
        Wp(x:=x+1,x>0) = x      0

        Wp(i:=i+1,i   ) = i<n

        Wp(i:=0,i=0) = True

        Wp(i:=0,i=1) = False

        La pfc P de Wp(S,Q) est telle que :
Sémantique Axiomatique

 LD : Calcul de la plus faible précondition (pfc)
    Ci-dessous quelques règles de calcul de la pfc :

    Skip : Wp(skip,Q) = Q
    Affectation : Wp(x:=e,Q) = Q[x:=e]   : remplacer toutes les occurrence de x par E

         ou Wp(x := e, Q) = [x := e] Q

    Séquence :
                Wp(S ; S‘ , Q) = Wp(S ; Wp(S', Q))

    Conditionnelle                                                                      :

      Wp(if P then S1 else S2, Q) =
Sémantique Axiomatique

 LD : Calcul de la plus faible précondition (pfc)
   Conditionnelle                                                             :
      Wp(if P then S1 else S2, Q) =
    Exemple
           Wp(if x > 0 then x := 1 else x := x+1, x = 1) = Wp(, x = 1)
        

                                                                   

                                                  
                                          
                                                                      


                        Wp(, x = 1) =       
Sémantique Axiomatique

 LD : Calcul de la plus faible précondition (pfc)
   Ci-dessous Ci-dessous quelques règles de calcul de la pfc :
    Répétition : {P} T ; While C do S end {R}
        <= Condition suffisante :

        {P} T {I}                      -- établir l'invariant

                                       -- Préservation de l'invariant

                                       -- sortie de la boucle

                                       -- variant



        Remarque :            = [S]Q
Sémantique Axiomatique


LD : Calcul de la plus faible précondition (pfc)
  Ci-dessous Ci-dessous quelques règles de calcul de la pfc :
   Répétition : {P} T ; While C do S end {R}
   Exemple :
         Wp(x:=0; while x<10 do x:=x+1 end, (x=10)) =

         INVARIANT :

         VARIANT : 10 – x

         Remarque : Wp(, (x=10)) = [] Q
Sémantique Axiomatique

 LD : Calcul de la plus faible précondition (pfc)
    Exemple :
          Wp(x:=0; while x<10 do x:=x+1 end, (x=10))
          INVARIANT :
          VARIANT : 10 – x
        {P} T {I}                         -- établir l'invariant
          [x := 0] I = [x := 0] (0
                     =                True
                                                   -- Préservation de l'invariant




                                               True
Sémantique Axiomatique

 LD : Calcul de la plus faible précondition (pfc)
    Exemple :
          Wp(x:=0; while x<10 do x:=x+1 end, (x=10))
          INVARIANT : 0 ≤ 𝑥 < 10
          VARIANT : 10 – x

                                             -- sortie de la boucle


                                                        True
                                             -- variant


                                                          True
Sémantique Axiomatique

 LD : Calcul de la plus faible précondition (pfc)
    Exemple :
          Wp(x:=0; while x<10 do x:=x+1 end, (x=10))
          INVARIANT : 0 ≤ 𝑥 < 10
          VARIANT : 10 – x




                                                x      x+1
                                                x      x+1
                                                              True
Sémantique Axiomatique


 LD : Calcul de la plus faible précondition (pfc)

    Autres commandes :
    Wp(PRE p then S end, Q) = P     Wp(S,Q)

    Wp(Select P then S end,Q) = P     Wp(S,Q)

    Wp(choice S or T end,Q) = Wp(S,Q)   Wp(T,Q)
Sémantique Axiomatique


 LD : Calcul de la plus faible précondition (pfc)

    Remarque :
        Wp est une fonction à deux arguments : une instruction S et un prédicat Q.
        Pour un S fixé, on peut voir Wp(S, Q) comme une fonction à un seul
        argument Wps(Q)

        La fonction Wps(Q) est appelée transformateurs de prédicats. Il associe à Q
        la plus faible précondition P telle que {P} S {Q}.
Sémantique Axiomatique


 LD : Calcul de la plus faible précondition (pfc)

    Exercice :
          Wp(z:=2; y:=z+1; x:=y+z, x   3 ..8)
          = Wp(z:=2; Wp(y:=z+1; Wp(x:=y+z, x 3..8)))
          = Wp(z:=2; Wp(y:=z+1,y+z     3..8))
          = Wp(z:=2 ; z+1+z 3..8)
          = 2+1+2 3.. 8
          = TRUE
