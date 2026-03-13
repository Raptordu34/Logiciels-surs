# Correction du TD 2 - Logiciels Sûrs

Cette correction est basée sur les énoncés présents dans les images du dossier `Sources/TD2`. Notez que l'exercice 3 n'était pas présent sur les photographies et a donc été omis.

## Exercice 1 : Calcul de substitutions (Plus Faible Précondition)

L'objectif est de calculer la substitution $[S]R$ (qui correspond à la plus faible précondition $wp(S, R)$ de la méthode de Dijkstra).

**Règle pour la séquence :** $[S_1 ; S_2] R \iff [S_1] ([S_2] R)$

**1) $[x := x+2 ; x := x+4] (x > 9)$**
*   On applique d'abord la deuxième affectation :
    $[x := x+2] (x+4 > 9)$
    $[x := x+2] (x > 5)$
*   Puis on applique la première affectation :
    $(x+2) > 5$
*   **Résultat :** $x > 3$

**2) $[y := x+y ; x := y-x] (y \ge 5 \land x \le 3)$**
*   On applique d'abord la deuxième affectation (on remplace $x$ par $y-x$) :
    $[y := x+y] (y \ge 5 \land (y-x) \le 3)$
*   Puis on applique la première affectation (on remplace $y$ par $x+y$) :
    $(x+y) \ge 5 \land ((x+y)-x) \le 3$
*   **Résultat :** $x+y \ge 5 \land y \le 3$

**3) $[x := y ; y := x^2] (y > x)$**
*   On applique d'abord la deuxième affectation :
    $[x := y] (x^2 > x)$
*   Puis on applique la première affectation :
    $y^2 > y$
*   **Résultat :** $y^2 > y$ (ou de manière équivalente $y(y-1) > 0$, donc $y < 0$ ou $y > 1$)

---

## Exercice 2 : Invariant et Variant de boucle (Produit)

Le programme calcule le produit des éléments d'un tableau de taille $N$.

```text
prod := 1;
i := 0;
while i < N do
  i := i+1 ; 
  prod := prod * a(i);
INVARIANT ...
VARIANT ...
end
Postcondition : prod = Π_{j ∈ 1..N} a(j)
```

