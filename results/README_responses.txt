
## Réponses aux questions

### Partie 1 - Bagging & Random Forest

**Pourquoi la limitation des variables à chaque nœud (max_features) améliore-t-elle la diversité des arbres par rapport à un Bagging classique ?**

Le Bagging classique réduit la corrélation entre les arbres uniquement en utilisant des bootstraps différents. Cependant, si une feature est très discriminante, tous les arbres vont la sélectionner en premier, créant des arbres fortement corrélés.

Random Forest ajoute une couche supplémentaire de diversité en sélectionnant aléatoirement un sous-ensemble de features à chaque nœud. Ainsi :
- Les arbres ne peuvent pas toujours utiliser la feature dominante
- Ils sont forcés d'explorer des features alternatives
- La corrélation entre les arbres diminue significativement
- La réduction de variance est plus efficace → meilleure généralisation

### Partie 2 - Boosting

**1. Quelle est la différence fondamentale entre Bagging et Boosting ?**

- **Bagging** (Bootstrap Aggregating) :
  - Entraîne des modèles en parallèle sur des bootstraps
  - Objectif : réduire la variance
  - Les modèles sont indépendants
  - Vote majoritaire ou moyenne simple

- **Boosting** (séquentiel) :
  - Entraîne des modèles en séquence
  - Objectif : réduire le biais
  - Chaque modèle corrige les erreurs du précédent
  - Combinaison pondérée des modèles

**2. Pourquoi AdaBoost utilise-t-il des arbres de profondeur 1 (stumps) ?**

AdaBoost s'appuie sur la théorie PAC (Probably Approximately Correct) :
- Les stumps sont des "weak learners" (juste mieux que le hasard)
- La combinaison séquentielle de stumps crée un "strong learner"
- Des arbres trop profonds annuleraient l'effet de boosting
- Cela permet une correction progressive des erreurs

**3. Quel est l'avantage de XGBoost par rapport à AdaBoost ?**

- Utilise les gradients ET les Hessiennes (optimisation 2nd ordre)
- Régularisation L1/L2 pour éviter le surapprentissage
- Gère les valeurs manquantes
- Arrêt précoce (early stopping) pour trouver le nombre optimal d'arbres
- Plus rapide et scalable (histogrammes, parallélisation)

### Partie 3 - Voting & Stacking

**1. Quelle est la différence entre Hard Voting et Soft Voting ?**

- **Hard Voting** : vote majoritaire sur les classes prédites
- **Soft Voting** : moyenne des probabilités prédites
- Soft Voting est généralement plus robuste car il utilise l'information de confiance des modèles

**2. Quels sont les avantages du Stacking par rapport au Voting ?**

- Le Stacking apprend un méta-modèle qui optimise la combinaison
- Peut capturer des relations complexes entre les prédictions
- Permet d'utiliser des modèles plus sophistiqués comme méta-modèle
- Plus flexible mais plus coûteux en temps d'entraînement

**3. Pourquoi utiliser des modèles hétérogènes dans les métamodèles ?**

- Les modèles hétérogènes ont des biais différents
- Leur combinaison réduit à la fois le biais et la variance
- Ils capturent différentes structures dans les données
- Moins de corrélation entre les erreurs → meilleure généralisation
