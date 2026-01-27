# Atelier Infographie : Créez votre propre Fiche Pokémon

Bienvenue dans cet atelier créatif ! Nous allons maintenant utiliser les compétences que nous avons acquises pour générer une infographie : une fiche de statistiques pour un Pokémon, comme dans le jeu !

---
## Étape 1 : Importer les bibliothèques

### Explication
Pour commencer, nous avons besoin de nos outils. Nous allons importer la bibliothèque **Pandas** pour gérer nos données, ainsi que la bibliothèque **random** pour nous aider à choisir un Pokémon au hasard.

### ⚡ Expérimentation ⚡:
- Dans un nouveau bloc de code:
    - Importer la bibliothèque pandas
    - Importer la bibliothèque random

### 💡 Astuce 💡:
- Reférez-vous au [starter](starter.md) pour savoir comment importer une bibliothèque.
- N'oubliez pas d'exécuter vos cellules de code.

---
## Étape 2 : Lire les données et les stocker

### Explication
Comme dans les ateliers précédents, nous allons lire un fichier CSV, cette fois-ci `complete_pokedex.csv`, et le stocker dans un **DataFrame** Pandas pour pouvoir travailler avec.

### ⚡ Expérimentation ⚡:
- Dans un nouveau bloc de code:
    - Lisez le csv `complete_pokedex.csv` et stockez-le dans un dataframe `pokemon_df`.

### 💡 Astuce 💡:
- Comme précédemment, prenez le temps d'observer le dataframe: nombre de lignes, nom des colonnes, etc.

---
## Étape 3 : Sélectionner un Pokémon de façon aléatoire

### Explication
Pour pimenter un peu les choses, nous allons laisser le hasard choisir pour nous ! Nous allons utiliser la fonction `random.randint()` pour générer un nombre aléatoire entre 1 et 1024, qui correspond à l' `id` d'un Pokémon dans notre tableau. Ensuite, nous filtrerons le DataFrame pour ne garder que la ligne de ce Pokémon.

### Exemple:
Pour générer un nombre aléatoire allant de 1 à 6 (comme un jet de dé) en Python:
```python
>>> random.randint(1, 6)
4
```

### ⚡ Expérimentation ⚡:
- Dans un nouveau bloc de code:
    - Générez un nombre aléatoire entre 1 et 1024, stockez ce nombre dans une variable `random_id`.
    - Récupérez la ligne dont la colonne `id` vaut `random_id` dans le DataFrame `pokemon_df` (filtre), stockez cette ligne dans une variable `my_pokemon`.

### 💡 Astuce 💡:
- Attention ne confondez pas la valeur de `id` dans `pokemon_df` (commence à 1) et le numéro de la ligne dans `pokemon_df` (commence à 0).
- Vous pouvez afficher le contenu de vos variables (ici `my_pokemon`) en terminant votre cellule de code par une ligne avec cette variable.

---
## Étape 4 : Récupérer les informations du Pokémon

### Explication
Maintenant que nous avons une seule ligne dans notre DataFrame `my_pokemon`, nous devons en extraire les informations (son nom, son type, ses statistiques...). Pour récupérer une valeur unique depuis une colonne d'un DataFrame ne contenant qu'une ligne, nous utilisons la syntaxe `.values[0]`.

### Exemple:
Si nous avons un DataFrame `df` d'une seule ligne :
| nom | age | classe | moyenne |
| --- | --- | --- | --- |
| Bob | 16  | 1ère   |  14.2 |

```python
>>> nom_eleve = df.nom.values[0]
>>> nom_eleve
'Bob'
```
```python
>>> moyenne_eleve = df.moyenne.values[0]
>>> moyenne_eleve
14.2
```

