# Projet IA/Data Science Finance — Cartographie risque/rendement des actions du CAC 40

## Objectif
Analyser 15 actions françaises à partir de données historiques publiques Yahoo Finance et les regrouper automatiquement selon leur profil de risque et de rendement.

## Méthodes utilisées
- Statistiques descriptives
- Visualisation avec Matplotlib
- ACP avec Scikit-Learn
- Clustering K-Means
- Classification ascendante hiérarchique (CAH)

## Données
- Source : Yahoo Finance via yfinance
- Période : 2020-01-01 à 2025-12-31
- Actions : 15 grandes actions françaises
- Indice de référence : CAC 40 (^FCHI)

## Exécution
1. Installer les bibliothèques :
   ```bash
   pip install -r requirements.txt
   ```

2. Lancer les notebooks dans l'ordre :
   - notebooks/01_collecte_donnees.ipynb
   - notebooks/02_statistiques_descriptives.ipynb
   - notebooks/03_acp_clustering.ipynb

## Résultat attendu
À la fin, vous obtenez :
- data/brut/prix_actions.csv
- data/obtenue/rendements_journaliers.csv
- data/obtenue/indicateurs_actions.csv
- figures/*.png
- rapport/rapport.md à compléter