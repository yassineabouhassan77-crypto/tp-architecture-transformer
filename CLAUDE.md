# Instructions pour Claude Code

Projet : TP « Activité pratique N°4 — Architecture Transformer » (EMSI, filière Data & IA), en PyTorch.
Langue du projet : **français** (code commenté, markdown, messages de commit).

## Règle principale : une étape à la fois

Le dépôt est publié sur GitHub **étape par étape**. Le plan est dans `ETAPES.md`.

Quand l'utilisateur dit « fais l'étape N » :
1. Vérifier avec `git log --oneline` que l'étape N-1 est déjà commitée et poussée. Sinon, s'arrêter et le dire.
2. Exécuter le ou les notebooks de l'étape :
   `jupyter nbconvert --to notebook --execute --inplace <notebook>`
   (depuis la racine du dépôt ; les notebooks lisent les données dans `data/`).
3. Lire les sorties : vérifier qu'il n'y a pas d'erreur et résumer les résultats (pertes, MSE/MAE, exemples générés).
4. `git add` **uniquement** les fichiers listés pour l'étape N dans `ETAPES.md`.
5. `git commit -m "<message de ETAPES.md>"` puis `git push`.
6. Expliquer en 5 lignes ce que fait l'étape, pour que l'utilisateur puisse le présenter en démonstration.

Ne jamais ajouter les fichiers d'une étape future (dont `README_final.md` avant l'étape 10), ne jamais faire `git add .`, ne jamais modifier les dates de commit.

## Environnement

```bash
python -m venv .venv
# Windows : .venv\Scripts\activate   |   Linux/Mac : source .venv/bin/activate
pip install -r requirements.txt
```

- Étapes 5 et 6 téléchargent `gpt2` et `bert-base-multilingual-cased` depuis Hugging Face (connexion Internet requise).
- Exercice 1 a besoin de `data/household_power_consumption.txt` (~130 Mo, ignoré par git, voir `data/README.md`).
- Tout tourne sur CPU. L'exercice 1 avec la fenêtre 168 h est le plus long ; mettre `LANCER_168 = False` pour le sauter.
