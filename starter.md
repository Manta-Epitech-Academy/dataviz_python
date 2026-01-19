# Introduction

## Contexte

Vous devez répondre à la question : Est-ce que les pays obtiennent plus de médailles quand ils organisent les Jeux Olympiques d'hiver ?

Pour cela vous avez à votre disposition un jeu de données comportant l'ensemble des médailles obtenues aux JO d'hiver depuis la première édition en 1924 jusqu'à l'édition de 2010.

## Ce que vous allez faire durant cet atelier

En utilisant le langage Python et des outils d'analyse de données vous allez tenter de répondre à la question posée en introduction.

## Prise en main de l'environnement Jupyter Notebook

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
- Une ligne commençant par `#` en Markdown permet de déclarer un titre

- **Bloc de code (Python)** :

Entrez votre premier bloc de code Python dans votre notebook.

```python
print("Hello, world!")
21 * 2
```

La combinaison `Ctrl+Entrée` vous permet d'exécuter votre bloc de code.

### 💡 Astuce 💡:
- Le résultat de la dernière expression entrée dans un bloc de code (ici `21 * 2`) de votre notebook est automatiquement affiché (si possible) après le bloc de code

# Lecture du CSV

Lors de l'étape précédente vous avez uploadé le fichier CSV fourni sur votre environnement Jupyter.

Un fichier CSV est un fichier texte qui stocke des données sous forme de tableau.
Chaque ligne du CSV correspond à une ligne de données, chaque valeur est séparée par une virgule.

![csv](img/csv.png)

Nous allons utiliser la bibliothèque **Pandas** pour lire, organiser et analyser ces données. L'utilisation d'une bibliothèque telle que **Pandas** permet de nous faciliter le travail sur des tableaux de données.

## ⚡ Expérimentation ⚡ :

Dans un bloc de code:
- importez la bibliothèque **Pandas**
- utilisez **Pandas** pour lire le fichier CSV dans un **DataFrame** (df)

---
```python
import pandas

df = pandas.read_csv("winter_olympics_medals.csv")
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

Un DataFrame est la structure de données principale de Pandas.
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

Il est ensuite possible d'appliquer un calcul sur chacun des groupes: ici on récupère leur taille.


![groupby2](img/Slide4.jpg)

💡 Astuce 💡 :

`.reset_index(name="xxx")` permet de réinitialiser l'index d'une série/groupement en DataFrame tout en donnant le nom "xxx" à la nouvelle colonne contenant les valeurs.

## ⚡ Expérimentation ⚡:

- **Bloc de code**:
  Regroupez les médailles obtenues par la France par année. Comptez le nombre de médailles obtenues chaque année. Votre nouvelle colonne devrait s'appeler `medal_count`.

- **Bloc de Markdown** :  
  Rédigez une courte réponse à la question suivante:
  - Quel est le nombre de médailles remportées par la France en 1968 et en 1992 ?
    
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

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Ajoutez le code nécessaire pour afficher un graphe (exemple ci-dessus) montrant le nombre de médailles obtenues par la France à chaque JO d'hiver.
  - Vous pouvez ensuite tenter de personnaliser votre graphe.

- **Explications** :
  Pouvez-vous expliquer chaque ligne de code de l'exemple précédent ?


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


# Trier des données avec Pandas

Nous voulons ici savoir quels sont les pays ayant obtenu le plus de médailles dans l'histoire des JO d'hiver. Pour cela il va falloir trier les pays par nombre de médailles.

La méthode `sort_values()` de Pandas permet de trier facilement un DataFrame selon une ou plusieurs colonnes.  
- Si vous souhaitez trier les lignes par ordre croissant ou décroissant d'une colonne, il suffit d'indiquer le nom de la colonne avec le paramètre `by`.
- Le paramètre `ascending` permet de choisir entre l'ordre croissant (`True`, par défaut) ou décroissant (`False`).
- Il est aussi possible de trier selon plusieurs colonnes en passant une liste de noms de colonnes.


## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Triez les pays par nombre de médailles obtenues
  - Affichez le graphique correspondant


# Top 5

Nous voulons garder que le Top 5 des pays en nombre de médailles obtenues aux JO d'hiver.

Il est possible de récupérer les `N` premiers éléments d'un DataFrame avec la méthode `.head(N)`, si votre DataFrame est déjà trié par ordre décroissant cela revient à faire un "Top N" 

💡 Astuce 💡:
- Dans cet exemple, on suppose que votre DataFrame trié s'appelle `classement_pays` (classement des pays par nombre de médailles).


➡️ Après avoir utilisé `.head(3)`, vous aurez un DataFrame contenant uniquement les 3 premières lignes du tableau, dans l'ordre d'origine.

### Exemple visuel

Avant `head(3)` :  

| artiste        | écoutes |
|----------------|---------|
| Jul            | 350     |
| Aya Nakamura   | 320     |
| Orelsan        | 280     |
| Stromae        | 230     |
| PNL            | 220     |
| Angèle         | 189     |

Après `classement_artistes.head(3)` :  

| artiste      | écoutes |
|--------------|---------|
| Jul          | 350     |
| Aya Nakamura | 320     |
| Orelsan      | 280     |


## ⚡ Expérimentation ⚡

Dans un nouveau bloc de code :
- Utilisez simplement `.head(5)` sur votre DataFrame déjà trié de l'étape précédente pour obtenir le top 5.
- Affichez ensuite le graphique correspondant (par exemple un barplot avec matplotlib ou pandas plotting) sur ce top 5 uniquement.

---

