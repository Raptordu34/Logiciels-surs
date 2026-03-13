   Model Checking
         &
Logiques Temporelles
         LOS
       Chapitre 5
Détails du Chapitre 5
   Définitions générales
     Systèmes réactifs
     Propriétés temporelles
     Systèmes de transitions
     Automates
  Langage de la logique temporelle
   Syntaxe de la logique temporelle
  Sémantique de la logique temporelle
Définitions générales
 Définitions générales

 Systèmes réactifs
    Programme Standard
        Se termine, retourne un résultat, manipule des données complexes
        Sa structure de contrôle est assez simple (propriétés à prouver à l'aide de la LH)
        Exemples : compilateur, algorithme de tri, etc.

    Systèmes réactifs
        Ils ne se terminent pas forcément
        Ils ne calculent pas un résultat (mais plutôt maintiennent une interaction)
        Les types de données manipulés sont souvent simples, mais le contrôle est complexe
       (exécution de plusieurs composants en parallèle)
        Ils interagissent avec un environnement par le biais de capteurs (prise d'info) et
       d'actionneurs (action)
        Exemple : Systèmes embraqués pour transport/énergie, OS, Protocoles de communication,
       Système ascenseur, feux de croisement, ....
 Définitions générales
 Systèmes réactifs
 Définitions générales

Propriétés temporelles
    Programme Standard
       Propriétés à vérifier impliquent des prédicats très riches sur les données manipulées (ex.
        tableau est trié)
       Aspects temporels très restreints (toujours identiques)

    Systèmes réactifs
       Aspect temporel est très varié (relations temporelles de précédences, …)
       Prédicats sur les données sont souvent simples (ex. x  0)
          Si un processus demande infiniment souvent à être exécuté alors l'OS finira par
           l'exécuter
          Chaque fois qu'une panne est détectée, une alarme est émise

    Pour exprimer des propriétés temporelles, on utilise des logiques
    temporelles
       Décrivent les comportements temporels d'une manière non ambiguë
       Souplesse et généricité des algorithmes exprimables dans une certaine logique
 Définitions générales

 Model-Checking
    Une technique de la vérification formelle
       Pour prouver formellement la correction d’une spécification ou d’un programme
       Utilisée pour vérifier des logiciels en particulier le logiciel temps réel et critique

    Ingrédients :
       Une formule logique F (en logique LTL, CTL, etc.)
       Un modèle/abstraction finie du système, sous forme d’un système de transition S
       Question : Est-ce que S satisfait F? ou est ce que S est un modèle pour F


    D’où le nom de Model-Checking

   Les outils de model-checking rendent un verdict : oui (la propriété est satisfaite) ou
    non. En général, les outils fonctionnent à l’aide de contre exemples.
 Définitions générales

 Model-Checking




               Principe simplifié du model-checking
 Définitions générales

Propriétés temporelles
    Programme Standard
       Propriétés à vérifier impliquent des prédicats très riches sur les données manipulées (ex.
        tableau est trié)
       Aspects temporels très restreints (toujours identiques)

    Systèmes réactifs
       Aspect temporel est très varié (relations temporelles de précédences, …)
       Prédicats sur les données sont souvent simples (ex. x  0)
          Si un processus demande infiniment souvent à être exécuté alors l'OS finira par
           l'exécuter
          Chaque fois qu'une panne est détectée, une alarme est émise

    Pour exprimer des propriétés temporelles, on utilise des logiques
    temporelles
       Décrivent les comportements temporels d'une manière non ambiguë
       Souplesse et généricité des algorithmes exprimables dans une certaine logique
 Définitions générales

 Systèmes de transitions (ST)
    ST    permet de représenter le comportement d’un ensemble de processus
    (d’un système concurrent, d’un système réactif)

   Il est défini par un quadruplet S = (Q, E, T, q0) : ST de transitions étiquetés
       Q : Un ensemble fini d’états
       E : Ensemble fini des étiquettes associées aux transitions
       T  Q  E  Q : Ensemble de transitions                      Q = {s0, s1}
           Une transition est une relation entre                    E = {a, b}
            deux états de Q, étiquetée par un élément de E.          q0 = s 0

       q0 : est l’élément initial, q0  Q

    Une transition t est un triplet t = (p, e, q)
       que l’on note
 Définitions générales

 Systèmes de transitions (ST) : Exemples

   Système d’un ascenseur :
       Ensemble de processus : cabine, contrôleur, porte_i
       3 étages
       Système (porte_0 || porte_1 || porte_2 || cabine || contrôleur)
       cabine :

           ?down
                                                                              ?up
                               ?up                       ?up


                    0                          1                          2


                             ?down                     ?down
 Définitions générales
 Systèmes de transitions (ST) : Exemples
   Un système à 3 processus exécutant concurremment (par entrelacement) :
                    boucle              boucle            boucle
                    x  y+1             yx               y0

       Le système peut-être décrit en termes d’états :




   Propriétés désirables :
       L’état 4,2 est-il accessible?
       Le système s’arrête-il? toujours, parfois?
       Est-il toujours vrai que y = 0  0  x – y  1?
 Définitions générales
 Systèmes de transitions (ST) : Exemples
   Soit un système de digicode à 3 touches A, B et C
       La porte s’ouvre quand ABA est saisi

       Le digicode est dans l’état initial après saisie d’un mauvais code.

    Le digicode peut-être décrit par le ST suivant :
 Définitions générales

 Systèmes de transitions (ST) :
    ST est aussi appelé automate
   Systèmes réactifs présentent souvent des comportements infinis
     (pas d’états terminaux, nombre d’états possibles infinis, exécution
     infinie possible)
 Définitions générales

 Automates et propriétés : Définitions
                      : ensemble de propositions élémentaires décrivant des
     propriétés associées aux états

   Un automate, dans ce cas, est un quadruplet A = (Q, E, T, q0, l) où :
        Q, E, T, q0 : même définition que précédemment
        l : application qui associe à tout état de Q l’ensemble fini des propriétés
            élémentaires vérifiées dans cet état.

                  𝒊      𝒌    𝒌         𝒊     𝒌   ,   : relation de satisfaction
   L’application l permet entre autre de :
        Décrire les variables d’états qui caractérisent un système de processus
        Les observer lors d’un changement d’état
Définitions générales


 Automates et propriétés : Comportement
   Illustré en termes de chemins dans un automate A = (Q, E, T, q0, l)
   Un chemin dans A est une suite             , finie ou infinie de :
       transitions            de A, qui
       s’enchaînent, c-à-d,

   Un chemin est noté
   Longueur de chemin :
       nombre de transitions qu’il contient
                      : peut-être finie ou non
 Définitions générales


 Automates et propriétés : Comportement
   En    terminologie des systèmes de processus, un chemin est également
    désigné par le mot trace

   Exécution partielle
       Chemin partant de l’état initial

   Exécution complète
       Exécution partielle maximale (qui ne peut être prolongée)
 Langage de la logique temporelle
 Règle de composition concurrente
   Besoin d’un nouveau modèle
       Soit un système concurrent formé par deux processus Proc1 et Proc2
       On est tenté par écrire pour ce programme la règle de composition concurrente
      suivante (issue d’une extension de la LH)

                 𝟏       𝟏   𝟏           𝟐      𝟐       𝟐
                     𝟏   𝟐       𝟏        𝟐         𝟐

    Mais,   la règle est fausse s’il y a de l’interaction (via des mémoires
    partagées) entre les processus Proc1 et Proc2

   Besoin donc d’un autre modèle pour raisonner sur les propriétés globales
    des programmes concurrents (les exprimer, vérifier et prouver)
 Langage de la logique temporelle
 Logique temporelle (LT)
   LT est un langage décrivant les propriétés des séquencements d’états

       Chaque état dans la séquence donne une valeur de vérité à des propositions
      atomiques

    LT est une extension de la logique des propositions
   LT utilise des opérateurs temporels pour parler du futur et du passé
       Exemples :
          p est vrai à l’instant (ou état) suivant
          p finit par être vrai dans le futur
          Quand je vois p, je vois ensuite q exactement 3 observations après
 Langage de la logique temporelle

 Logique temporelle :
   Propriétés temporelles : utiles en vérification
       Accessibilité : Une certaine situation peut être atteinte
          Le compteur x peut valoir 0
       Sureté : Quelque chose de mauvais n’arrive jamais
          J’accède au fichier uniquement si j’ai entré le bon PIN
       Invariance : Chaque état local respecte une bonne propriété
          Pas de division par 0, le tableau ne déborde jamais
       Vivacité : Quelque chose de bon finit par arriver
          Le programme termine, le message finit toujours par être transmis
       Equité : Quelque chose de bon se répète infiniment souvent (variante de la vivacité)
          si un processus demande toujours la main, il l’aura infiniment

    La plupart des propriétés intéressantes sur les systèmes de processus
    peuvent s’exprimer comme la conjonction de sûreté et de vivacité.
 Langage de la logique temporelle

 Logique temporelle : 3 Composantes essentielles
   Propositions :
       Permettent de caractériser les états qui apparaissent dans les comportements (les
      séquencements)
          Pi est vraie dans l’état q si Pi  l(q)
    Connecteurs logiques :
       Connecteurs classiques , , ,  et  : indispensables pour construire des
      formules logiques complexes.

   Connecteurs temporels :
       Permettent de décrire les séquencements des états/événements observés le long
      d’une exécution.
 Langage de la logique temporelle

 Logique temporelle : 3 Composantes essentielles
   Connecteurs temporels :




      Next noté aussi X, Future F, Always G (pour Globally) et Until U
 Langage de la logique temporelle
 Logique temporelle : 3 Composants essentielles
   Connecteurs temporels : Intuition sémantique
 Langage de la logique temporelle
 Logique temporelle : 3 Composants essentielles
   Connecteurs temporels : Intuition sémantique
 Langage de la logique temporelle
 Logique temporelle : 3 Composantes essentielles
   Connecteurs temporels : Exemple




       Dans le 4ème état : on peut observer que les propositions
              pq et (pq) sont vraies
              p est fausse
   Opérateurs minimaux : {, U} forme un ensemble minimal d’opérateurs
       p  true U p
       p  p
              (p  q)
 Langage de la logique temporelle

 Logique temporelle : 3 Composantes essentielles
   Plus d’exemples :
       pp : énonce p est vraie dans l’état courant et sera vraie dans l’état suivant
       p   : p vraie dans l’état suivant de l’état suivant
       (p      p)   : signifie que toujours quand p est vraie dans un état s, elle sera
                           fausse dans l’état suivant de s
       (p    q) : signifie que toujours quand p est vraie dans s, q sera vraie dans l’état
                      suivant de s
       (p      (q U   r)) : signifie que toujours quand p est vraie dans un état s, alors q
                                 reste fausse à partir de l’état suivant de s jusqu’à l’état où r
                                 est vraie
 Langage de la logique temporelle

 Logique temporelle : 3 Composantes essentielles
   Opérateurs complémentaires :


          Opérateur        W : Weak-Until ou le           R : Release
                               Waiting-for

          Définition       p W q  p  p U q       p R q  q  q U (p  q)

                        On exprime que p soit vrai
                        jusqu’à ce que q le soit, informally means that q is
         Sémantique     mais sans exiger que q true until p becomes true,
                        finisse par être vraie, et si q or q is true forever.
                        n’a jamais lieu, alors p
                        restera indéfiniment vrai
 Langage de la logique temporelle

 Logique temporelle : 3 Composantes essentielles
   Equivalence des formules de LT
 Langage de la logique temporelle

 Logique temporelle : 3 Composantes essentielles
   Mais attention …………………
 Langage de la logique temporelle

 Logique temporelle : Fragment linéaire

        Jusqu’à   maintenant,    on   a   considéré    une      seule
        exécution du système, les connecteurs permettent
        d’exprimer des propriétés le long de cette exécution.
        C’est une vision linaire du temps : le futur est fixé



       On parle de Logique Temporelle Linéaire (LTL)
 Langage de la logique temporelle

 Logique temporelle : Fragment branchant ou arborescent

        Le temps peut être aussi vu comme une structure
        branchante : à partir d’un même état, plusieurs futurs
        sont possibles (selon l’action qui sera effectuée).




       On parle de Logique arborescente (CTL)
 Langage de la logique temporelle

 Logique CTL : Computation Tree Logic
     La logique initiale de E. Clarke et E. Emerson




Professor Emeritus in the Dept. of Computer   Regents Chair and Professor of Computer Science,
Science at Carnegie Mellon University,        University of Texas in Austin,
ACM Turing Award in 2007                      ACM Turing Award in 2007
 Langage de la logique temporelle

 Logique CTL : Computation Tree Logic
   Logique temporelle arborescente (plusieurs futures sont possibles)
   Considère      le système de transition non étiquetées plutôt que les
    traces du système.

   CTL est une restriction de la logique CTL* :                                       ∗


       CTL * est une logique branchante très expressive

       CTL* combine les opérateurs temporels linéaires et arborescents

          Opérateurs arborescents : Quantificateurs de chemins (utilisés librement)

          Ce qui permet d’exprimer des propriétés sur les arbres d’exécution
 Langage de la logique temporelle

 Logique CTL : Computation Tree Logic
 Langage de la logique temporelle

 Logique CTL : Computation Tree Logic
   Les   chemins (ou comportements sont donc des parcours ou des
    branches particuliers dans l’arborescence des comportements
 Langage de la logique temporelle

 Logique CTL : Computation Tree Logic
   Opérateurs de chemins
          : Signifie que toutes les exécutions, partant de l’état courant, satisfont la
             propriété
         : Signifie qu’il existe (au moins) une exécution, partant de l’état courant, qui
            satisfait la propriété

   Ne pas confondre :          et  Opérateurs
         : toutes les exécutions possibles maintenant satisfont
       : à tout instant (ou état) de l’exécution considérée   est vérifiée

   Liens entre quantificateurs de chemins
 Langage de la logique temporelle


 Logique CTL : Computation Tree Logic
   Un   quantificateur de chemin peut être associé à une formule de
     chemin bâtie sur ,,, U (avec s l’état courant)

   Opérateurs   temporels linéaires,,, U doivent être immédiatement
    précédés d’opérateurs de chemins ,

   Exemple
      EF(AGp) dans CTL

      E(Gp   Xq) pas dans CTL, AFGp pas dans CTL
   Langage de la logique temporelle




Course Organization (unibz.it)
 Langage de la logique temporelle

 Logique CTL : Computation Tree Logic


    Formule                                Sémantique
     AFp      Tous les chemins partant de s finissent par atteindre p

     AGp      p est toujours vrai en partant de s (aussi vrai dans s)



     EFp       un chemin partant de s qui atteint p

     EGp       un chemin partant de s tel que p est vraie le long du chemin
 Syntaxe de la logique temporelle

 LTL v.s. CTL
   Certaines formules de LTL ne peuvent pas être exprimées dans CTL
      
       F(p  Xp)

   Certaines formules de CTL ne peuvent pas être exprimées dans LTL
      
       GEF p

     Ne peuvent pas être exprimées = il n'y a pas de formule équivalente
 Syntaxe de la logique temporelle

 Comparaison (LTL, CTL, CLT*)
Syntaxe de la logique
     temporelle
 Syntaxe de la logique temporelle

 Logique LTL : sur un chemin
   Grammaire

      AP : ensemble des propositions atomiques
      {, , } : connecteurs logiques
      {X, F, G, U} : connecteurs temporels

   Domaine d‘interprétation : ensemble de chemins 
                𝟎 𝟏 𝟐    𝒏    : séquence infinie d’états s de Q
         𝒊   : chemin extrait de    à partir de la i-ème position,   𝟐
                                                                           𝟐 𝟑    𝒏

               : désigne le k-ième état de 
       Fonction               𝑨𝑷   indique quelles propriétés            sont vraies dans un s de
      Q
 Syntaxe de la logique temporelle

 Logique LTL : sur une structure de Kriple
   Modèle de Kriple : M
      Q : ensemble des états
                  : relation de transition
      AP : ensemble des propositions atomiques
                𝑨𝑷
                     : fonction d’étiquetage des états (propriétés vraies)
       𝟎     : l’état initial
   Domaine d’interprétation : un couple (M, s)
   Grammaire
       Formules LTL sur une structure de Kriple de la forme A où  est une formule LTL
      de chemin
 Syntaxe de la logique temporelle

 Logique CTL* :
   Formules : Deux types
       Formules d’état (   ), interprétées sur les états de la structure de Kriple
       Formules de chemin (     ), interprétées sur les chemins de la structure de Kriple

   Grammaire




   Domaine d’interprétation : un couple (M, s)
 Syntaxe de la logique temporelle

 Logique CTL :
   CTL restriction branchante de CTL*
       A, E libres
       X, F,G,U doivent être précédés directement de A, E

   Formule CTL s’obtient à partir de
       de {, , }
       et des opérateurs
          AX et EX
         AF et EF
         AG et EG
         AU et EU
Sémantique de la logique
      temporelle
 Sémantique de la logique temporelle

 Relation de satisfaction / satisfaisabilité :
    Modèle d’un système de transitions : M
    Formule temporelle 
    Questions :
      M     ? : M valide – t-il (satisfait-il)  ?  est – elle vraie dans M ?
         M,       ? :  valide – t-il (satisfait-il)  ?  est – elle vraie dans  ?

    Notation
       M, , i     : signifie au temps i (instant ou état) de l’exécution (calcul ou chemin)
                        de M, la formule  est vraie.
       On peut omettre M (le même système étudié) : , i          
 Sémantique de la logique temporelle

 Formule LTL :
   Satisfaisabilité sur un chemin 
 Sémantique de la logique temporelle

 Formule LTL :
   Satisfaisabilité sur un couple (M, s)




                        M      ssi M
                                  OU
            M      ssi, pour toute exécution   M, on a
 Sémantique de la logique temporelle
 Formule CTL* :
 Sémantique de la logique temporelle


 Formule CTL* :

                     M     ssi M
                               OU
           M    ssi, pour toute exécution   M, on a
 Sémantique de la logique temporelle
 Formule CTL* :
Sémantique de la logique temporelle

 Exemples
  Négation
                      ( : ne valide pas ou ne satisfait pas)
    M      : Il existe au moins une exécution (chemin) qui invalide  mais pas toutes
               les exécutions le font.
     En LTL, on peut avoir : M   M      
         a ? a ?
Sémantique de la logique temporelle

 Exemples
  Exemple
Sémantique de la logique temporelle

 Exemples
  Exemple 1 :
Sémantique de la logique temporelle

 Exemples
  Exemple 2 :
    Soit le système de transitions ST ci-dessous.

    Soit la formule logique  = a. Montrer que les deux formules AFAG et FG ne sont
    pas équivalentes.
Sémantique de la logique temporelle
 Exemples
  Exemple 3 :
    You are given the following Kripke model M :
Sémantique de la logique temporelle
 Exemples
  Exemple 3 (Cont):
Algorithmes de Model-Checking




    Reste à étudier les algorithmes de Model-Checking
                    pour LTL et CTL