### ⚡ Expérimentation ⚡:
- Dans un nouveau bloc de code:
    - Dans une variable `my_poke_name` récupérez le nom de votre Pokémon.
    - Dans une variable `my_poke_catch` récupérez l'indice de capture de votre Pokémon.
    - Dans une variable `my_poke_type1` récupérez le premier type de votre Pokémon.
    - Dans une variable `my_poke_type2` récupérez le second type de votre Pokémon.
    - Dans une variable `my_poke_hp` récupérez la valeur de sa statistique de PV.
    - Dans une variable `my_poke_atk` récupérez la valeur de sa statistique d'attaque.
    - Dans une variable `my_poke_def` récupérez la valeur de sa statistique de défense.
    - Dans une variable `my_poke_spe_atk` récupérez la valeur de sa statistique d'attaque spéciale.
    - Dans une variable `my_poke_spe_def` récupérez la valeur de sa statistique de défense spéciale.
  - Dans une variable `my_poke_speed` récupérez la valeur de sa statistique de vitesse.
    - Dans une variable `my_poke_stats_total` stockez la somme totale des statistiques de votre Pokémon.

### 💡 Astuce 💡:
- Vous pouvez faire un `print(my_poke_name, my_poke_type1, ..., my_poke_speed)` à la fin de votre bloc de code pour vérifier la valeur de toutes vos variables.

---
## Étape 5 : Utiliser des fonctions pour des tâches complexes

### Explication
Parfois, une tâche peut être complexe ou répétitive. Pour simplifier notre code, nous pouvons l'encapsuler dans une **fonction**. Une fonction est un bloc de code réutilisable auquel on donne un nom. Nous allons utiliser des fonctions déjà préparées pour générer les URLs des images des Pokémon et calculer les probabilités de capture.

### Exemple
Déclarer et utiliser une fonction :
```python
# On déclare une fonction qui prend un nom en argument
def saluer(nom):
    return f"Bonjour, {nom} !"

# On peut ensuite l'utiliser autant de fois qu'on veut
>>> saluer("Alice")
'Bonjour, Alice !'
>>> saluer("Bob")
'Bonjour, Bob !'
```

### ⚡ Expérimentation ⚡:
- Dans un nouveau bloc de code, copiez-collez les fonctions `get_img_url(id)`, `get_type_url(name)` et `catch_pct(C, B)` depuis le fichier `infographic.md` original.
- **Ensuite, dans une nouvelle cellule** :
    - En utilisant la fonction `get_img_url()`, récupérez le lien vers le sprite de votre Pokémon dans une variable `my_poke_img`.
    - En utilisant (deux fois) la fonction `get_type_url()`, récupérez le lien vers les illustrations des deux types de votre Pokémon dans deux variables nommées respectivement `my_poke_type1_url` et `my_poke_type2_url`.
    - Utilisez (plusieurs fois) la fonction `catch_pct()` pour calculer et stocker dans les variables `proba_poke`, `proba_super`, `proba_hyper` les pourcentages de chance d'attraper votre Pokémon avec une PokéBall, une SuperBall et une HyperBall.

### 💡 Astuce 💡:
- Lors des étapes précédentes vous avez normalement récupéré l'indice de capture de votre Pokémon dans une variable appelée `my_poke_catch`.

---
## Étape 6 : Afficher le rendu final

### Explication
C'est le moment d'assembler tout notre travail ! Nous allons utiliser un bloc de code HTML/CSS fourni pour mettre en forme toutes les variables que nous avons préparées et afficher une belle fiche de statistiques.

### ⚡ Expérimentation ⚡:
- Lorsque vous avez terminé toutes les étapes précédentes, vous pouvez enfin afficher le rendu de votre fiche dans votre notebook Jupyter avec le code suivant (à copier-coller directement dans un nouveau bloc de code à la fin de votre notebook).
```python
from IPython.display import HTML, display

html_code = f"""
<!DOCTYPE html>
... (le reste du code HTML du fichier original) ...
</html>
"""

display(HTML(html_code))
```
- Exécutez la cellule. Si toutes vos variables des étapes précédentes sont correctement nommées, vous devriez voir apparaître la fiche de statistique complète et stylisée de votre Pokémon !
