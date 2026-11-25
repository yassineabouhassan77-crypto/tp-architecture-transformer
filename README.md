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

## Avancement

Voir `ETAPES.md` : le projet est publié étape par étape.
