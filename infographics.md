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
- Dans un nouveau bloc de code, copiez-collez les fonctions `get_img_url(id)`, `get_type_url(name)` et `catch_pct(C, B)` (disponibles dans la documentation complète).
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
<html lang="fr">
<head>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {{
            --bg-color: transparent;
            --card-bg: #ffffff;
            --text-main: #2c3e50;
            --text-secondary: #7f8c8d;
            --accent-border: #dfe6e9;
            --main-color: #58A8F8;
            
            --hp-color: #FF5959;
            --atk-color: #F5AC78;
            --def-color: #FAE078;
            --spatk-color: #9DB7F5;
            --spdef-color: #A7DB8D;
            --spd-color: #FA92B2;
        }}

        .pokemon-card {{
            font-family: 'Poppins', sans-serif;
            background: var(--card-bg);
            width: 320px;
            padding: 30px 20px;
            border-radius: 24px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            text-align: center;
            position: relative;
            margin: 20px auto;
            overflow: hidden;
        }}

        .image-container {{
            width: 140px; height: 140px;
            margin: 0 auto 10px;
            position: relative;
            display: flex; justify-content: center; align-items: center;
        }}
        
        .image-bg {{
            position: absolute; width: 100%; height: 100%;
            background: radial-gradient(circle, rgba(88, 168, 248, 0.2) 0%, transparent 70%);
            border-radius: 50%; z-index: 0;
        }}

        .image-container img {{
            width: 100%; height: 100%;
            object-fit: contain; position: relative; z-index: 1;
            filter: drop-shadow(0 5px 5px rgba(0,0,0,0.2));
            image-rendering: pixelated; 
        }}

        .pokemon-name {{
            font-size: 1.8rem; font-weight: 700; color: var(--text-main);
            margin: 5px 0 5px 0; text-transform: capitalize;
        }}

        .name-underline {{
            height: 4px; width: 40px; background: var(--main-color);
            margin: 0 auto 20px; border-radius: 2px; opacity: 0.8;
        }}

        .types-container {{
            display: flex; justify-content: center; gap: 12px;
            margin-bottom: 25px; align-items: center;
        }}

        .type-img-wrapper img {{
            height: 28px; width: auto; 
            filter: drop-shadow(0 2px 3px rgba(0,0,0,0.1));
            transition: transform 0.2s;
        }}
        .type-img-wrapper img:hover {{ transform: scale(1.1); }}

        .stats-box {{
            position: relative;
            border: 1px solid var(--accent-border);
            border-radius: 18px;
            padding: 25px 15px 15px;
            margin-bottom: 25px;
            text-align: left;
            background: linear-gradient(to bottom, #ffffff, #fafbfc);
        }}

        .total-label {{
            position: absolute; top: -12px; right: 15px;
            background: var(--text-main); color: white;
            padding: 4px 10px; font-weight: 700; font-size: 0.75rem;
            border-radius: 10px; text-transform: uppercase;
        }}

        .stat-row {{ display: flex; align-items: center; margin-bottom: 10px; }}
        .stat-name {{ width: 70px; font-weight: 600; color: var(--text-secondary); font-size: 0.75rem; }}
        .stat-bar-bg {{ flex-grow: 1; height: 6px; background-color: #eff2f6; border-radius: 4px; overflow: hidden; margin: 0 10px; }}
        .stat-bar-fill {{ height: 100%; border-radius: 4px; }}
        .stat-value {{ width: 25px; text-align: right; font-weight: 700; color: var(--text-main); font-size: 0.8rem; }}

        .catch-container {{ display: flex; justify-content: space-between; padding: 0 5px; }}
        .catch-circle {{
            width: 70px; height: 80px;
            border-radius: 16px; background: white;
            border: 1px solid var(--accent-border);
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            transition: all 0.3s ease;
        }}
        .catch-ball-img {{ width: 32px; margin-bottom: 4px; }}
        .catch-percent {{ font-size: 0.85rem; font-weight: 700; color: var(--text-main); }}
        .catch-label {{ font-size: 0.6rem; color: var(--text-secondary); }}
        .catch-circle:hover {{ transform: translateY(-3px); border-color: var(--main-color); }}

    </style>
</head>
<body>

    <div class="pokemon-card">
        
        <div class="image-container">
            <div class="image-bg"></div>
            <img src="{my_poke_img}" alt="{my_poke_name}">
        </div>

        <div class="pokemon-name">{my_poke_name}</div>
        <div class="name-underline"></div>

        <div class="types-container">
            <div class="type-img-wrapper"><img src="{my_poke_type1_url}"></div>
            {f'<div class="type-img-wrapper"><img src="{my_poke_type2_url}"></div>' if my_poke_type1_url != my_poke_type2_url else ''}
        </div>

        <div class="stats-box">
            <div class="total-label">Total : {my_poke_stats_total}</div>

            <div class="stat-row">
                <span class="stat-name">PV</span>
                <div class="stat-bar-bg"><div class="stat-bar-fill" style="width: {(my_poke_hp / 255) * 100}%; background-color: var(--hp-color);"></div></div>
                <span class="stat-value">{my_poke_hp}</span>
            </div>
            <div class="stat-row">
                <span class="stat-name">Attaque</span>
                <div class="stat-bar-bg"><div class="stat-bar-fill" style="width: {(my_poke_atk / 255) * 100}%; background-color: var(--atk-color);"></div></div>
                <span class="stat-value">{my_poke_atk}</span>
            </div>
            <div class="stat-row">
                <span class="stat-name">Défense</span>
                <div class="stat-bar-bg"><div class="stat-bar-fill" style="width: {(my_poke_def / 255) * 100}%; background-color: var(--def-color);"></div></div>
                <span class="stat-value">{my_poke_def}</span>
            </div>
            <div class="stat-row">
                <span class="stat-name">Atq. Spé.</span>
                <div class="stat-bar-bg"><div class="stat-bar-fill" style="width: {(my_poke_spe_atk / 255) * 100}%; background-color: var(--spatk-color);"></div></div>
                <span class="stat-value">{my_poke_spe_atk}</span>
            </div>
            <div class="stat-row">
                <span class="stat-name">Déf. Spé.</span>
                <div class="stat-bar-bg"><div class="stat-bar-fill" style="width: {(my_poke_spe_def / 255) * 100}%; background-color: var(--spdef-color);"></div></div>
                <span class="stat-value">{my_poke_spe_def}</span>
            </div>
            <div class="stat-row">
                <span class="stat-name">Vitesse</span>
                <div class="stat-bar-bg"><div class="stat-bar-fill" style="width: {(min(my_poke_speed/255) * 100)}%; background-color: var(--spd-color);"></div></div>
                <span class="stat-value">{my_poke_speed}</span>
            </div>
        </div>

        <div class="catch-container">
            <div class="catch-circle">
                <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/items/poke-ball.png" class="catch-ball-img">
                <span class="catch-percent">{proba_poke}%</span>
                <span class="catch-label">Poke Ball</span>
            </div>
            
            <div class="catch-circle">
                <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/items/great-ball.png" class="catch-ball-img">
                <span class="catch-percent">{proba_super}%</span>
                <span class="catch-label">Super Ball</span>
            </div>
            
            <div class="catch-circle">
                <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/items/ultra-ball.png" class="catch-ball-img">
                <span class="catch-percent">{proba_hyper}%</span>
                <span class="catch-label">Hyper Ball</span>
            </div>
        </div>
    </div>
</body>
</html>
"""

display(HTML(html_code))
```

## Idées de bonus:

Voici quelques idées pour aller plus loin avec votre fiche de statistiques Pokémon :

### Générer plusieurs fiches

Générez des fiches pour plusieurs Pokémons différents. Vous pouvez relancer toutes les cellules de votre notebook avec un numéro de Pokémon que vous avez choisi au lieu d'un numéro aléatoire.


### Récupérer les sprite en version chromatique

Vous pouvez rendre votre fiche encore plus intéressante en affichant le sprite de votre Pokémon dans sa version chromatique (shiny), qui propose des couleurs alternatives souvent recherchées par les collectionneurs.

Pour récupérer l'URL du sprite chromatique, il suffit de remplacer `pokemon` par `pokemon/shiny` dans l'URL utilisée précédemment. Par exemple, l'URL pour le Léviator chromatique (id 130) devient :
```
https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/130.png
```

au lieu de 
```
https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/130.png
```

Vous pouvez donc créer une nouvelle fonction Python pour obtenir l'URL de la version chromatique :
```python
def get_shiny_img_url(id):
    return f"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/{id}.png"
```

Utilisez cette fonction pour afficher l'image shiny dans votre fiche, à côté ou en dessous du sprite classique.


### Personnaliser le design

Modifiez les couleurs, les styles CSS, ou la mise en page de votre fiche pour créer un design unique. Par exemple :
- Changez les couleurs des barres de statistiques (reportez-vous au fichier [starter.md](starter.md) pour voir comment utiliser des couleurs en format Hexadécimal)

### Comparer deux Pokémons

Créez une fiche de comparaison qui affiche côte à côte les statistiques de deux Pokémons différents.

### Ajouter des informations supplémentaires

Enrichissez votre fiche avec d'autres informations disponibles dans le DataFrame, comme :
- La génération à laquelle il appartient
- Son habitat
- Sa description
- Le cri du Pokémon `https://raw.githubusercontent.com/PokeAPI/cries/main/cries/pokemon/latest/<id_du_pokemon>.ogg`
- etc.

display(HTML(html_code))
```
- Exécutez la cellule. Si toutes vos variables des étapes précédentes sont correctement nommées, vous devriez voir apparaître la fiche de statistique complète et stylisée de votre Pokémon !
