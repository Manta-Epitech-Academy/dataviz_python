# Introduction

## Contexte

Vous devez répondre à la question : Est-ce que les pays obtiennent plus de médailles quand ils organisent les Jeux Olympiques d'hiver ?

Pour cela vous avez à votre disposition un jeu de données comportant l'ensemble des médailles obtenues aux JO d'hiver depuis la première édition en 1924 jusqu'à l'édition de 2010.

## Ce que vous allez faire durant cet atelier

En utilisant le language Python et des outils d'analyse de données vous allez tenter de répondre à la question posée en introduction.

## Prise en main de l'environement Jupyter Notebook

Rendez-vous sur [Jupyter.org](https://jupyter.org/try-jupyter/lab/index.html)

Jupyter Notebook est un environnement interactif qui permet de créer et d'exécuter des documents combinant code, texte explicatif, formules mathématiques et visualisations (graphiques).

Il est très utilisé en data science, en apprentissage automatique et enseignement, notamment avec Python.

- **Créer un nouveau notebook** : *New → Notebook* puis sélectionner le kernel **Python (Pyodide)**
- **Uploader le fichier CSV** : *Upload* → sélectionner `winter_olympics_medals.csv` → valider

![intro_jupyter](img/dataviz_intro.gif)

## ⚡ Expérimentation ⚡: 

- **Bloc de Markdown** :

Le Markdown est un langage de balisage simple qui permet de mettre en forme du texte facilement.

Ajoutez un bloc de Markdown à votre notebook.
```markdown
# Les pays obtiennent-ils plus de médailles quand ils organisent les JO d'hiver ?
```
La combinaison `Ctrl+Entrée` vous permet d'afficher le rendu de votre Markdown.

### 💡 Astuce 💡:
- Une ligne commencent par ```# ``` en Markdown permet de déclarer un titre

- **Bloc de code (Python)** :

Entrez votre premier bloc de code python dans votre notebook.

```python
print("Hello, world!")
21 * 2
```

La combinaison `Ctrl+Entrée` vous permet d'éxécuter votre bloc de code.

### 💡 Astuce 💡:
- Le resultat de la dernière expression entrée dans un bloc de code (ici `21 * 2`) de votre notebook est automatiquement affichée (si possible) après le bloc de code

# Lecture du CSV

Lors de l'étape précédente vous avez uploadé le fichier CSV fourni sur votre environemment Jupyter.

Un fichier CSV est fichier texte qui stocke des données sous forme de tableau.
Chaque ligne du CSV correspond à une ligne de données, chaque valeur est séparée par une virgule.

![csv](img/csv.png)

Nous allons utiliser la bibliothèque **Pandas** pour lire, organiser et analyser ces données. L'utilisation d'une bibliothèque telle que **Pandas** permet de nous faciliter le travail sur des tableaux de données.

## ⚡ Expérimentation ⚡ :

Dans un bloc de code:
- importez la bibliothèque **Pandas**
- utilisez **Pandas** pour lire le fichier CSV dans un **DataFrame** (df)

---
```python
import pandas as pd

df = pd.read_csv("winter_olympics_medals.csv")
df
```

| | id | year | sport | medal | country | pays | host |
|---|---|---|---|---|---|---|---|
| 0 | 31666 | 1924 | biathlon | gold | SUI | Switzerland | False |
| 1 | 31666 | 1924 | biathlon | silver | FIN | Finland | False |
| 2 | 31666 | 1924 | biathlon | bronze | FRA | France | True |
| 3 | 31666 | 1960 | biathlon | gold | SWE | Sweden | False |
| 4 | 31666 | 1960 | biathlon | silver | FIN | Finland | False |
| ... | ... | ... | ... | ... | ... | ... | ... |
| 2566 | 32514 | 2010 | snowboard | silver | RUS | Russian Federation | False |
| 2567 | 32514 | 2010 | snowboard | bronze | AUT | Austria | False |
| 2568 | 32514 | 2010 | snowboard | gold | CAN | Canada | True |
| 2569 | 32514 | 2010 | snowboard | silver | FRA | France | False |
| 2570 | 32514 | 2010 | snowboard | bronze | SUI | Switzerland | False |

2571 rows × 7 columns

---

Un DataFrame est la structure de données principale de pandas.
Elle ressemble à un tableau Excel avec des lignes et des colonnes, et permet de filtrer, trier et analyser les données facilement.


Prenez le temps d'observer les données présentes dans le DataFrame: 
- Le nombre de lignes
- Le nom des colonnes et les données qu'elles contiennent
- La colonne `host` qui indique si le pays a organisé les Jeux Olympiques cette année-là

# Filtrer les données

Pour la première étape de notre analyse nous allons filtrer nos données.

Par exemple, dans un nouveau bloc de code: pour extraire uniquement les médailles d'or de notre jeu de données:

```python
data = df[df.medal == "gold"]
data
```

![filtre1](img/Slide1.jpg)

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  Essayez d'extraire toutes les médailles obtenues par la France dans notre jeu de données.

- **Bloc de Markdown** :  
  Rédigez une brève description des données que vous venez de filtrer.

💡 Astuce 💡:

- Utilisez `Ctrl+Entrée` pour exécuter chaque bloc (code ou Markdown) et afficher le résultat ou le rendu du texte.

# Regrouper les données

Il est possible de regrouper les données d'un DataFrame selon une caractéristique, puis appliquer un calcul sur chaque groupe

Par exemple pour regrouper les médailles par année d'obtention:

![groupby1](img/Slide3.jpg)

Il est ensuite possible ensuite d'appliquer un calcul sur chacun des groupes: ici on récupère leur taille.


![groupby2](img/Slide4.jpg)

💡 Astuce 💡 :

`.reset_index(name="xxx")` permet de réinitialiser l'index d'une série/groupement en DataFrame tout en donnant le nom "xxx" à la nouvelle colonne contenant les valeurs.

## ⚡ Expérimentation ⚡:

- **Bloc de code**:
  Regroupez les médailles obtenues par la France par année. Comptez le nombre de médailles obtenues chaque année. Votre nouvelle colone devrait s'appeller `medal_count`.

- **Bloc de Markdown** :  
  Rédigez une courte réponse à la question suivante:
  - Quel est nombre de médailles remportées par la France en 1968 et en 1992 ?
    
# Premier graphique

Nous pouvons créer un graphique pour visualiser les données en utilisant **matplotlib**.

Commencez par importer **matplotlib** dans votre notebook.

```python
import matplotlib.pyplot as plt
```

Par exemple, pour visualiser le nombre de médailles obtenues par la France par année (étape précédente):

```python

medals_fr = df[df.country == "FRA"]

data = medals_fr.groupby('year').size().reset_index(name="medals_count")

print(data)

plt.bar(data.year.astype(str), data.medals_count)
plt.xticks(rotation=90)
plt.xlabel('Année')
plt.ylabel('Nombre de médailles')
plt.title('Nombre de médailles par année')
plt.show()

```

## TODO: broken link
![med_france_year](img/med_year_fra.png)


## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Ajoutez le code nécessaire pour afficher un graphe (exemple ci-dessus) montrant le nombre de médailles obtenues par la France à chaque JO d'hiver.
  - Vous pouvez ensuite tenter de personnaliser votre graphe.

- **Explications** :
  Pouvez-vous expliquer chaque ligne de code  de l'exemple précédent ?


💡 Astuce 💡 : 

- Un graphique peut être personnalisé avec les fonctions de matplotlib. Le type du graphique peut être modifié en utilisant différentes fonctions:
  - `plt.plot()` : ligne
  - `plt.bar()` : barres verticales
  - `plt.barh()` : barres horizontales
  - `plt.scatter()` : nuage de points
  - etc.

- La couleur peut être spécifiée avec le paramètre `color`
  - 'r' : rouge
  - 'g' : vert
  - 'b' : bleu
  - '#xxyyzz' : code couleur hexadécimal [https://www.color-name.com/search/blue](https://www.color-name.com/search/blue)
  - etc.

Par exemple:
```
...
plt.plot(data.year.astype(str), data.medals_count, color="r")
```

Vous donnera un graphique avec une apparence différente.


# Evaluer les perfomances des différents pays

Nous avons : une table contenant pour chaque médaille le pays, l'année et le statut d'organisateur.

Nous voulons : comparer les performances de chaque pays selon qu'il organise les Jeux ou non.

## Étape 1 : Regrouper par pays, année et statut d'organisateur

Pour commencer, nous allons regrouper les données pour compter le nombre de médailles pour chaque combinaison (pays, année, statut d'organisateur).

Par exemple, supposons que nous avons un DataFrame `ventes` avec les ventes de produits par magasin et par mois (chaque ligne représente une transaction) :

| produit | magasin | mois | quantite |
|---------|---------|------|----------|
| Laptop  | Paris   | Jan  | 1        |
| Laptop  | Paris   | Jan  | 1        |
| Laptop  | Paris   | Jan  | 1        |
| Laptop  | Paris   | Fév  | 1        |
| Laptop  | Paris   | Fév  | 1        |
| Laptop  | Lyon    | Jan  | 1        |
| Laptop  | Lyon    | Jan  | 1        |
| Laptop  | Lyon    | Fév  | 1        |
| Souris  | Paris   | Jan  | 1        |
| Souris  | Paris   | Jan  | 1        |
| Souris  | Paris   | Fév  | 1        |
| Souris  | Paris   | Fév  | 1        |
| Souris  | Paris   | Fév  | 1        |
| Souris  | Lyon    | Jan  | 1        |
| Souris  | Lyon    | Fév  | 1        |
| Souris  | Lyon    | Fév  | 1        |

Pour regrouper et compter le nombre de transactions (ventes) par produit, magasin et mois :

```python
# Exemple : regrouper par produit, magasin et mois
ventes_group = ventes.groupby(['produit', 'magasin', 'mois']).size().reset_index(name="nombre_ventes")
print(ventes_group)
```

**Résultat :**

| produit | magasin | mois | nombre_ventes |
|---------|---------|------|---------------|
| Laptop  | Lyon    | Fév  | 1             |
| Laptop  | Lyon    | Jan  | 2             |
| Laptop  | Paris   | Fév  | 2             |
| Laptop  | Paris   | Jan  | 3             |
| Souris  | Lyon    | Fév  | 2             |
| Souris  | Lyon    | Jan  | 1             |
| Souris  | Paris   | Fév  | 3             |
| Souris  | Paris   | Jan  | 2             |

💡 Astuce 💡:
- Il est possible d'utiliser `.groupby()` sur plusieurs colonnes: ```.groupby(['col1', 'col2', 'col3'])```
- L'ordre des colonnes est important:
  - ```.groupby(['produit', 'magasin', 'mois']).size()``` donne une information différente de ```.groupby(['mois', 'produit', 'magasin']).size()```

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- Regroupez les données par `country`, `host` et `year` et comptez le nombre de médailles pour chaque groupe
- Utilisez `.reset_index(name="medals")` pour transformer le résultat en DataFrame avec une colonne nommée "medals"

Prenez le temps d'observer le résultat : vous devriez voir pour chaque pays, chaque année, et chaque statut d'organisateur, le nombre de médailles obtenues.

## Étape 2 : Calculer la moyenne par pays et statut d'organisateur

Maintenant que nous avons le nombre de médailles par année pour chaque pays (quand il organise ou non), nous pouvons calculer la moyenne de médailles pour chaque pays selon son statut d'organisateur.

Par exemple, supposons que nous avons un DataFrame `notes_etudiants` avec les notes de plusieurs étudiants :

| etudiant | matiere   | note |
|----------|-----------|------|
| Alice    | Math      | 15   |
| Alice    | Français  | 12   |
| Alice    | Anglais   | 14   |
| Bob      | Math      | 18   |
| Bob      | Français  | 16   |
| Bob      | Anglais   | 17   |
| Claire   | Math      | 13   |
| Claire   | Français  | 11   |
| Claire   | Anglais   | 15   |

Pour calculer la moyenne de notes par étudiant :

```python
# Exemple : calculer la moyenne de notes par étudiant
moyennes = notes_etudiants.groupby('etudiant')['note'].mean().reset_index(name="moyenne")
print(moyennes)
```

**Résultat :**

| etudiant | moyenne |
|----------|---------|
| Alice    | 13.67   |
| Bob      | 17.00   |
| Claire   | 13.00   |

Ce code calcule la moyenne de notes pour chaque étudiant en regroupant toutes les matières.

💡 Astuce 💡:
- Après un `.groupby()`, vous pouvez appliquer différentes fonctions comme `.mean()`, `.sum()`, `.max()`, etc.
- Par exemple : `group.groupby(['country', 'host'])['medals'].mean()` calcule la moyenne de la colonne 'medals' pour chaque groupe (pays, statut)

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- À partir du DataFrame `group` créé à l'étape précédente, regroupez par `country` et `host`
- Calculez la moyenne de la colonne `medals` pour chaque groupe
- Utilisez `.reset_index(name="average")` pour transformer le résultat en DataFrame

Observez le résultat : vous devriez voir pour chaque pays deux lignes (une où `host` est `True`, une où `host` est `False`) avec la moyenne de médailles dans chaque cas.

# Réorganiser les données avec pivot_table

Actuellement, nos données sont organisées avec une ligne par pays et statut d'organisateur. Pour comparer facilement les performances, il serait plus pratique d'avoir une ligne par pays avec deux colonnes : une pour la moyenne quand le pays organise, une pour la moyenne quand il n'organise pas.

La méthode `.pivot_table()` permet de transformer nos données pour avoir les valeurs de `host` (True/False) en colonnes séparées.

## Comprendre pivot_table

Avant d'utiliser `.pivot_table()`, regardons un exemple simple avec les notes d'étudiants par semestre :

Supposons que nous avons un DataFrame `notes_semestre` avec les notes moyennes des étudiants par semestre :

| etudiant | semestre | moyenne |
|----------|----------|---------|
| Alice    | S1       | 14.5    |
| Alice    | S2       | 15.0    |
| Bob      | S1       | 16.0    |
| Bob      | S2       | 17.5    |
| Claire   | S1       | 12.0    |
| Claire   | S2       | 13.5    |

Pour réorganiser ces données avec les semestres en colonnes :

```python
# Exemple : pivot_table avec etudiant et semestre
pivot_notes = notes_semestre.pivot_table(
    index='etudiant',
    columns='semestre',
    values='moyenne'
).reset_index()
print(pivot_notes)
```

**Résultat :**

| etudiant | S1   | S2   |
|----------|------|------|
| Alice    | 14.5 | 15.0 |
| Bob      | 16.0 | 17.5 |
| Claire   | 12.0 | 13.5 |

💡 Astuce 💡:
- `index='etudiant'` : les étudiants deviennent les lignes
- `columns='semestre'` : les valeurs de semestre (S1, S2) deviennent les colonnes
- `values='moyenne'` : les valeurs à placer dans le tableau sont les moyennes

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- Utilisez `.pivot_table()` sur votre DataFrame `avg` pour réorganiser les données avec `country` en lignes et `host` en colonnes
- Utilisez `.reset_index()` pour transformer le résultat en DataFrame normal
- Renommez les colonnes pour plus de clarté : `['country', 'avg_ext', 'avg_dom']` (extérieur/domicile)

💡 Astuce 💡:
- Les colonnes True/False peuvent être dans un ordre différent selon vos données
- Vérifiez l'ordre avec `pivot.columns` avant de renommer

## Filtrer les pays avec les deux types de données

Certains pays n'ont peut-être jamais organisé les Jeux (pas de ligne avec `host=True`) ou n'ont jamais participé sans organiser (pas de ligne avec `host=False`). Pour faire une comparaison valide, nous devons ne garder que les pays qui ont les deux types de données.

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- Utilisez `.dropna()` sur votre DataFrame `pivot` pour ne garder que les pays qui ont les deux types de données (pas de valeurs manquantes)

Dans un nouveau bloc de Markdown:
- Expliquez pourquoi il est important de ne garder que les pays qui ont les deux types de données pour faire une comparaison valide


# Calculer le pourcentage d'amélioration

Maintenant que nous avons les moyennes de médailles pour chaque pays quand il organise (`avg_dom`) et quand il n'organise pas (`avg_ext`), nous pouvons calculer le pourcentage d'amélioration (ou de diminution).

## La formule

La formule pour calculer le pourcentage d'amélioration est :

```
pourcentage = ((moyenne_domicile - moyenne_extérieur) / moyenne_extérieur) × 100
```

- Si le résultat est **positif** : le pays obtient plus de médailles quand il organise
- Si le résultat est **négatif** : le pays obtient moins de médailles quand il organise

**Exemple avec un calcul simple :**
- Si un pays a une moyenne de 10 médailles en extérieur et 15 médailles à domicile
- Pourcentage = ((15 - 10) / 10) × 100 = 50%
- Ce pays obtient 50% de médailles en plus quand il organise !

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- Créez une nouvelle colonne `boost` dans votre DataFrame `pivot` avec la formule du pourcentage d'amélioration
- Utilisez la même logique que dans l'exemple ci-dessus, mais avec vos colonnes `avg_dom` et `avg_ext`
- Affichez le résultat

## Trier les résultats

Pour mieux visualiser quels pays s'améliorent le plus (ou le moins), nous pouvons trier les données.

💡 Astuce 💡:
- `.sort_values('nom_colonne', ascending=True)` : tri croissant (du plus petit au plus grand)
- `.sort_values('nom_colonne', ascending=False)` : tri décroissant (du plus grand au plus petit)

![sort](img/Slide6.jpg)

Par exemple, pour trier les sports par nombre de médailles décroissant :

```python
# Exemple : trier par nombre de médailles
sorted_sports = pivot_example.sort_values('gold', ascending=False)
sorted_sports.head()
```

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- Triez votre DataFrame `pivot` par la colonne `boost` en ordre croissant avec `.sort_values('boost', ascending=True)`
- Affichez le résultat

Dans un nouveau bloc de Markdown:
- Interprétez les résultats : 
  - Quels pays s'améliorent le plus quand ils organisent les Jeux ?
  - Quels pays s'aggravent quand ils organisent les Jeux ?
  - Que pouvez-vous conclure ?



# Visualiser les résultats

Maintenant que nous avons calculé le pourcentage d'amélioration, visualisons ces résultats avec un graphique en utilisant matplotlib.

## Créer un graphique en barres horizontales

Un graphique en barres horizontales est idéal pour comparer plusieurs pays. Nous allons utiliser `plt.barh()`.

Par exemple, pour créer un graphique en barres horizontales montrant le nombre de médailles d'or par sport :

```python
# Exemple : graphique en barres horizontales
plt.barh(pivot_example.sport, pivot_example.gold)
plt.xlabel('Nombre de médailles d\'or')
plt.ylabel('Sport')
plt.title('Médailles d\'or par sport')
plt.show()
```

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- Créez un graphique en barres horizontales avec `plt.barh()` montrant le pourcentage d'amélioration pour chaque pays
- Utilisez `pivot.country` pour les labels (axe y) et `pivot.boost` pour les valeurs (axe x)
- Ajoutez des titres et labels pour les axes avec `plt.xlabel()`, `plt.ylabel()` et `plt.title()`

## Ajouter des couleurs conditionnelles

Pour rendre le graphique plus lisible, nous pouvons utiliser des couleurs différentes selon que le pourcentage est positif (vert) ou négatif (rouge).

Par exemple, pour colorer les barres selon une condition :

```python
# Exemple : couleurs conditionnelles avec une liste simple
colors_example = ["b" if x > 30 else "r" for x in pivot_example.gold]
plt.barh(pivot_example.sport, pivot_example.gold, color=colors_example)
plt.show()
```

💡 Astuce 💡:
- Vous pouvez créer une liste de couleurs en utilisant une **compréhension de liste** (list comprehension)
- Syntaxe : `[couleur1 if condition else couleur2 for valeur in liste]`
- Exemple : `["g" if boost > 0 else "r" for boost in pivot.boost]` crée une liste avec "g" (vert) si boost > 0, sinon "r" (rouge)

## ⚡ Expérimentation ⚡ :

Dans un nouveau bloc de code:
- Créez une liste de couleurs en utilisant une compréhension de liste : vert ("g") si boost >= 0, rouge ("r") sinon
- Utilisez cette liste avec le paramètre `color=` dans `plt.barh()`
- Ajoutez les labels et le titre comme précédemment


# 9: Comparaison des moyennes

Nous pouvons améliorer notre visualisation en créant un graphique comparatif qui montre à la fois les moyennes de médailles quand le pays organise et quand il n'organise pas.

Nous pouvons améliorer ce graphique en triant au préalable nos données.


![sort](img/Slide6.jpg)


**Astuce**: il est possible de choisir l'ordre de tri (croissant ou décroissant) renseignant le paramètre `ascending=`  à `.sort_values`:

- True: tri dans l'ordre croissant
- False: tri dans l'ordre décroissant

## Exercice:

Dans un nouveau bloc de code:
- Créez un graphique comparatif avec deux séries de barres horizontales côte à côte en utilisant matplotlib
- Une série pour les moyennes quand le pays n'organise pas (avg_non_host)
- Une série pour les moyennes quand le pays organise (avg_host)
- Utilisez `plt.barh()` avec des positions ajustées pour créer les barres côte à côte
- Trier les pays par pourcentage d'amélioration avant de créer le graphique avec `.sort_values()`







