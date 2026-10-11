# Prédiction des prix de l'immobilier

Projet Machine Learning, Sujet 5 (Dr Yoro DIA).
Auteur : Seydina Omar

Estimation du prix de vente de maisons à partir de leurs caractéristiques, avec le jeu de données Kaggle
« House Prices : Advanced Regression Techniques » (maisons d'Ames, Iowa).

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `projet-immo.ipynb` | Notebook : chargement, nettoyage, préparation, modèles, évaluation, compléments |
| `data_description.txt` | Description de chaque colonne du jeu de données (en anglais) |
| `livrables/` | Rapport Word et présentation PowerPoint |

## Données

Les fichiers de données ne sont pas inclus dans le dépôt. Pour reproduire le travail :

1. Télécharger `train.csv` sur la page Kaggle de la compétition « House Prices - Advanced Regression Techniques » (onglet Data).
2. Placer `train.csv` dans le même dossier que le notebook.

## Lancer le notebook

```
pip install pandas numpy matplotlib seaborn scikit-learn
jupyter notebook projet-immo.ipynb
```

Puis exécuter toutes les cellules dans l'ordre (Run, Run All Cells).

## Démarche

1. **Découverte** : 1460 maisons, 81 colonnes, cible `SalePrice`.
2. **Nettoyage** : cases vides traitées selon leur sens (absence ou donnée perdue), deux valeurs aberrantes retirées (1458 maisons restantes).
3. **Préparation** : encodage one-hot (79 variables, puis 301 colonnes), séparation 80 % / 20 % (1166 / 292 maisons).
4. **Modèles** : régression linéaire, Ridge, Lasso, forêt aléatoire, arbre de décision, réseau de neurones.
5. **Évaluation** : MAE, RMSE, R², validation croisée.

## Résultats principaux (292 maisons de test)

| Modèle | MAE (dollars) | RMSE (dollars) | R² test |
|---|---|---|---|
| Régression linéaire | 18 207 | 25 759 | 0,880 |
| **Ridge (alpha = 10), modèle retenu** | 16 807 | 23 213 | 0,902 |
| Lasso (alpha = 100) | 16 286 | 22 937 | 0,905 |
| Forêt aléatoire | 16 860 | 24 262 | 0,893 |
| Arbre de décision | 26 674 | 37 514 | 0,745 |
| Réseau de neurones | 15 581 | 22 375 | 0,909 |

Ridge est retenu car son réglage a été validé par validation croisée, sans toucher au jeu de test. Les réglages de Lasso, de l'arbre et du réseau ont été fixés après des essais examinés sur le test : leurs scores sont légèrement optimistes.

## Limite

Le modèle a appris sur des maisons d'Ames (prix en dollars, quartiers américains). Il ne peut pas estimer des biens à Ziguinchor sans être réentraîné avec des données locales.
