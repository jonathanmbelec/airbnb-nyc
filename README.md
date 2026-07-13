# Analyse et prédiction des prix Airbnb à New York

Analyse exploratoire et modélisation prédictive du prix des annonces Airbnb à New York, à partir du jeu de données public *New York City Airbnb Open Data* (Inside Airbnb, 2019).

## Objectif

Comprendre ce qui détermine le prix d'une annonce (arrondissement, type de logement, popularité, localisation) et construire un modèle de régression capable de le prédire à partir de ses caractéristiques.

## Contenu

Le notebook [`notebooks/analyse.ipynb`](notebooks/analyse.ipynb) couvre :

1. **Exploration et nettoyage des données** — valeurs manquantes, propriétaires, prix par arrondissement/type/quartier, popularité, ancienneté des annonces.
2. **Visualisation géographique et analyse des prix** — répartition spatiale des annonces, distribution des prix, évolution temporelle, distance aux grands parcs (feature engineering géospatial via la formule de Haversine).
3. **Modélisation prédictive** — préparation des données (imputation, encodage one-hot, standardisation robuste), analyse de colinéarité, régression linéaire, évaluation par erreur absolue moyenne (MAE).
4. **Conclusion et pistes d'amélioration**.

## Données

Le jeu de données utilisé correspond aux colonnes classiques du dataset *AB_NYC_2019* (Inside Airbnb / Kaggle), traduites en français :

| Colonne | Description |
|---|---|
| `ID`, `Nom` | Identifiant et titre de l'annonce |
| `ID proprio`, `Nom proprio` | Identifiant et nom de l'hôte |
| `Arrondissement`, `Quartier` | Localisation administrative |
| `Latitude`, `Longitude` | Coordonnées GPS |
| `Type` | Type de logement (logement entier, chambre privée, chambre partagée) |
| `Prix` | Prix par nuit ($) — variable cible |
| `Minimum nuits` | Nombre minimal de nuits exigé |
| `Nombre avis`, `Avis par mois`, `Dernier avis` | Indicateurs de popularité |
| `Affichages proprio` | Nombre d'annonces de l'hôte |
| `Jours disponibles annuel` | Disponibilité sur 365 jours |

Les fichiers de données (`airbnb.csv`, `nyc.jpg`) ne sont pas versionnés dans ce dépôt (voir `.gitignore`). Pour reproduire l'analyse, placez-les dans un dossier `fichiers/` à la racine du projet.

## Installation

```bash
git clone <url-du-depot>
cd <nom-du-depot>
pip install -r requirements.txt
jupyter notebook notebooks/Airbnb_NYC_analyse_et_prediction.ipynb
```

## Résultats clés

- Le prix dépend fortement de l'arrondissement (Manhattan nettement au-dessus des autres) et du type de logement.
- Les annonces les plus commentées (populaires/anciennes) affichent des prix moyens plus bas, suggérant un ajustement des hôtes vers des prix plus compétitifs avec le temps.
- Forte croissance du nombre d'annonces entre 2017 et 2019, sans hausse correspondante du prix médian.
- Un modèle de régression linéaire simple (type de logement, arrondissement, disponibilité, popularité) capture une partie du signal, avec une marge d'erreur attendue vu l'absence de variables comme la taille du logement ou les équipements.

## Pistes d'amélioration

- Transformation logarithmique du prix pour réduire l'asymétrie de sa distribution.
- Modèles non linéaires (Random Forest, Gradient Boosting) pour capter les interactions entre variables.
- Utilisation de la localisation précise (quartier, distance aux points d'intérêt) plutôt que l'arrondissement seul.
- Validation croisée plutôt qu'un split unique train/validation.

## Structure du dépôt

```
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── analyse.ipynb
└── fichiers/              # données locales, non versionnées
    ├── airbnb.csv
    └── nyc.jpg
```

## Outils

Python, pandas, numpy, matplotlib, seaborn, scikit-learn.
