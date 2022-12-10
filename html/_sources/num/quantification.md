(P:quantification)=
# Quantification

La quantification (_quantization_) consiste à transformer un signal à valeurs continues en un signal à valeurs discrètes.
Ces valeurs discrètes correspondent à des « niveaux de quantification ».
En pratique, elles sont représentées par un code binaire,
c'est pourquoi le nombre de niveaux de quantification est souvent une puissance de deux.

## Principe

La « quantification uniforme par arrondi » est la méthode la plus plus simple : les niveaux de quantification sont répartis uniformément et distants de la même valeur $q$ (appelée « pas de quantification »).
Les valeurs que prend le signal non quantifié $x(t)$ sont arrondies au niveau de quantification le plus proche :

$$
x_q(t) = q \times \left\lfloor \frac{x(t)}{q}+\frac{1}{2} \right\rfloor
$$

où $\lfloor\cdot\rfloor$ est la [partie entière](https://www.bibmath.net/dico/index.php?action=affiche&quoi=./p/partieentiere.html).

La {numref}`F:quantification:signal` représente un exemple de quantification uniforme par arrondi pour $K=8$ niveaux de quantification et $q=0,3$.

```{figure} quantification-signal.svg
---
width: 700px
name: F:quantification:signal
---
Exemple de quantification d'un signal $x(t)$ sur $K=8$ niveaux.
```

La « caractéristique de quantification » illustre la quantification utilisée.
C'est la courbe représentant $x_q$ en fonction de $x$, elle a donc la forme d'une fonction en escalier ({numref}`F:quantification:caracteristique`).

```{figure} quantification-caracteristique.svg
---
width: 400px
name: F:quantification:caracteristique
---
Caractéristique de quantification d'une quantification uniforme par arrondi sur $K=8$ niveaux.
```

Le choix du niveau de quantification $q$ doit être déterminé en fonction de la dynamique du signal
qui est la différence entre ses valeurs extrêmes $x_\mathrm{min}$ et $x_\mathrm{max}$.
Puisqu'une quantification sur $K$ niveaux correspond à une amplitude maximale de $(K-1)q$,
alors le pas de quantification est égale à :

$$
q = \frac{x_\mathrm{max}-x_\mathrm{min}}{K-1}.
$$

Dans le cas où $q$ est plus petit que le deuxième membre de cette équation,
on les amplitudes extrêmes du signal seront mal quantifiées, comme c'est le cas dans l'exemple de la {numref}`F:quantification:signal`.


## Erreur de quantification

On a vu que l'[échantillonnage](P:Echantillonnage) n'introduisait aucune erreur
(à condition de respecter la condition $f_e > 2 f_\mathrm{max}$).
Ce n'est pas le cas pour la quantification :
elle engendre une erreur puisque le signal quantifié $x_q$ n'a pas les mêmes valeurs que le signal non quantifié $x$.
La différence $\varepsilon(t) = x(t) - x_q(t)$ est appelée « erreur de quantification » (cf. {numref}`F:quantification-erreur`).

```{figure} quantification-erreur.svg
---
width: 700px
name: F:quantification-erreur
---
Erreur de quantification sur l'exemple précédent (en rouge).
La zone en rouge pâle correspond à l'erreur maximale théorique.
L'erreur dépasse cette zone autour de 0,4 et 0,8 car le pas de quantification est mal défini par rapport à la dynamique du signal.
```

Dans le cas où $q$ est correctement défini, la valeur maximale de cette erreur est la moitié du pas de quantification : $q/2$.
Sa moyenne est (statistiquement) nulle et sa puissance est (statistiquement) égale à $q^2/12$ (dans l'hypothèse d'un signal $x(t)$ distribué uniformément).


## Qantification non uniforme

Dans certaines applications, le signal présente rarement de grandes amplitudes mais il est souvent d'amplitude faible.
C'est le cas par exemple des signaux de parole.
Aussi, il est intéressant d'avoir une quantification où le pas de quantification est différent dans les faibles et les grandes amplitudes.
Plus précisément, on privilégiera un pas de quantification faible pour les faibles amplitudes et grand pour les grandes amplitudes.
Cela aboutit à une quantification non uniforme.

Par exemple, l'application d'une transformation non linéaire sur le signal avant une quantification uniforme
correspond à une quantification non uniforme.
En téléphonie, la « loi A » permet d'obtenir la quantification représentée {numref}`F:quantification:caracteristique-A`.

```{figure} quantification-caracteristique-A.svg
---
width: 400px
name: F:quantification:caracteristique-A
---
Caractéristique de quantification d'une quantification uniforme par arrondi sur $N=8$ niveaux.
```

