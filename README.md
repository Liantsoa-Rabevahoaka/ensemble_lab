# Laboratoire : Algorithmes d'Ensemble

## Description

Exploration des méthodes d'ensemble (Bagging, Boosting, Voting, Stacking) pour la classification binaire.

## Installation

```bash
python -m venv .venv
source .venv/bin/activate
pip install numpy pandas matplotlib scikit-learn xgboost
```

## Exécution

Lancer le notebook : `notebooks/lab_ensemble.ipynb`

---

## Résultats

### Tableau récapitulatif des performances

| Modèle | Accuracy (Test) | Temps (s) | Observations |
|--------|----------------|-----------|--------------|
| Arbre seul | 95.87% | 0.240 | Fort surapprentissage (train ~100%) |
| Bagging manuel | 94.00% | 0.926 | Réduction du surapprentissage, bonne généralisation |
| Random Forest | 94.80% | 0.423 | Très bonne généralisation, stable |
| AdaBoost | 81.87% | 0.241 | Bon compromis, sensible au learning_rate |
| XGBoost | 95.87% | 0.542 | Performances élevées, régularisation intégrée |
| Hard Voting | 95.60% | 1.221 | Robuste, combine les décisions |
| Soft Voting | 95.33% | 1.379 | Utilise les probabilités, plus précis |
| Stacking | **96.40%** | 4.356 | Apprend la meilleure combinaison des modèles |

### Classement

| # | Modèle | Accuracy |
|---|--------|----------|
| 1 | **Stacking** | **96.40%** |
| 2 | Arbre seul | 95.87% |
| 3 | XGBoost | 95.87% |
| 4 | Hard Voting | 95.60% |
| 5 | Soft Voting | 95.33% |
| 6 | Random Forest | 94.80% |
| 7 | Bagging manuel | 94.00% |
| 8 | AdaBoost | 81.87% |

---

## Questions de réflexion

### Partie 1 - Bagging & Random Forest

**Pourquoi la limitation des variables à chaque nœud (`max_features`) améliore-t-elle la diversité des arbres par rapport à un Bagging classique ?**

Dans le Bagging classique, les arbres sont entraînés sur des bootstraps différents mais si une feature est très discriminante, tous l'utilisent en premier → arbres corrélés.

Random Forest sélectionne aléatoirement un sous-ensemble de features à chaque nœud :

- Les arbres ne peuvent pas toujours utiliser la feature dominante.
- Ils explorent des features alternatives.
- La corrélation diminue → meilleure réduction de variance.

### Partie 2 - Boosting

**1. Quelle est la différence fondamentale entre Bagging et Boosting ?**

| Aspect | Bagging | Boosting |
|--------|---------|----------|
| Entraînement | Parallèle | Séquentiel |
| Objectif | Réduire la variance | Réduire le biais |
| Modèles | Indépendants | Dépendants |
| Agrégation | Vote majoritaire | Combinaison pondérée |

**2. Pourquoi AdaBoost utilise-t-il des arbres de profondeur 1 (stumps) ?**

AdaBoost se base sur la théorie PAC : les stumps sont des "weak learners" (juste mieux que le hasard). Leur combinaison séquentielle crée un "strong learner". Des arbres trop profonds annuleraient l'effet de boosting.

**3. Quel est l'avantage de XGBoost par rapport à AdaBoost ?**

- Optimisation 2nd ordre (gradients + Hessiennes).
- Régularisation L1/L2 contre le surapprentissage.
- Gestion des valeurs manquantes.
- Early stopping.
- Plus rapide et scalable.

### Partie 3 - Voting & Stacking

**1. Quelle est la différence entre Hard Voting et Soft Voting ?**

- **Hard Voting** : vote majoritaire sur les classes prédites.
- **Soft Voting** : moyenne des probabilités (plus robuste car utilise la confiance).

**2. Quels sont les avantages du Stacking par rapport au Voting ?**

- Apprend la meilleure combinaison des modèles.
- Capture des relations complexes entre les prédictions.
- Plus flexible (tout méta-modèle possible).
- Performance supérieure (96.40% vs 95.60%).

**3. Pourquoi utiliser des modèles hétérogènes dans les métamodèles ?**

- Biais différents → complémentarité.
- Réduction simultanée du biais et de la variance.
- Capture de structures différentes dans les données.
- Moins de corrélation entre les erreurs.

---

## Conclusion

**🏆 Meilleur modèle : Stacking avec 96.40% d'accuracy**

Le Stacking surpasse tous les autres modèles en apprenant la combinaison optimale des prédictions. Les méthodes de Bagging (Random Forest) offrent un bon équilibre performance/temps, tandis que XGBoost se montre très performant avec régularisation intégrée.

## Auteur

Liantsoa RABEVAHOAKA - 31 août 2026

**C'est tout !** 🎉
