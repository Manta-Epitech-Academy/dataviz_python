# Introduction

## Rappel de l'atelier précédent

Dans l'atelier précédent, vous avez appris à :
- **Lire des données** avec Pandas (`pandas.read_csv()`)
- **Filtrer des données** pour extraire des sous-ensembles (`df[df.colonne == valeur]`)
- **Regrouper des données** avec `groupby()` pour calculer des statistiques
- **Visualiser des données** avec matplotlib (`plt.bar()`, `plt.plot()`, `plt.scatter()`)
- **Trier des données** avec `sort_values()`
- **Sélectionner les N premiers éléments** avec `.head(N)`

## Contexte

Maintenant, nous allons aller plus loin en apprenant à **prédire l'évolution du nombre d'utilisateurs Internet dans le futur**.

Pour cela vous avez à votre disposition un jeu de données comportant l'évolution du nombre d'utilisateurs Internet par pays depuis 1960 jusqu'à 2023.

## Ce que vous allez faire durant cet atelier

En utilisant le langage Python et des outils d'analyse de données et de machine learning, vous allez apprendre à :
1. Visualiser des données temporelles avec matplotlib
2. Créer un modèle de prédiction avec la régression linéaire (scikit-learn)
3. Faire des prédictions pour le futur

## Prise en main de l'environnement Jupyter Notebook

Si vous n'avez pas encore créé votre notebook, rendez-vous sur [Jupyter.org](https://jupyter.org/try-jupyter/lab/index.html)

- **Créer un nouveau notebook** : *New → Notebook* puis sélectionner le kernel **Python (Pyodide)**
- **Uploader le fichier CSV** : *Upload* → sélectionner `ict-adoption.csv` → valider

# Importer les bibliothèques

Avant de commencer, nous devons importer les bibliothèques nécessaires.

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  Importez `pandas` et `matplotlib.pyplot` (sous le nom `plt`).

# Lecture du CSV

Lisez le fichier CSV `ict-adoption.csv` avec **pandas** et stockez les données dans un dataframe `df`.

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  Lisez le fichier CSV `ict-adoption.csv` avec `pandas.read_csv()` et stockez le résultat dans une variable `df`. Affichez le DataFrame.

Prenez le temps d'observer les données présentes dans le DataFrame: 
- Le nombre de lignes
- Le nom des colonnes et les données qu'elles contiennent
- La colonne `year` qui indique l'année
- La colonne `numberOfInternetUsers` qui contient le nombre d'utilisateurs Internet

# Filtrer et nettoyer les données

Pour notre analyse, nous allons filtrer nos données pour ne garder qu'un seul pays, puis supprimer les valeurs manquantes.

## Exemple

Pour filtrer et nettoyer des données :

**Avant** (toutes les données) :

| | country | code | year | temperature |
|---|---|---|---|---|
| 0 | France | FRA | 2020 | 5.0 |
| 1 | Germany | DEU | 2020 | NaN |
| 2 | France | FRA | 2021 | 7.0 |
| 3 | France | FRA | 2022 | NaN |

```python
fra = df[df.code == "FRA"]
fra = fra.dropna()
fra
```

**Après** (données filtrées et nettoyées) :

| | country | code | year | temperature |
|---|---|---|---|---|
| 0 | France | FRA | 2020 | 5.0 |
| 2 | France | FRA | 2021 | 7.0 |

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Filtrez les données pour ne garder que la France en utilisant `df[df.code == "FRA"]`
  - Supprimez les lignes avec des valeurs manquantes avec `.dropna()`
  - Stockez le résultat dans une variable `fra` et affichez le DataFrame

# Premier graphique

Nous pouvons créer un graphique pour visualiser les données en utilisant **matplotlib**.

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  Créez un graphique en nuage de points avec `plt.scatter()` en utilisant `fra.year` en abscisse et `fra.numberOfInternetUsers` en ordonnée.


# Créer et entraîner le modèle de régression linéaire

La régression linéaire est une méthode qui permet de trouver une relation linéaire (une ligne droite) entre deux variables. Elle peut être utilisée pour prédire des valeurs futures.

## Exemple

Dans cet exemple, nous allons créer un modèle simple pour prédire le nombre de glaces vendues en fonction de la température, à l'aide du tableau suivant :

| | temperature | nb_glace_vendue |
|---|---|---|
| 0 | 18 | 22 |
| 1 | 20 | 28 |
| 2 | 22 | 36 |
| 3 | 24 | 45 |
| 4 | 26 | 54 |
| 5 | 28 | 65 |

**Avant** (données brutes) :

| | temperature | nb_glace_vendue |
|---|---|---|
| 0 | 18 | 22 |
| 1 | 20 | 28 |
| 2 | 22 | 36 |
| 3 | 24 | 45 |
| 4 | 26 | 54 |
| 5 | 28 | 65 |


```python
from sklearn.linear_model import LinearRegression

# Préparer les données
X = df_temp[['temperature']]  # Variable explicative (température) - DataFrame requis
y = df_temp.nb_glace_vendue  # Variable à prédire (nombre de glaces vendues)

# Créer et entraîner le modèle
model = LinearRegression()
model.fit(X, y)

# Faire des prédictions
y_pred = model.predict(X)

# Visualiser
plt.plot(df_temp.temperature, y_pred)
plt.show()
```

