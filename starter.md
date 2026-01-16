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
df_medailles_or = df[df.medal == "gold"]
df_medailles_or
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

df_medailles_france = df[df.country == "FRA"]

df_france_par_annee = df_medailles_france.groupby('year').size().reset_index(name="medals_count")

print(df_france_par_annee)

plt.bar(df_france_par_annee.year.astype(str), df_france_par_annee.medals_count)
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
plt.plot(df_france_par_annee.year.astype(str), df_france_par_annee.medals_count, color="r")
```

Vous donnera un graphique avec une apparence différente.


# Trier des données avec pandas

Nous voulons ici savoir quels sont les pays ayant obtenu le plus de médailles dans l'histoire des JO d'hiver. Pour cela il va falloir trier les pays par nombre de médailles.

La méthode `sort_values()` de pandas permet de trier facilement un DataFrame selon une ou plusieurs colonnes.  
- Si vous souhaitez trier les lignes par ordre croissant ou décroissant d’une colonne, il suffit d’indiquer le nom de la colonne avec le paramètre `by`.
- Le paramètre `ascending` permet de choisir entre l’ordre croissant (`True`, par défaut) ou décroissant (`False`).
- Il est aussi possible de trier selon plusieurs colonnes en passant une liste de noms de colonnes.


## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Triez les pays par nombre de médaille obtenue
  - Affichez le graphique correspondant


# Top 5

Nous voulons garder que le Top 5 des pays en nombre de médaille obtenue aux JO d'hiver.

Il est possible de récupérer les `N` premiers elements d'un DataFrame avec la méthode `.head(N)`, si votre DataFrame est déjà trié par ordre décroissant celà revient à faire un "Top N" 

💡 Astuce 💡:
- Dans cet exemple, on suppose que votre DataFrame trié s'appelle `classement_pays` (classement des pays par nombre de médailles).


➡️ Après avoir utilisé `.head(3)`, vous aurez un DataFrame contenant uniquement les 3 premières lignes du tableau, dans l'ordre d'origine.

### Exemple visuel

Avant `head(3)` :  

| artiste        | ecoutes |
|----------------|---------|
| Jul            | 350     |
| Aya Nakamura   | 320     |
| Orelsan        | 280     |
| Stromae        | 230     |
| PNL            | 220     |
| Angèle         | 189     |

Après `classement_artistes.head(3)` :  

| artiste      | ecoutes |
|--------------|---------|
| Jul          | 350     |
| Aya Nakamura | 320     |
| Orelsan      | 280     |


## ⚡ Expérimentation ⚡

Dans un nouveau bloc de code :
- Utilisez simplement `.head(5)` sur votre DataFrame déjà trié du step précédent pour obtenir le top 5.
- Affichez ensuite le graphique correspondant (par exemple un barplot avec matplotlib ou pandas plotting) sur ce top 5 uniquement.

---

# Fin du starter


---






# Evaluer les perfomances des différents pays

Nous avons : une table contenant pour chaque médaille le pays, l'année et le statut d'organisateur.

Nous voulons : comparer les performances de chaque pays selon qu'il organise les Jeux ou non.

## Étape 1 : Regrouper par pays, année et statut d'organisateur

### Explication

Pour commencer, nous allons regrouper les données pour compter le nombre de médailles pour chaque combinaison (pays, année, statut d'organisateur).

**Exemple avec des ventes de produits :**

Supposons que nous avons un DataFrame `ventes` avec les ventes de produits par magasin et par mois (chaque ligne représente une transaction) :

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

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Regroupez les données par `country`, `host` et `year` et comptez le nombre de médailles pour chaque groupe
- Utilisez `.reset_index(name="medals")` pour transformer le résultat en DataFrame avec une colonne nommée "medals"

Prenez le temps d'observer le résultat : vous devriez voir pour chaque pays, chaque année, et chaque statut d'organisateur, le nombre de médailles obtenues.

## Étape 2 : Calculer la moyenne par pays et statut d'organisateur

### Explication

Maintenant que nous avons le nombre de médailles par année pour chaque pays (quand il organise ou non), nous pouvons calculer la moyenne de médailles pour chaque pays selon son statut d'organisateur.

**Exemple avec des notes d'étudiants :**

Supposons que nous avons un DataFrame `notes_etudiants` avec les notes de plusieurs étudiants :

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
- Par exemple : `df_medailles_par_pays_hote_annee.groupby(['country', 'host'])['medals'].mean()` calcule la moyenne de la colonne 'medals' pour chaque groupe (pays, statut)

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- À partir du DataFrame `df_medailles_par_pays_hote_annee` créé à l'étape précédente, regroupez par `country` et `host`
- Calculez la moyenne de la colonne `medals` pour chaque groupe
- Utilisez `.reset_index(name="average")` pour transformer le résultat en DataFrame

Observez le résultat : vous devriez voir pour chaque pays deux lignes (une où `host` est `True`, une où `host` est `False`) avec la moyenne de médailles dans chaque cas.

## Étape 3 : Calculer le nombre de participations

### Explication

💡 **Important** : Pour comparer équitablement les performances, il est essentiel de tenir compte du nombre de données disponibles. 

**Exemple avec des notes d'étudiants :**

Supposons que nous voulons comparer les moyennes de notes entre deux étudiants :
- Alice a eu 3 notes : 15, 12, 14 → moyenne = 13.67
- Bob a eu 1 seule note : 18 → moyenne = 18.00

La moyenne de Bob semble meilleure, mais elle est basée sur une seule note ! La moyenne d'Alice est plus fiable car elle est calculée sur plusieurs notes.

**Exemple avec des ventes :**

Supposons que nous avons des ventes de produits par magasin :

| produit | magasin | mois | ventes |
|---------|---------|------|--------|
| Laptop  | Paris   | Jan  | 10     |
| Laptop  | Paris   | Fév  | 12     |
| Laptop  | Paris   | Mar  | 8      |
| Laptop  | Lyon    | Jan  | 15     |
| Souris  | Paris   | Jan  | 5      |
| Souris  | Lyon    | Jan  | 20     |

Pour calculer le nombre de mois de données disponibles par produit et magasin :

```python
# Calculer le nombre de mois (participations) par produit et magasin
nb_mois = ventes.groupby(['produit', 'magasin']).size().reset_index(name="nb_mois")
print(nb_mois)
```

**Résultat :**

| produit | magasin | nb_mois |
|---------|---------|---------|
| Laptop  | Lyon    | 1       |
| Laptop  | Paris   | 3       |
| Souris  | Lyon    | 1       |
| Souris  | Paris   | 1       |

💡 **Pourquoi c'est important** :
- Une moyenne calculée sur 3 mois est plus fiable qu'une moyenne sur 1 mois
- Un magasin avec peu de données peut avoir une moyenne très élevée ou très basse simplement par chance
- Pour une analyse robuste, il est recommandé de filtrer les cas qui ont un nombre minimum de données (par exemple, au moins 3 mois)

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Calculez le nombre de participations pour chaque combinaison (pays, statut d'organisateur) à partir du DataFrame `df_medailles_par_pays_hote_annee`
- Utilisez `.groupby(['country', 'host']).size()` pour compter le nombre d'années
- Utilisez `.reset_index(name="nb_participations")` pour créer un DataFrame avec une colonne nommée "nb_participations"

Dans un nouveau bloc de Markdown:
- Expliquez pourquoi il est important de considérer le nombre de participations lors de la comparaison des performances
- Proposez un seuil minimum de participations (par exemple, 3) pour considérer qu'une moyenne est fiable

## Étape 4 : Fusionner les données de moyenne et de participations

### Explication

Maintenant, fusionnons les données de moyenne avec les données de nombre de participations pour avoir une vue complète.

**Exemple avec des notes d'étudiants :**

Supposons que nous avons deux DataFrames :
- `moyennes` : contient les moyennes par étudiant
- `nb_notes` : contient le nombre de notes par étudiant

| etudiant | moyenne |
|----------|---------|
| Alice    | 13.67   |
| Bob      | 17.00   |
| Claire   | 13.00   |

| etudiant | nb_notes |
|----------|----------|
| Alice    | 3        |
| Bob      | 1        |
| Claire   | 3        |

Pour fusionner ces deux DataFrames :

```python
# Fusionner les moyennes avec le nombre de notes
moyennes_completes = moyennes.merge(nb_notes, on='etudiant', how='left')
print(moyennes_completes)
```

**Résultat :**

| etudiant | moyenne | nb_notes |
|----------|---------|----------|
| Alice    | 13.67   | 3        |
| Bob      | 17.00   | 1        |
| Claire   | 13.00   | 3        |

💡 Astuce 💡:
- La méthode `.merge()` permet de fusionner deux DataFrames sur des colonnes communes
- `on='etudiant'` : colonne sur laquelle faire la jointure
- `how='left'` : garde toutes les lignes du DataFrame de gauche (moyennes)

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Fusionnez le DataFrame `df_moyennes_par_pays_hote` (moyennes) avec le DataFrame `df_participations_par_pays_hote` en utilisant `.merge()`
- Utilisez `on=['country', 'host']` pour faire la jointure sur ces deux colonnes
- Affichez le résultat pour voir les moyennes avec leur nombre de participations correspondant

# Réorganiser les données avec pivot_table

Actuellement, nos données sont organisées avec une ligne par pays et statut d'organisateur. Pour comparer facilement les performances, il serait plus pratique d'avoir une ligne par pays avec deux colonnes : une pour la moyenne quand le pays organise, une pour la moyenne quand il n'organise pas.

La méthode `.pivot_table()` permet de transformer nos données pour avoir les valeurs de `host` (True/False) en colonnes séparées.

## Comprendre pivot_table

### Explication

**Exemple avec des notes d'étudiants par semestre :**

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

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Utilisez `.pivot_table()` sur votre DataFrame `df_moyennes_avec_participations` pour réorganiser les données avec `country` en lignes et `host` en colonnes
- Utilisez `.reset_index()` pour transformer le résultat en DataFrame normal
- Renommez les colonnes pour plus de clarté : `['country', 'avg_ext', 'avg_dom']` (extérieur/domicile)

💡 Astuce 💡:
- Les colonnes True/False peuvent être dans un ordre différent selon vos données
- Vérifiez l'ordre avec `pivot_moyennes.columns` avant de renommer

## Filtrer les pays avec les deux types de données et un nombre minimum de participations

### Explication

**Exemple avec des notes d'étudiants :**

Supposons que nous voulons comparer les moyennes entre le premier et le deuxième semestre. Pour faire une comparaison valide, nous devons ne garder que les étudiants qui ont des notes dans les deux semestres.

De plus, pour avoir des moyennes fiables, il est recommandé de ne garder que les étudiants qui ont un nombre minimum de notes dans chaque semestre (par exemple, au moins 3 notes au S1 ET au moins 3 notes au S2).

**Exemple avec des ventes :**

Supposons que nous avons des ventes par produit et par magasin :

| produit | magasin | moyenne_ventes | nb_mois |
|---------|---------|----------------|---------|
| Laptop  | Paris   | 10.0           | 3       |
| Laptop  | Lyon    | 15.0           | 1       |
| Souris  | Paris   | 5.0            | 3       |
| Souris  | Lyon    | 20.0           | 1       |

Pour comparer les performances entre Paris et Lyon, nous devons :
1. Ne garder que les produits présents dans les deux magasins
2. Filtrer ceux qui ont au moins 3 mois de données dans chaque magasin

```python
# Filtrer les produits avec au moins 3 mois dans chaque magasin
# et présents dans les deux magasins
ventes_filtrees = ventes[
    (ventes['nb_mois'] >= 3) &  # Au moins 3 mois de données
    (ventes['moyenne_ventes'].notna())  # A une moyenne
].copy()
```

💡 **Pourquoi filtrer par nombre de données ?**
- Une moyenne calculée sur 1 ou 2 données peut être très variable et peu fiable
- En filtrant les cas avec peu de données, nous nous assurons que nos comparaisons sont basées sur des données suffisamment robustes

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Créez un pivot pour les participations à partir de `df_moyennes_avec_participations` :
  ```python
  pivot_participations = df_moyennes_avec_participations.pivot_table(
      index='country',
      columns='host',
      values='nb_participations'
  ).reset_index()
  ```
- Utilisez `.dropna()` sur votre DataFrame `pivot_moyennes` pour ne garder que les pays qui ont les deux types de données (pas de valeurs manquantes)
- Optionnel : Filtrez également les pays qui ont moins de 3 participations en extérieur ou moins de 1 participation en domicile :
  ```python
  pivot_moyennes_filtre = pivot_moyennes[
      (pivot_participations[False] >= 3) &  # Au moins 3 participations en extérieur
      (pivot_participations[True] >= 1) &   # Au moins 1 participation en domicile
      (pivot_moyennes['avg_ext'].notna()) &          # A une moyenne en extérieur
      (pivot_moyennes['avg_dom'].notna())            # A une moyenne en domicile
  ].copy()
  ```
- Comparez le nombre de pays avant et après le filtrage

Dans un nouveau bloc de Markdown:
- Expliquez pourquoi il est important de ne garder que les pays qui ont les deux types de données pour faire une comparaison valide
- Expliquez pourquoi il est également important de considérer le nombre de participations


# Calculer le pourcentage d'amélioration

Maintenant que nous avons les moyennes de médailles pour chaque pays quand il organise (`avg_dom`) et quand il n'organise pas (`avg_ext`), nous pouvons calculer le pourcentage d'amélioration (ou de diminution).

## La formule

### Explication

La formule pour calculer le pourcentage d'amélioration est :

```
pourcentage = ((valeur_finale - valeur_initiale) / valeur_initiale) × 100
```

**Exemple avec des notes d'étudiants :**

Supposons qu'un étudiant a une moyenne de 10/20 au premier semestre et 15/20 au deuxième semestre :
- Pourcentage d'amélioration = ((15 - 10) / 10) × 100 = 50%
- L'étudiant a amélioré sa moyenne de 50% !

**Exemple avec des ventes :**

Supposons qu'un magasin a vendu en moyenne 100 produits par mois l'année dernière et 150 produits par mois cette année :
- Pourcentage d'amélioration = ((150 - 100) / 100) × 100 = 50%
- Les ventes ont augmenté de 50% !

**Pour notre analyse des Jeux Olympiques :**
- Si le résultat est **positif** : le pays obtient plus de médailles quand il organise
- Si le résultat est **négatif** : le pays obtient moins de médailles quand il organise

**Exemple avec un calcul simple :**
- Si un pays a une moyenne de 10 médailles en extérieur et 15 médailles à domicile
- Pourcentage = ((15 - 10) / 10) × 100 = 50%
- Ce pays obtient 50% de médailles en plus quand il organise !

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Créez une nouvelle colonne `boost` dans votre DataFrame `pivot_moyennes` (ou `pivot_moyennes_filtre` si vous avez déjà filtré) avec la formule du pourcentage d'amélioration
- Utilisez la formule : `((avg_dom - avg_ext) / avg_ext) * 100`
- Si vous utilisez `pivot_moyennes_filtre`, le calcul du boost se fera automatiquement sur les pays filtrés
- Affichez le résultat

💡 **Note** : Si vous avez créé `pivot_moyennes_filtre` à l'étape précédente, utilisez-le pour calculer le boost. Sinon, vous pouvez calculer le boost sur `pivot_moyennes` puis filtrer ensuite.

## Trier les résultats

### Explication

Pour mieux visualiser quels éléments sont les meilleurs (ou les moins bons), nous pouvons trier les données.

**Exemple avec des notes d'étudiants :**

Supposons que nous avons un DataFrame avec les moyennes des étudiants :

| etudiant | moyenne |
|----------|---------|
| Alice    | 13.67   |
| Bob      | 17.00   |
| Claire   | 13.00   |

Pour trier par moyenne décroissante (du meilleur au moins bon) :

```python
# Exemple : trier par moyenne décroissante
etudiants_tries = notes_etudiants.sort_values('moyenne', ascending=False)
print(etudiants_tries)
```

**Résultat :**

| etudiant | moyenne |
|----------|---------|
| Bob      | 17.00   |
| Alice    | 13.67   |
| Claire   | 13.00   |

💡 Astuce 💡:
- `.sort_values('nom_colonne', ascending=True)` : tri croissant (du plus petit au plus grand)
- `.sort_values('nom_colonne', ascending=False)` : tri décroissant (du plus grand au plus petit)

![sort](img/Slide6.jpg)

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Triez votre DataFrame `pivot_moyennes_filtre` (ou `pivot_moyennes` si vous n'avez pas filtré) par la colonne `boost` en ordre croissant avec `.sort_values('boost', ascending=True)`
- Affichez le résultat

Dans un nouveau bloc de Markdown:
- Interprétez les résultats : 
  - Quels pays s'améliorent le plus quand ils organisent les Jeux ?
  - Quels pays s'aggravent quand ils organisent les Jeux ?
  - Que pouvez-vous conclure ?



# Visualiser les résultats

Maintenant que nous avons calculé le pourcentage d'amélioration, visualisons ces résultats avec un graphique en utilisant matplotlib.

## Créer un graphique en barres horizontales

### Explication

Un graphique en barres horizontales est idéal pour comparer plusieurs éléments. Nous allons utiliser `plt.barh()`.

**Exemple avec des notes d'étudiants :**

Supposons que nous avons un DataFrame avec les moyennes des étudiants :

| etudiant | moyenne |
|----------|---------|
| Alice    | 13.67   |
| Bob      | 17.00   |
| Claire   | 13.00   |

Pour créer un graphique en barres horizontales :

```python
# Exemple : graphique en barres horizontales
plt.barh(notes_etudiants.etudiant, notes_etudiants.moyenne)
plt.xlabel('Moyenne')
plt.ylabel('Étudiant')
plt.title('Moyennes des étudiants')
plt.show()
```

**Exemple avec des ventes :**

```python
# Exemple : graphique en barres horizontales pour les ventes
plt.barh(ventes.produit, ventes.total_ventes)
plt.xlabel('Total des ventes')
plt.ylabel('Produit')
plt.title('Ventes par produit')
plt.show()
```

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Créez un graphique en barres horizontales avec `plt.barh()` montrant le pourcentage d'amélioration pour chaque pays
- Utilisez `pivot_moyennes_filtre.country` (ou `pivot_moyennes.country` si vous n'avez pas filtré) pour les labels (axe y) et `pivot_moyennes_filtre.boost` pour les valeurs (axe x)
- Ajoutez des titres et labels pour les axes avec `plt.xlabel()`, `plt.ylabel()` et `plt.title()`

## Ajouter des couleurs conditionnelles

### Explication

Pour rendre le graphique plus lisible, nous pouvons utiliser des couleurs différentes selon une condition.

**Exemple avec des notes d'étudiants :**

Supposons que nous voulons colorer les barres en vert si la moyenne est >= 15, et en rouge sinon :

```python
# Exemple : couleurs conditionnelles avec une liste simple
couleurs = ["g" if x >= 15 else "r" for x in notes_etudiants.moyenne]
plt.barh(notes_etudiants.etudiant, notes_etudiants.moyenne, color=couleurs)
plt.xlabel('Moyenne')
plt.ylabel('Étudiant')
plt.title('Moyennes des étudiants')
plt.show()
```

**Exemple avec des ventes :**

Pour colorer en vert si les ventes sont > 100, sinon en rouge :

```python
couleurs = ["g" if x > 100 else "r" for x in ventes.total_ventes]
plt.barh(ventes.produit, ventes.total_ventes, color=couleurs)
plt.show()
```

💡 Astuce 💡:
- Vous pouvez créer une liste de couleurs en utilisant une **compréhension de liste** (list comprehension)
- Syntaxe : `[couleur1 if condition else couleur2 for valeur in liste]`
- Exemple : `["g" if boost > 0 else "r" for boost in pivot_moyennes_filtre.boost]` crée une liste avec "g" (vert) si boost > 0, sinon "r" (rouge)

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Créez une liste de couleurs en utilisant une compréhension de liste : vert ("g") si boost >= 0, rouge ("r") sinon
- Utilisez cette liste avec le paramètre `color=` dans `plt.barh()`
- Ajoutez les labels et le titre comme précédemment


# Comparaison des moyennes

Nous pouvons améliorer notre visualisation en créant un graphique comparatif qui montre à la fois les moyennes de médailles quand le pays organise et quand il n'organise pas.

## Créer un graphique comparatif

### Explication

Un graphique comparatif permet de visualiser deux séries de données côte à côte pour faciliter la comparaison.

**Exemple avec des notes d'étudiants par semestre :**

Supposons que nous avons les moyennes des étudiants au S1 et au S2 :

| etudiant | S1   | S2   |
|----------|------|------|
| Alice    | 14.5 | 15.0 |
| Bob      | 16.0 | 17.5 |
| Claire   | 12.0 | 13.5 |

Pour créer un graphique comparatif avec deux séries de barres côte à côte :

```python
import numpy as np

