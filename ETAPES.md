# Plan des étapes (un commit + un push par étape)

Chaque étape = exécuter le notebook, vérifier les résultats, puis `git add` des fichiers listés, `git commit`, `git push`.
Ne jamais ajouter une étape avant que la précédente soit poussée.
`README_final.md` reste hors de git jusqu'à l'étape 10.

## Préparation (une seule fois)

1. Créer un dépôt **vide** sur GitHub (sans README), par ex. `tp-architecture-transformer`.
2. Dans ce dossier :
```bash
git init -b main
git remote add origin https://github.com/<ton-compte>/tp-architecture-transformer.git
```
3. Placer `household_power_consumption.txt` dans `data/` (ignoré par git).

## Étapes

| # | Fichiers à ajouter | Message de commit |
|---|---|---|
| 0 | `README.md` `ETAPES.md` `CLAUDE.md` `requirements.txt` `.gitignore` `data/README.md` | `Étape 0 : initialisation du projet` |
| 1 | `notebooks/01_dataset_serie_temporelle.ipynb` | `Étape 1 : génération de la série temporelle sin(x) et séquences de 10` |
| 2 | `notebooks/02_rnn.ipynb` | `Étape 2 : modèle RNN (création, entraînement, test)` |
| 3 | `notebooks/03_lstm.ipynb` | `Étape 3 : modèle LSTM (création, entraînement, test)` |
| 4 | `notebooks/04_transformer.ipynb` | `Étape 4 : modèle Transformer + comparaison RNN/LSTM/Transformer` |
| 5 | `notebooks/05_gpt.ipynb` | `Étape 5 : génération de texte avec GPT-2` |
| 6 | `notebooks/06_bert.ipynb` | `Étape 6 : prédiction de mot masqué avec BERT` |
| 7 | `exercices/exercice1_energy_transformer.ipynb` | `Exercice 1 : EnergyTransformer sur la consommation électrique` |
| 8 | `data/corpus.txt` `exercices/exercice2_mini_gpt.ipynb` | `Exercice 2 : mini-GPT par caractères` |
| 9 | `exercices/exercice3_mini_bert.ipynb` | `Exercice 3 : mini-BERT (modélisation du langage masqué)` |
| 10 | `README.md` (remplacé par `README_final.md` : `mv README_final.md README.md`) | `README : résumé des résultats et plan de démonstration` |

Commandes type (étape 2) :

```bash
jupyter nbconvert --to notebook --execute --inplace notebooks/02_rnn.ipynb
git add notebooks/02_rnn.ipynb
git commit -m "Étape 2 : modèle RNN (création, entraînement, test)"
git push   # à l'étape 0 : git push -u origin main
```
