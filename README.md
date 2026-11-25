# Activité pratique N°4 — Architecture Transformer

TP de Deep Learning (PyTorch) : des réseaux récurrents (RNN, LSTM) au **Transformer**, puis aux modèles **GPT** et **BERT**.

## Structure

```
.
├── notebooks/                          # Première partie
│   ├── 01_dataset_serie_temporelle.ipynb   s = sin(x), 200 valeurs dans [0, 20], séquences de 10
│   ├── 02_rnn.ipynb                        RNN 16 unités → Linear(16→1)
│   ├── 03_lstm.ipynb                       LSTM 16 unités → Linear(16→1)
│   ├── 04_transformer.ipynb                Projection 1→16 + Positional Embedding + MHSA 2 têtes
│   │                                       + FFN 16→32→16 → Linear(16→1), comparaison des 3 modèles
│   ├── 05_gpt.ipynb                        GPT-2 : prédire la suite d'un texte
│   └── 06_bert.ipynb                       BERT : prédire le mot masqué (« Rabat est la [MASK] du Maroc »)
├── exercices/                          # Deuxième partie
│   ├── exercice1_energy_transformer.ipynb  Consommation électrique horaire (UCI) avec un Transformer
│   ├── exercice2_mini_gpt.ipynb            Mini-GPT par caractères entraîné depuis zéro
│   └── exercice3_mini_bert.ipynb           Mini-BERT : modélisation du langage masqué
├── data/                               corpus.txt (+ dataset UCI à télécharger, voir data/README.md)
├── ETAPES.md                           plan des commits étape par étape
└── requirements.txt
```

## Installation

```bash
python -m venv .venv
# Windows : .venv\Scripts\activate   |   Linux/Mac : source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

- Les notebooks 05 et 06 téléchargent les modèles préentraînés `gpt2` et `bert-base-multilingual-cased` (Hugging Face).
- L'exercice 1 nécessite `data/household_power_consumption.txt` (voir `data/README.md`).

## Première partie — résumé

Même tâche pour les trois modèles : prédire la valeur suivante d'une séquence de 10 valeurs de sin(x)
(150 séquences d'entraînement, 40 de test, découpage chronologique, Adam lr = 0.01, 300 époques).

| Modèle | Paramètres | MSE test | MAE test |
|---|---|---|---|
| RNN (16 unités) | 321 | 0.000028 | 0.0046 |
| LSTM (16 unités) | 1 233 | 0.000003 | 0.0014 |
| Transformer (d=16, 2 têtes) | 2 433 | 0.000006 | 0.0020 |

| | GPT | BERT |
|---|---|---|
| Architecture | Décodeur, attention **causale** | Encodeur, attention **bidirectionnelle** |
| Préentraînement | Prédire le token suivant | Retrouver des tokens masqués |
| Usage | Génération de texte | Compréhension, complétion de masque |

## Deuxième partie — résumé

### Exercice 1 — EnergyTransformer (consommation électrique horaire, UCI)

Fenêtre de 24 h → heure suivante, 2 couches encodeur (d=32, 4 têtes), meilleur modèle sur la validation.

| Modèle (test) | MAE (kW) | RMSE (kW) |
|---|---|---|
| **EnergyTransformer** | **0.340** | **0.492** |
| Persistance (h-1) | 0.389 | 0.588 |
| Référence journalière (h-24) | 0.513 | 0.764 |

Fenêtre de 168 h : gain léger (MAE 0.330 contre 0.337 kW sur les mêmes heures) pour un coût de calcul environ 15 fois plus élevé.

### Exercice 2 — Mini-GPT (caractères, 2 blocs, 4 têtes, d=64)

Entropie croisée de validation 1.96 (contre ln(55) ≈ 4.0 au hasard). La causalité est vérifiée : modifier un caractère futur ne change pas les logits passés. Comparaison des températures 0.5 / 1.0 / 1.5. Le corpus étant petit, le surapprentissage est contrôlé en gardant le meilleur modèle sur la validation.

### Exercice 3 — Mini-BERT (mots, 2 couches, 4 têtes, d=64)

Masquage 15 % (80/10/10), perte uniquement sur les positions sélectionnées. **≈ 83 % d'exactitude** sur les tokens masqués de phrases jamais vues (*le [MASK] aboie* → chien 96 %, *rabat est la [MASK] du maroc* → capitale 95 %). Le masque de padding est vérifié : changer les tokens de padding ne modifie pas les prédictions.

## Démonstration

1. `04_transformer.ipynb` : schéma de l'architecture, dimensions à chaque étape, carte d'attention, comparaison des 3 modèles.
2. `05_gpt.ipynb` / `06_bert.ipynb` : génération (« Artificial intelligence can help people... ») et mot masqué (« Rabat est la [MASK] du Maroc »).
3. Exercices : tableau MAE/RMSE vs références, vérification de la causalité (mini-GPT), vérification du padding (mini-BERT).
