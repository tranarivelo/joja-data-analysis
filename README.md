# JOJA Analyse exploratoire des données (EDA)

Exploration d'un jeu de données de courses en ligne: Instacart, environ 3,4M commandes, 200k clients. L'objectif est d'en tirer des insights business utiles pour la prise d'actions.

## Contenu

- `joja_analysis.ipynb` : notebook principal : analyse et visualisations, question par question.
- `datasets/` : fichiers sources (`orders`, `order_products`, `products`, `aisles`, `departments`).
- `axes_d'analyses.md` : plan détaillé des axes d'analyse.

## Setup

```bash
pip install -r requirements.txt
jupyter notebook joja_analysis.ipynb
```

## Axes d'analyse

Le plan complet (regroupement par thème métier + détail question par question : type d'analyse, données mobilisées, graphique, insight visé) se trouve dans [`axes_d'analyses.md`](axes_d'analyses.md). Les choix sont ensuite justifiés étape par étape directement dans `joja_analysis.ipynb`.


## Equipe :

- Samyra Mangan Mben
- Tiavina Ranarivelo
- Jules Lejeune 