  ### `starter.md` (Introduction)

   * **Durée de l'atelier : moyenne (2h-3h)**
       * Cet atelier introduit plusieurs concepts fondamentaux de la programmation (Python), de la manipulation de données (Pandas) et de la visualisation (Matplotlib), avec de nombreuses
         sections d'expérimentation.

   * **Difficulté des Concepts : moyen**
       * Bien qu'il introduise des concepts entièrement nouveaux pour un débutant (environnement Jupyter, DataFrames, fonctions, filtrage de base, tracés simples), ils sont présentés de
         manière très progressive et expliquée, le rendant facile à suivre.

   * **Quantité de Code : moyenne**
       * L'étudiant doit écrire plusieurs blocs de code différents, couvrant l'initialisation, la lecture de données, le filtrage, le regroupement et la création d'un premier graphique. Les tâches sont simples mais variées.

---

### `infographics.md` (Statistiques Pokémon)

*   **Durée *(estimée)* de l'atelier : moyenne**
    *   Il y a un nombre modéré d'étapes, car il faut rassembler de nombreuses informations différentes (nom, stats, types, URL des images, etc.) une par une.

*   **Difficulté des Concepts *(après avoir fait le starter)* : accessible**
    *   Le nouveau concept le plus difficile est la "déclaration" et (surtout) l'utilisation de fonctions, mais il est présenté avec des exemples simples et prêts à être copiés. Les concepts complexes (formule du taux de capture, HTML/CSS de la fiche de statistique) sont fournis et n'ont pas besoin d'être compris en totalité pour terminer l'atelier.

*   **Quantité de Code : moyenne**
    *   Le participant écrit très peu de *nouveau* code lui-même. La plupart des tâches consistent en des instructions d'une seule ligne pour extraire des données, ce qui est répétitif et renforce les compétences de l'atelier de démarrage. Le plus gros bloc de code (le rendu HTML final) est copié-collé.

### `analyse.md` (Analyse de Données Approfondie)

*   **Durée *(estimée)* de l'atelier : moyenne**
    *   Cet atelier comporte plusieurs étapes : nettoyage, regroupement, calcul de moyennes, vérification du nombre de participations, fusion, pivotage, calcul d'un score de "boost", et création de plusieurs visualisations. Le format guidé le rend gérable.

*   **Difficulté des Concepts *(après avoir fait le starter)*: moyenne**
    *   Cet atelier introduit plusieurs concepts de manipulation de données abstraits comme `pivot_table`. Cependant, les concepts sont décomposés avec des explications claires et des exemples, les rendant plus accessibles.

*   **Quantité de Code : moyenne**
    *   Cet atelier demande au participant d'écrire une quantité moyenne de code `pandas` et `matplotlib`, guidé par des exemples et des astuces.

### `prediction.md` (Apprentissage Automatique... ou presque)

*   **Durée *(estimée)* de l'atelier : courte**
    *   Cet atelier a le moins d'étapes : charger les données, les nettoyer, construire un modèle, l'entraîner, prédire et visualiser. Il est très direct.

*   **Difficulté des Concepts *(après avoir fait le starter)*: avancé**
    *   Les concepts sont les plus abstraits des trois ateliers. Il introduit le tout nouveau paradigme de l'apprentissage automatique (Machine Learning). Comprendre les rôles de `X` et `y`, ce qu'est un "modèle", et ce que signifient `.fit()` (entraîner) et `.predict()` (prédire) est un saut conceptuel énorme, bien loin de la simple consultation d'un tableau de données.

*   **Quantité de Code : faible**
    *   Étonnamment, cet atelier nécessite de taper peu de *nouveau* code. La bibliothèque `scikit-learn` est très puissante, et la plupart des actions se font en une seule ligne (ex: `model.fit(X, y)`). Cependant, chaque ligne a un poids conceptuel important.
