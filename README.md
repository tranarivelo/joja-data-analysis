# JOJA Analyse exploratoire des données

Exploration d'un jeu de données de courses en ligne: Instacart, environ 3,4M commandes, 200k clients. L'objectif est d'en tirer des insights business utiles pour la prise d'actions.

## Contenu

- `joja_analysis.ipynb` : notebook principal : analyse et visualisations, question par question.
- `datasets/` : fichiers sources (`orders`, `order_products`, `products`, `aisles`, `departments`).
- `axes_analyse.csv` : plan des axes d'analyse.

## Setup

```bash
pip install -r requirements.txt
jupyter notebook joja_analysis.ipynb
```

## Axes d'analyse

Le détail de chaque axe (type d'analyse, données mobilisées, graphique, insight business) se trouve dans le notebook `joja_analysis.ipynb`. Nous avons également décidé d'y justifier nos choix, étape par étape. 

### Analyse de la clientèle

1. Combien d'articles les clients commandent-ils par commande ?
2. Quand les clients commandent-ils (jour de la semaine × heure) ?
3. Quel produit est ajouté en premier / en dernier au panier ?
4. À quelle fréquence un client repasse-t-il commande (nombre de commandes, jours entre deux commandes) ?
5. Quels rayons sont les plus souvent combinés dans une même commande ?

### Stock / assortiment

1. Comment l'assortiment se répartit-il entre les rayons et les départements (largeur de gamme) ?
2. L'offre par catégorie est-elle alignée sur la demande (nombre de références vs volume vendu) ?
3. Quelle est la rotation de l'assortiment : quelle part des produits concentre l'essentiel des ventes, quelle part tourne peu ?
4. Quels rayons sont le plus souvent achetés ensemble et gagneraient à être rapprochés ou mis en avant (ex. fromage/vin, chat/chien) ?

### Performances

1. Quels sont les produits les plus vendus ?
2. Quel est le ratio de commandes bio vs non-bio ?
3. Quel est le taux de réachat global (et par département) ?
4. Quelle est la concentration des ventes (part des produits réalisant 80 % du volume) ?


## Equipe :
- Samyra Mangan Mben
- Tiavina Ranarivelo
- Jules Lejeune 