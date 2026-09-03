# Documentation JOJA

Ce document s'adresse à quelqu'un qui **découvre le projet** et n'a pas forcément de bagage en data science. Il explique ce qu'on a fait, pourquoi, et ce qu'on en a tiré. Pour le détail technique (calculs, code, graphiques), tout se trouve dans `joja_analysis.ipynb`, qui reste la référence.

---

## En une phrase

On a analysé 3,4 millions de commandes d'un site de courses en ligne pour en tirer des constats concrets : quels produits marchent, qui rachète quoi, l'offre est-elle bien dimensionnée ? Chaque réponse aux questions est complétée par une proposition des actions que le magasin peut réellement prendre.

---

## Le projet en contexte

**JOJA** est un exercice d'analyse exploratoire de données (EDA) pour Epitech. Le principe : on nous donne des données brutes d'un site de livraison de courses (inspirées du jeu de données public Instacart), et on doit en extraire des **insights actionnables** — pas juste des statistiques, mais des observations qui débouchent sur une décision concrète pour le business.

---

## Les données, en clair

Le site fournit 5 fichiers. Voici ce qu'ils contiennent :

| Fichier | Ce qu'il contient | Volume |
|---|---|---|
| `orders` | Une ligne = une commande passée par un client (quand, par qui, dans quel ordre par rapport à ses commandes précédentes) | 3,4 millions de commandes, 206 209 clients |
| `order_products` | Une ligne = un produit à l'intérieur d'une commande (position dans le panier, si c'est un rachat) | 32,4 millions de lignes |
| `products` | La liste des produits du catalogue (nom, à quel rayon il appartient) | 49 688 produits |
| `aisles` | La liste des rayons (ex. "fresh fruits", "red wines") | 134 rayons |
| `departments` | La liste des départements, qui regroupent plusieurs rayons (ex. "produce", "alcohol") | 21 départements |

**Repère utile :** chaque client a entre 4 et 100 commandes dans les données. Les rayons sont regroupés en départements. Par exemple, le rayon *fresh fruits* fait partie du département *produce*.

**Une subtilité découverte en cours d'analyse :** pour chaque client, sa toute dernière commande a été volontairement gardée dans `orders` mais **retirée** de `order_products` (son contenu est caché). Concrètement : dès qu'une analyse porte sur le *contenu* des paniers, elle ne peut porter que sur l'historique de chaque client (ses commandes précédentes), pas sur sa toute dernière commande. C'est expliqué en détail dans la section 1 du notebook.

---

## Comment le notebook est organisé

`joja_analysis.ipynb` se lit dans l'ordre, du haut vers le bas :

1. **Contexte, méthodologie, choix des outils** : pourquoi pandas/matplotlib/seaborn, quelle méthode on suit (EDA), quelle règle on s'impose sur les graphiques (un type de graphique = un seul usage).

2. **Préparation des données** : chargement des fichiers, vérification qu'il n'y a pas d'erreurs ou d'incohérences cachées (valeurs manquantes, doublons, la subtilité sur la dernière commande mentionnée plus haut), puis construction d'une table produits enrichie (produit + son rayon + son département en une seule table).

3. **Clientèle**

4 questions sur l'offre du magasin : combien d'artiles les clients commandent, quand les clients commandent par commande, quels produits sont ajoutés en premier/dernier au panier, quels rayons sont les plus souvent combinés dans une même commande.

4. **Stock / assortiment**

4 questions sur l'offre du magasin : la gamme de produits est-elle bien répartie, est-elle alignée sur la demande, quels produits tournent peu, quels rayons sont souvent achetés ensemble.

5. **Performances**

4 questions sur les ventes : quels sont les produits les plus vendus, quelle part du bio, le taux de réachat, à quel point les ventes sont concentrées sur peu de produits.

Chaque question suit le même déroulé : **objectif → calcul → graphique → lecture des résultats → piste d'action**.

---

## Ce qu'on a trouvé (résumé sans les calculs)

### Clientèle

(à compléter)

### Stock / assortiment

- **`personal care` est sur-dimensionné** : 20 % de toutes les références du catalogue, mais seulement 1,4 % du volume vendu. À l'inverse, **`produce`** (fruits et légumes) ne représente que 5 % des références mais **29 %** des ventes.
- **Une petite partie du catalogue ne sert presque à rien** : 6,4 % des produits vendus (~3 171 références) ne pèsent que 0,04 % du volume total — des candidats naturels à retirer du catalogue.
- **Deux associations classiques testées avec les données** : "fromage + vin" n'est **pas confirmée** (les clients ne les achètent pas plus ensemble qu'au hasard), alors que "nourriture chat + nourriture chien" l'est largement (achetés ensemble ~5x plus souvent qu'au hasard).

### Performances (ventes)

- Le **top 15** des produits les plus vendus est dominé par des fruits et légumes frais, souvent bio (bananes, fraises, épinards, avocats...).
- **10 % du catalogue est bio**, mais ces produits représentent **32 % de tout ce qui est acheté** — le bio se vend largement mieux que sa part dans l'offre. 74 % des commandes contiennent au moins un produit bio.
- **59 % de tout ce qui est acheté est un rachat** (le client avait déjà commandé ce produit avant). Ce taux varie de 32 % (`personal care`) à 67 % (`dairy eggs`) selon le département.
- **9 % des produits du catalogue génèrent 80 % du volume de ventes** — l'activité repose sur un noyau très restreint de références.

Chaque constat est accompagné dans le notebook d'une **piste d'action concrète** (ex. resserrer la gamme `personal care`, mettre en avant le rapprochement chat/chien plutôt que fromage/vin).

---

## Petit glossaire

| Terme | Ce que ça veut dire ici |
|---|---|
| **EDA** | *Exploratory Data Analysis* : explorer des données brutes pour en dégager une compréhension, avant d'en tirer des conclusions |
| **Rayon / département** | Le rayon est la catégorie fine (ex. *red wines*), le département la catégorie large qui regroupe plusieurs rayons (ex. *alcohol*) |
| **Réachat (`reordered`)** | Le client avait déjà commandé ce produit lors d'une commande précédente |
| **Taux de réachat** | Sur 100 produits achetés, combien sont des rachats plutôt qu'un premier achat |
| **Bio** | Ici, un produit est considéré "bio" si son nom contient le mot *organic* (c'est une approximation, pas une certification officielle) |
| **Concentration des ventes** | À quel point les ventes reposent sur peu de produits plutôt que d'être réparties également sur tout le catalogue |
| **Lift** | Mesure statistique : à quel point deux rayons sont achetés ensemble *plus souvent* que si c'était le pur hasard. `lift = 1` → aucun lien, `lift > 1` → association réelle |
| **Largeur de gamme** | Le nombre de références différentes disponibles dans un rayon ou un département |
| **Sur-assorti / sous-assorti** | Un département a plus (ou moins) de références que ce que son volume de ventes justifierait |

---

## Lancer le projet soi-même

```bash
pip install -r requirements.txt
jupyter notebook joja_analysis.ipynb
```

Les fichiers de données doivent être dans un dossier `datasets/` à la racine du projet (non fournis dans le repo, voir `README.md`).

---

## Pour aller plus loin

- **`axes_d'analyses.md`** : le plan détaillé de toutes les questions traitées (et celles encore prévues), regroupées par thème métier.
- **`README.md`** : structure du repo, installation, équipe.
- **`joja_analysis.ipynb`** : le détail technique complet (code, calculs, graphiques, justifications).

## Équipe

Samyra Mangan Mben · Tiavina Ranarivelo · Jules Lejeune
