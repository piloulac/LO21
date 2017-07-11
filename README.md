# LO21
Development of a scientific calculator with Reverse Polish Notation in C++

# UTComputer : Calculatrice RPN

La notation polonaise inversée permet une écriture arithmétique sans ambiguité et sans parenthèses :

- `1 + 1` donne `1 1 +` en RPN.
- `2 * 2 + 1` donne `2 2 * 1 +`
- `(2 + 3) * 4` donne `2 3 + 4 *`

Cela nécessite l'implémentation d'une pile pour le calcul :

- Si l'opérande est une littérale, elle est empiler sur la pile
- Si l'opérande est un opérateur d'arité *n*, *n* expressions sont dépilés et le résultat du calcul est empilé. 

Un opérateur a **une et une seule** arité. 

## Priorité des opérateurs

Associativité : De gauche à droite

Il manque des opérateurs. 

| Opérateur | Priorité | Arité |
|:---------:|:--------:|:--------:|
| `()` | 9 | Pas vraiment un opérateur |
| `$` | **8** | unaire |
| `NEG` | 7 | unaire |
| `NOT` | 7 | unaire |
| `*` | **6** | binaire |
| `/` | **6** | binaire |
| `MOD` | **6** | binaire |
| `DIV` | **6** | binaire |
| `+` | 5 | binaire |
| `-` | 5 | binaire | 
| `<` | **4** | binaire |
| `<=` | **4** | binaire |
| `>` | **4** | binaire |
| `>=` | **4** | binaire |
| `=` | 3 | binaire |
| `!=` | 3 | binaire |
| `AND` | **2** | binaire |
| `OR` | 1 | binaire |
| Autres (opérateurs de pile, etc.) | 0 | Pas d'arité |


## Options de l'application

- Affichage du clavier
- X derniers éléments de la pile à afficher
- Bip sonore (message utilisateurs)

## Opérations

### +

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleEntière` | `LittéraleEntière` | `LittéraleEntière` |
| `LittéraleRationnelle` | `LittéraleRationnelle` | `LittéraleRationnelle` ou `LittéraleEntière` (si dénominateur = 1) |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle`| `LittéraleRéelle` | `LittéraleRéelle` |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle` (`LittéraleNumérique`) | `LittéraleComplexe` | `LittéraleComplexe` ou `LittéraleNumérique` (si partie imaginaire = 0) |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |

### -

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleEntière` | `LittéraleEntière` | `LittéraleEntière` |
| `LittéraleRationnelle` | `LittéraleRationnelle` | `LittéraleRationnelle` ou `LittéraleEntière` (si dénominateur = 1) |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle`| `LittéraleRéelle` | `LittéraleRéelle` |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle` (`LittéraleNumérique`) | `LittéraleComplexe` | `LittéraleComplexe` ou `LittéraleNumérique` (si partie imaginaire = 0) |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |

### *

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleEntière` | `LittéraleEntière` | `LittéraleEntière` |
| `LittéraleRationnelle` | `LittéraleRationnelle` | `LittéraleRationnelle` ou `LittéraleEntière` (si dénominateur = 1) |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle`| `LittéraleRéelle` | `LittéraleRéelle` |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle` (`LittéraleNumérique`) | `LittéraleComplexe` | `LittéraleComplexe` ou `LittéraleNumérique` (si partie imaginaire = 0) |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |

### /

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleEntière` | `LittéraleEntière` | `LittéraleEntière` ou `LittéraleRationnelle`|
| `LittéraleRationnelle` | `LittéraleRationnelle` | `LittéraleRationnelle` ou `LittéraleEntière` (si dénominateur = 1) |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle`| `LittéraleRéelle` | `LittéraleRéelle` |
| `LittéraleEntière` ou `LittéraleRationnelle` ou `LittéraleRéelle` (`LittéraleNumérique`) | `LittéraleComplexe` | `LittéraleComplexe` ou `LittéraleNumérique` (si partie imaginaire = 0) |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |


### DIV

Provoque une erreur sur `LittéraleRationnelle`, `LittéraleRéelle` ou `LittéraleComplexe` ?

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleEntière` | `LittéraleEntière` | `LittéraleEntière` |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |

### MOD

Provoque une erreur sur `LittéraleRationnelle`, `LittéraleRéelle` ou `LittéraleComplexe` ?

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleEntière` | `LittéraleEntière` | `LittéraleEntière` |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |

### POW

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleNumérique` ou `LittéraleComplexe` |  `LittéraleNumérique` | `LittéraleNumérique` ou `LittéraleComplexe` |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |

### NEG

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleNumérique` ou `LittéraleComplexe` |
| `LittéraleExpression` | `LittéraleExpression` |

### SIN, ARCSIN, COS, ARCCOS, TAN, ARCTAN (radian)

On va oublier la trigonométrie complexe, ça part en sinus hyperboliques etc.

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleNumérique` | `LittéraleNumérique` |
| `LittéraleExpression` | `LittéraleExpression` |

### SQRT

On va commencer sans implémenter le calcul d'une racine carrée d'un nombre complexe.
Une racine négative renvoie un nombre complexe.

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleNumérique` | `LittéraleNumérique` ou `LittéraleComplexe` |
| `LittéraleExpression` | `LittéraleExpression` |

### EXP

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleNumérique` ou `LittéraleComplexe` |
| `LittéraleExpression` | `LittéraleExpression` |

### LN 

Il s'agit par définition du logarithme naturelle, donc réel. On ne se préoccupe pas de l'implémentation complexe.

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleNumérique` | `LittéraleNumérique` |
| `LittéraleExpression` | `LittéraleExpression` |

### NUM

Provoque une erreur sur `LittéraleRéelle` ou `LittéraleComplexe`.

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleEntière` ou `LittéraleRationnelle` | `LittéraleEntière` |
| `LittéraleExpression` | `LittéraleExpression` |

### DEN

Provoque une erreur sur `LittéraleRéelle` ou `LittéraleComplexe`.

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleEntière` ou `LittéraleRationnelle` | `LittéraleEntière` |
| `LittéraleExpression` | `LittéraleExpression` |

### $

| Opérande 1 | Opérande 2 | Sortie |
|:----------:|:----------:|:------:|
| `LittéraleNumérique` |  `LittéraleNumérique` | `LittéraleComplexe` |
| `LittéraleExpression` | `LittéraleExpression` | `LittéraleExpression` |
| `LittéraleExpression` | `LittéraleNumérique` ou `LittéraleComplexe` | `LittéraleExpression` |

### RE, IM, ARG, NORM

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleComplexe` ou `LittéraleNumérique` | `LittéraleNumérique` |
| `LittéraleExpression` | `LittéraleExpression` |

### Opérateurs logiques

| Opérande | Sortie |
|:--------:|:------:|
| `LittéraleComplexe` ou `LittéraleNumérique` | `LittéraleEntière` (0 ou 1) |
| `LittéraleExpression` | `LittéraleExpression` |

## Design Pattern

On utilise le design pattern Adapter (en objet serait mieux) pour réutiliser les classes QStack et QVector pour la pile et la/les factorie.
Design pattern Factory Method.
Peut-être Composite aussi.