**Après** (modèle entraîné et ligne de régression affichée) :

Le modèle a trouvé une relation linéaire entre la température et le nombre de glaces vendues. La ligne de régression est affichée sur le graphique.

Cette ligne permet de **modéliser** (représenter de manière simplifiée) l'évolution d'une donnée par rapport à une autre.

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Importez `LinearRegression` depuis `sklearn.linear_model`
  - Préparez vos données : `X` doit contenir la colonne `year` (sous forme de DataFrame avec `fra[['year']]`), `y` doit contenir `fra.numberOfInternetUsers`
  - Créez un modèle `LinearRegression()`
  - Entraînez le modèle avec `.fit(X, y)`
  - Faites des prédictions avec `.predict(X)` et stockez le résultat dans `y_pred`
  - Affichez la ligne de régression avec `plt.plot(fra.year, y_pred)` puis `plt.show()`

💡 Astuce 💡 :

- `X` doit être un DataFrame (avec des doubles crochets `[['year']]`)
- `y` peut être une série (utilisez `fra.numberOfInternetUsers`)

# Combiner les données et la ligne de régression

Maintenant, affichons à la fois les données historiques et la ligne de régression sur le même graphique.

## Exemple

Pour afficher les points de données et la ligne de régression ensemble :

**Avant** (seulement la ligne de régression) :

Un graphique avec seulement la ligne de régression.

```python
plt.plot(df_temp.temperature, y_pred)
plt.scatter(df_temp.temperature, df_temp.nb_glace_vendue)
```

**Après** (points + ligne de régression) :

Un graphique montrant les points de données ET la ligne de régression qui représente la tendance.

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Affichez la ligne de régression avec `plt.plot(fra.year, y_pred)`
  - Ajoutez les points de données avec `plt.scatter(fra.year, fra.numberOfInternetUsers)`

💡 Astuce 💡 :

- Vous pouvez appeler plusieurs fonctions matplotlib dans le même bloc de code
- Les graphiques s'ajoutent les uns aux autres sur la même figure

# Faire des prédictions pour plusieurs années

Maintenant que notre modèle est entraîné, nous pouvons l'utiliser pour faire des prédictions pour des années futures.

## Exemple

Pour prédire le nombre de glaces vendues pour différentes températures :

**Avant** (modèle entraîné) :

Un modèle qui peut prédire le nombre de glaces vendues.

```python
prediction_future = model.predict(pandas.DataFrame({'temperature': [30, 32, 34]}))
prediction_future
```

**Après** (prédictions générées) :

Un tableau contenant les prédictions pour les températures 30°C, 32°C et 34°C.

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Prédisez le nombre d'utilisateurs Internet pour les années 2026, 2027 et 2028
  - Utilisez `pandas.DataFrame({'year': [2026, 2027, 2028]})` pour créer les données d'entrée
  - Stockez le résultat dans une variable `prediction_next` et affichez-la

💡 Astuce 💡 :

- Pour faire une prédiction, utilisez `.predict()` avec des données dans le même format que lors de l'entraînement
- Vous pouvez prédire plusieurs valeurs en une seule fois en passant plusieurs années dans le DataFrame

# Visualiser les prédictions

Ajoutons les prédictions futures sur notre graphique pour voir l'évolution prévue.

## Exemple

Pour afficher les prédictions sur le graphique :

**Avant** (graphique avec données historiques et ligne de régression) :

Un graphique montrant les données historiques et la ligne de régression.

```python
plt.plot(df_temp.temperature, y_pred)
plt.scatter(df_temp.temperature, df_temp.nb_glace_vendue)
plt.scatter([30, 32, 34], prediction_future, s=100, marker='*')
```

**Après** (graphique avec prédictions) :

Un graphique montrant les données historiques, la ligne de régression, ET des points étoiles indiquant les prédictions futures.

## ⚡ Expérimentation ⚡

- **Bloc de code (Python)** :  
  - Affichez la ligne de régression avec `plt.plot(fra.year, y_pred)`
  - Ajoutez les points de données historiques avec `plt.scatter(fra.year, fra.numberOfInternetUsers)`
  - Ajoutez les prédictions futures avec `plt.scatter([2026, 2027, 2028], prediction_next, marker='*', s=100)`
  - N'hésitez pas à personnaliser les couleurs comme vous l'avez appris dans l'atelier précédent

💡 Astuce 💡 :

- `plt.scatter()` accepte des paramètres pour personnaliser l'apparence du marqueur
- Vous pouvez passer plusieurs valeurs en même temps pour les abscisses et les ordonnées

# Conclusion

Félicitations ! Vous avez appris à :
- Charger et filtrer des données avec Pandas
- Visualiser des données avec matplotlib
- Créer un modèle de régression linéaire avec scikit-learn
- Faire des prédictions pour le futur

## Questions de réflexion

- Que montre la ligne de régression sur votre graphique ?
- Une prédiction pour 2050 vous semble-t-elle réaliste ? Pourquoi ?
- Quelles sont les limites de ce modèle de prédiction ?
