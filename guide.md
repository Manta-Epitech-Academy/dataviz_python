# Aide-mémoire Pandas — Visualisation de données

---

## 1. Filtrer des lignes (condition unique)

Utilisez l'indexation booléenne pour filtrer un DataFrame selon une seule condition.

```python
df[(df.medal == "gold")]
```

Cela renvoie uniquement les lignes où la colonne `medal` vaut `"gold"`.

![Filtrage avec une condition unique](img/Slide1.jpg)

---

## 2. Filtrer des lignes (conditions multiples)

Combinez plusieurs conditions avec `&` (ET). Chaque condition doit être entourée de parenthèses.

```python
df[(df.year == 2002) & (df.medal == "gold") & (df.sport == "snowboard")]
```

Cela renvoie les lignes correspondant à **toutes** les conditions simultanément.

![Filtrage avec conditions multiples](img/Slide2.jpg)

---

## 3. Regrouper les données avec `groupby()`

`groupby()` découpe le DataFrame en groupes basés sur les valeurs d'une ou plusieurs colonnes.

```python
df.groupby("year")
```

Chaque groupe est comme un « sac » de lignes partageant la même valeur pour la colonne regroupée.

![Concept du GroupBy](img/Slide3.jpg)

---

## 4. Agréger les groupes avec `size()`

Après le regroupement, appliquez une fonction d'agrégation comme `.size()` pour compter le nombre de lignes dans chaque groupe.

```python
df.groupby("year").size()
```

Cela renvoie une Series avec les clés de groupe en index et les comptages en valeurs.

![GroupBy avec agrégation size](img/Slide4.jpg)

---

## 5. Tracer un diagramme en barres

Stockez le résultat agrégé et appelez `.plot(kind="bar")` pour le visualiser.

```python
gold_per_year = df.groupby("year").size()
gold_per_year.plot(kind="bar")
```

Cela produit un diagramme en barres avec les clés de groupe sur l'axe des x et les comptages sur l'axe des y.

![Tracé d'un diagramme en barres](img/Slide5.jpg)

---

## 6. Trier les valeurs

Utilisez `.sort_values()` pour trier une Series par ses valeurs, rendant les graphiques plus lisibles.

```python
medal_per_country_sorted = medal_per_country.sort_values()
```

| Non trié | Trié |
|----------|------|
| `medal_per_country.plot()` | `medal_per_country_sorted.plot()` |

Le tri ordonne les barres de la plus petite à la plus grande, révélant le classement d'un coup d'œil.

![Tri des valeurs pour une meilleure visualisation](img/Slide6.jpg)