*   **Invariant :** À chaque itération, `prod` contient le produit des éléments de `1` à `i`. Il faut aussi borner `i`.
    $I \equiv i \in 0..N \land prod = \prod_{j=1}^{i} a(j)$
    *(Convention : si $i=0$, le produit d'un ensemble vide est l'élément neutre $1$, ce qui correspond bien à l'initialisation).*
*   **Variant :** C'est une fonction qui doit décroître strictement à chaque itération et rester positive. La boucle s'arrête quand $i = N$.
    $V \equiv N - i$

---

## Exercice 4 : Multiplication égyptienne

L'algorithme proposé effectue la multiplication $a \times b$ en utilisant des additions, des multiplications par 2 et des divisions par 2.

```text
x := a;
y := b;
total := 0;
while x > 0 do
  if x mod 2 = 1 then
    total := total + y ; x := x - 1;
  end;
  x := x/2;
  y := y*2;
  INVARIANT x ∈ IN ∧ total + x * y = a * b
  VARIANT x
end
Postcondition : total = a * b
```

**Preuve de correction rapide :**

1.  **Initialisation :** Avant la boucle, $x=a$, $y=b$, $total=0$.
    On a bien $total + x \times y = 0 + a \times b = a \times b$. L'invariant est vérifié.
2.  **Préservation de l'invariant :** Supposons l'invariant vrai au début d'une itération.
    *   **Cas où $x$ est impair ($x \bmod 2 = 1$) :** 
        Nouvelles valeurs (en fin d'itération) : $x' = (x-1)/2$, $y' = y \times 2$, $total' = total + y$.
        Vérifions : $total' + x' \times y' = (total + y) + \frac{x-1}{2} \times (y \times 2) = total + y + (x-1)y = total + y + xy - y = total + xy = a \times b$. L'invariant est préservé.
    *   **Cas où $x$ est pair ($x \bmod 2 = 0$) :**
        Nouvelles valeurs : $x' = x/2$, $y' = y \times 2$, $total' = total$.
        Vérifions : $total' + x' \times y' = total + \frac{x}{2} \times (y \times 2) = total + xy = a \times b$. L'invariant est préservé.
3.  **Terminaison et Postcondition :**
    Le variant $V = x$ décroît strictement car à chaque tour $x$ devient soit $x/2$ soit $(x-1)/2$. Puisque la boucle tourne tant que $x>0$, la valeur finira par atteindre $0$.
    En sortie de boucle, la condition $x>0$ est fausse. Puisque l'invariant dit que $x \in \mathbb{N}$, cela implique $x=0$.
    On remplace dans l'invariant : $total + 0 \times y = a \times b \implies total = a \times b$. La postcondition est prouvée.

---

## Exercice 5 : Feux de circulation

Il s'agit d'écrire une Machine Abstraite B pour modéliser le carrefour.

**Propriétés à respecter :**
*   *Sûreté* : Si une direction est Vert ou Orange, l'autre est obligatoirement Rouge.
*   *Séquentialité* : L'ordre des couleurs est Rouge -> Vert -> Orange -> Rouge.

```b
MACHINE 
  FeuxCirculation

SETS
  COULEUR = {Rouge, Vert, Orange};
  DIRECTION = {EstOuest, NordSud}

VARIABLES
  feux

INVARIANT
  /* feux est une fonction totale : à chaque direction correspond exactement une couleur */
  feux : DIRECTION --> COULEUR &
  /* Propriété de Sûreté */
  (feux(EstOuest) : {Vert, Orange} => feux(NordSud) = Rouge) &
  (feux(NordSud) : {Vert, Orange} => feux(EstOuest) = Rouge)

INITIALISATION
  /* Initialisation de la fonction : toutes les directions sont au Rouge */
  feux := DIRECTION * {Rouge}

OPERATIONS

  PasseAuVert(dir) =
  PRE
    dir : DIRECTION &
    /* Séquentialité : on passe au Vert depuis le Rouge */
    feux(dir) = Rouge &
    /* Sûreté : l'autre direction doit aussi être au Rouge */
    (dir = EstOuest => feux(NordSud) = Rouge) &
    (dir = NordSud => feux(EstOuest) = Rouge)
  THEN
    feux(dir) := Vert
  END;

  PasseAlOrange(dir) =
  PRE
    dir : DIRECTION &
    /* Séquentialité : on passe à l'Orange depuis le Vert */
    feux(dir) = Vert
  THEN
    feux(dir) := Orange
  END;

  PasseAuRouge(dir) =
  PRE
    dir : DIRECTION &
    /* Séquentialité : on passe au Rouge depuis l'Orange */
    feux(dir) = Orange
  THEN
    feux(dir) := Rouge
  END

END
```

---

## Exercice 6 : Auto-école RAMOA

### 1- Analyse informelle du problème
*   L'ensemble de base est la population globale `POP`.
*   Les ensembles manipulés sont : `inscrit` (élèves actuels), `aCode` (élèves ayant le code, c'est un sous-ensemble de `inscrit`), et `aPermis` (anciens élèves avec permis).
*   **Contrainte vitale :** Un ancien élève (`aPermis`) ne peut plus être inscrit. Donc l'intersection entre `inscrit` et `aPermis` doit être vide.

### 2- Machine abstraite complétée (ANNEXE 1)

```b
MACHINE
  autoEcole_Ramoa

SETS
  POP

VARIABLES
  inscrit, aCode, aPermis

INVARIANT
  inscrit <: POP &
  aCode <: inscrit &
  aPermis <: POP &
  inscrit /\ aPermis = {} /* Intersection vide : on n'est pas à la fois inscrit et ancien élève */

INITIALISATION
  inscrit, aCode, aPermis := {}, {}, {}

OPERATIONS

  inscrire(pp) =
  PRE
    pp : POP & 
    pp /: inscrit & 
    pp /: aPermis
  THEN
    inscrit := inscrit \/ {pp}
  END;

  succesCode(pp) =
  PRE
    pp : inscrit & 
    pp /: aCode
  THEN
    aCode := aCode \/ {pp}
  END;

  succesPermis(pp) =
  PRE
    pp : aCode /* Pour avoir le permis, il faut avoir le code */
  THEN
    /* L'élève quitte l'auto-école et obtient son permis */
    aCode := aCode - {pp} ||
    inscrit := inscrit - {pp} ||
    aPermis := aPermis \/ {pp}
  END;

  abandon(pp) =
  PRE
    pp : inscrit
  THEN
    /* L'élève quitte l'auto-école, on lui retire ses statuts d'inscrit */
    inscrit := inscrit - {pp} ||
    aCode := aCode - {pp}
  END

END
```

### 3- Obligations de preuve (simplifiées)

Les Obligations de Preuve (OP) consistent à démontrer que chaque modification préserve l'invariant global du système.

*   **Pour l'initialisation :**
    *   `{} <: POP` (Vrai)
    *   `{} <: {}` (Vrai)
    *   `{} /\ {} = {}` (Vrai)
*   **Pour `inscrire(pp)` :**
    *   L'invariant demande `aCode <: inscrit`. Après ajout, on aura `aCode <: (inscrit \/ {pp})`, ce qui reste vrai si l'invariant précédent était vrai.
    *   L'invariant demande `inscrit /\ aPermis = {}`. Après ajout, `(inscrit \/ {pp}) /\ aPermis = {}` est vérifié car la précondition exige explicitement que `pp /: aPermis`.
*   **Pour `succesPermis(pp)` :**
    *   L'invariant demande `aPermis <: POP`. Après ajout, on a `(aPermis \/ {pp}) <: POP`. C'est vrai car `pp : aCode`, or `aCode <: inscrit <: POP`, donc `pp : POP`.
    *   L'invariant de non-chevauchement `(inscrit - {pp}) /\ (aPermis \/ {pp}) = {}` reste vrai car on a expressément retiré `pp` de l'ensemble `inscrit` avant de l'ajouter à `aPermis`.
*   **Pour `abandon(pp)` :**
    *   L'invariant demande `aCode <: inscrit`. On retire `pp` des deux côtés (s'il l'avait), l'inclusion `(aCode - {pp}) <: (inscrit - {pp})` reste donc valide.
    *   L'intersection avec `aPermis` reste vide car on ne fait que retirer un élément de `inscrit`.
