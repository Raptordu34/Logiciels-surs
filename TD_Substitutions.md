# TD : Substitutions en Méthode B

## Exercice : Calcul de substitution séquentielle

**Énoncé :** Calculer $[x := x+2 ; x := x+4] (x > 9)$

**Calcul :**
1. $[x := x+4](x > 9) \equiv x+4 > 9$
2. $[x := x+2](x+4 > 9) \equiv (x+2)+4 > 9$
3. Simplification : $x+6 > 9 \equiv x > 3$

**Résultat :**
$$x > 3$$

---

**Énoncé :** Calculer $[y := x+y ; x := y-x] (y \ge 5 \land x \le 3)$

**Calcul :**
1. $[x := y-x](y \ge 5 \land x \le 3) \equiv y \ge 5 \land (y-x) \le 3$
2. $[y := x+y](y \ge 5 \land (y-x) \le 3) \equiv (x+y) \ge 5 \land ((x+y)-x) \le 3$
3. Simplification : $x+y \ge 5 \land y \le 3$

**Résultat :**
$$x+y \ge 5 \land y \le 3$$

---

## Concept : Pourquoi utiliser des substitutions ?

En méthode B, on ne considère pas une instruction comme un changement de valeur, mais comme un **transformateur de prédicat**.

### Comparaison
- **Code classique** : On part de l'état A vers l'état B (Exécution).
- **Substitution B** : On part de la propriété souhaitée à la fin ($P$) et on remonte pour savoir quelle propriété devait être vraie au début ($[S]P$).

### Utilité majeure
1. **Garantie de sécurité** : Vérifier que $[S]Invariant$ est toujours vrai.
2. **Abstraction** : Décrire des comportements sans entrer dans le détail de l'implémentation (ex: choix non-déterministe).
3. **Preuve automatique** : Transformer du "code" en "équations" que l'ordinateur peut résoudre.