# Préparer les positions pour les barres
positions_y = np.arange(len(notes_etudiants))
largeur = 0.35  # Largeur des barres

# Créer le graphique
fig, ax = plt.subplots()
ax.barh(positions_y - largeur/2, notes_etudiants.S1, largeur, label='S1', color='blue')
ax.barh(positions_y + largeur/2, notes_etudiants.S2, largeur, label='S2', color='green')

# Configurer les axes
ax.set_yticks(positions_y)
ax.set_yticklabels(notes_etudiants.etudiant)
ax.set_xlabel('Moyenne')
ax.set_title('Comparaison des moyennes S1 vs S2')
ax.legend()

plt.show()
```

**Exemple avec des ventes par magasin :**

Pour comparer les ventes de produits entre deux magasins :

```python
positions_y = np.arange(len(ventes))
largeur = 0.35

fig, ax = plt.subplots()
ax.barh(positions_y - largeur/2, ventes.magasin_paris, largeur, label='Paris', color='blue')
ax.barh(positions_y + largeur/2, ventes.magasin_lyon, largeur, label='Lyon', color='green')

ax.set_yticks(positions_y)
ax.set_yticklabels(ventes.produit)
ax.set_xlabel('Ventes')
ax.set_title('Comparaison des ventes Paris vs Lyon')
ax.legend()

plt.show()
```

💡 **Astuce** : Il est possible de choisir l'ordre de tri (croissant ou décroissant) en renseignant le paramètre `ascending=` à `.sort_values`:
- `True`: tri dans l'ordre croissant
- `False`: tri dans l'ordre décroissant

![sort](img/Slide6.jpg)

### ⚡ Expérimentation ⚡

Dans un nouveau bloc de code:
- Triez d'abord votre DataFrame `pivot_moyennes_filtre` par la colonne `boost` avec `.sort_values('boost', ascending=True)`
- Créez un graphique comparatif avec deux séries de barres horizontales côte à côte en utilisant matplotlib
- Une série pour les moyennes quand le pays n'organise pas (`avg_ext`)
- Une série pour les moyennes quand le pays organise (`avg_dom`)
- Utilisez `plt.barh()` avec des positions ajustées (comme dans l'exemple ci-dessus) pour créer les barres côte à côte
- Ajoutez une légende pour distinguer les deux séries







