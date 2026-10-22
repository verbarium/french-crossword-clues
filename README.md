# French Crossword Clues

**English first, version française complète plus bas.**

## French Crossword Clues With Verified Answers

Merle, 9 letters, PASSEREAU. Belote bridgée, 7 letters, COINCHE. Maire en espagnol, 7 letters, ALCALDE.

That is what a French *mots fléchés* clue looks like. A few words, a number of cells, and one expected word. This dataset gathers **10,000 of these clues** with **17,309 answers checked by hand**. It is the first public French clue–answer collection of this kind on Hugging Face. English has had large crossword corpora for years (New York Times clues, cryptic clue archives, research benchmarks). French had none, and researchers who built a French crossword solver said so in their paper.

The data comes from [La Petite Case](https://www.lapetitecase.fr), a free French website that helps people finish their grids. On the site, each clue has its own page with every possible answer sorted by number of letters. What you get here is a sample of that work, chosen at random among the pages whose answers were fully reviewed.

### Mots Fléchés In Two Lines

*Mots fléchés* (arrow-words) are the most popular word puzzle in France. Clues sit inside the grid, in cells with small arrows pointing to where the answer goes. They are shorter and more playful than British cryptics and closer to American crosswords. A single clue often accepts several answers of different lengths. « Abri pour les animaux » can be NICHE, ÉTABLE or REFUGE, so the number of letters matters as much as the meaning.

### What Is In The File

| | |
|---|---|
| Clues | 10,000 distinct French clues |
| Rows | 17,309 clue → answer pairs |
| Answer length | 2 to 15 letters |
| Split | `train` (about 90 %) and `test` (about 10 %), split by clue, stable across versions |
| Language | French |

A few rows picked at random.

| clue | answer_display | length |
|---|---|---|
| Lac glaciaire | BOURGET | 7 |
| Une bicoque | CAHUTE | 6 |
| Lutin en anglais | GOBLIN | 6 |
| Chili ville | SANTIAGO | 8 |
| 1000 gigaoctets | TÉRAOCTET | 9 |
| Baraquée | BALÈZE | 6 |
| Abbé de Cluny | ODILON | 6 |

### Where The Clues And Answers Come From

The clues are real searches. When people get stuck on a grid, they type the clue into a search engine, sometimes with the number of letters. We collected these queries and kept the ones that read like genuine grid clues. That explains the style, short and elliptic, sometimes with a missing accent or a word that only makes sense inside a grid.

Answers were first generated from open French lexical resources, then scored. After that, each page went through three passes, a full review, a second review made blind (without seeing the first verdicts), and a final arbitration when the two disagreed. Only answers rated **strong** made it into this file. Uncertain answers, "possible" answers and rejected ones were left out. A clue keeps all its strong answers, which is why some clues have one row and others have five.

Every answer is written twice.
- `answer` is the grid form, capitals A to Z, no accents, no spaces, no hyphens, exactly as you would fill the cells.
- `answer_display` is the correct spelling, such as TÉRAOCTET, SOIXANTE-QUATRE or À JAMAIS.

### Columns

| column | description |
|---|---|
| `clue_id` | Stable clue identifier |
| `clue` | The clue as searched by solvers, with light spelling fixes |
| `answer` | Grid form of the answer (A–Z only) |
| `answer_display` | Answer with accents, hyphens and spaces |
| `length` | Number of letters in `answer`, which is the number of cells |
| `answer_words` | Number of words in `answer_display` |
| `category` | Clue type from a keyword rule (`general`, `geography`, `person`, `plant_animal`, `abbreviation`) |
| `split` | `train` or `test` |
| `url` | The clue's page on lapetitecase.fr, with every answer by length |

Read the file with `pd.read_csv(path, keep_default_na=False)`. Without it, pandas turns real answers like `NA` (sodium) or `NONE` into missing values.

### What You Can Do With It

- **Solve clues under a length constraint.** Give a model `clue` and `length` and ask for the word. Score exact match at rank 1 and in the top 5 on `test`.
- **Test LLMs in French.** Grid clues mix synonyms, puns, general knowledge, foreign words, conjugated verbs and abbreviations. A model has to understand French, not just translate it.
- **Build a reverse dictionary.** Go from a short French definition to the word it describes.
- **Generate crosswords.** Use clue and answer pairs that sound like a human wrote them.
- **Study French lexicon and polysemy.** One word has many clues, and one clue has many words.

The [starter notebook](https://www.kaggle.com/code/cuivrax/french-crossword-clues-solver-baseline) has a simple baseline, TF-IDF on character n-grams, then the nearest train clue whose answer has the right length. It gets **5.6 % at rank 1 and 9 % in the top 5**. Surface similarity barely helps here, so a better model has plenty of room.

### Limitations

This is a sample, not the full answer list. A clue can have other valid answers that are not here. Some clues are very short (« Merle », « Creton ») and stay ambiguous without the crossing letters. The `category` column comes from keywords, not from manual tagging, so most clues end up in `general`.

### License And Citation

**CC BY 4.0.** Use it, share it, adapt it, commercially or not. Just credit **La Petite Case** with a link to **[lapetitecase.fr](https://www.lapetitecase.fr)**.

```bibtex
@misc{lapetitecase_mots_fleches_2026,
  title  = {Mots fl\'ech\'es d\'efinitions, French crossword clues with verified answers},
  author = {{La Petite Case}},
  year   = {2026},
  url    = {https://www.lapetitecase.fr},
  note   = {Hugging Face dataset}
}
```

Companion dataset, **[Dictionnaire Mots Fléchés | French Crosswordese](https://huggingface.co/datasets/lapetitecase/dictionnaire-mots-fleches)**, the 2,000 short words that fill French grids.

---

### Try It And Find It Elsewhere

Search every clue of this dataset in the free [French Crossword Solver](https://huggingface.co/spaces/lapetitecase/french-crossword-solver) Space. The same data is also on [Kaggle](https://www.kaggle.com/datasets/cuivrax/mots-fleches-definitions-french-crossword-clues), with a starter notebook and a baseline. Companion dataset, [Dictionnaire Mots Fléchés](https://huggingface.co/datasets/lapetitecase/dictionnaire-mots-fleches).

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1D-ir6m01Q19pgKi2-QdZGvR2Fa-cKyIE)

Run the starter notebook in [Google Colab](https://colab.research.google.com/drive/1D-ir6m01Q19pgKi2-QdZGvR2Fa-cKyIE) in one click, no account or key needed to load the data.

---

## Version Française

### Définitions De Mots Fléchés Et Leurs Solutions Vérifiées

Merle, en 9 lettres, PASSEREAU. Belote bridgée, en 7 lettres, COINCHE. Maire en espagnol, en 7 lettres, ALCALDE.

Voilà à quoi ressemble une définition de mots fléchés. Quelques mots, un nombre de cases, un mot attendu. Ce jeu de données réunit **10 000 définitions de mots fléchés et de mots croisés** avec **17 309 réponses vérifiées à la main**. C'est le premier recueil public de ce genre en français sur Hugging Face. L'anglais dispose depuis longtemps de gros corpus de grilles. Le français n'en avait aucun, et les chercheurs qui ont conçu un solveur de mots croisés français l'ont eux-mêmes écrit.

Les données viennent de [La Petite Case](https://www.lapetitecase.fr), un site gratuit d'aide aux mots fléchés et aux mots croisés. Sur le site, chaque définition a sa page, avec toutes les solutions possibles classées par nombre de lettres. Ce fichier en est un échantillon, tiré au hasard parmi les pages dont les réponses ont été entièrement relues.

### Les Mots Fléchés En Deux Mots

Les mots fléchés sont le jeu de lettres le plus joué en France. Les définitions sont écrites dans la grille, dans des cases dont les flèches indiquent où placer la réponse. Une même définition admet souvent plusieurs solutions de longueurs différentes. « Abri pour les animaux » peut donner NICHE, ÉTABLE ou REFUGE, le nombre de lettres compte donc autant que le sens. C'est pour ça que les cruciverbistes cherchent toujours la définition avec le nombre de lettres.

### Contenu Du Fichier

| | |
|---|---|
| Définitions | 10 000 définitions distinctes |
| Lignes | 17 309 couples définition → réponse |
| Longueur des réponses | 2 à 15 lettres |
| Découpage | `train` (environ 90 %) et `test` (environ 10 %), par définition, stable d'une version à l'autre |
| Langue | français |

Quelques exemples. Lac glaciaire → BOURGET, Une bicoque → CAHUTE, Lutin en anglais → GOBLIN, Chili ville → SANTIAGO, 1000 gigaoctets → TÉRAOCTET, Baraquée → BALÈZE, Abbé de Cluny → ODILON.

### D'Où Viennent Les Définitions Et Les Solutions

Les définitions sont de vraies recherches. Quand un joueur bloque sur sa grille, il tape la définition dans un moteur de recherche, parfois avec le nombre de lettres. Nous avons gardé les requêtes qui ressemblent à de vraies définitions de grille. D'où leur style, court et elliptique, parfois sans accent, parfois compréhensible seulement dans une grille.

Les réponses ont d'abord été générées à partir de ressources lexicales françaises ouvertes, puis notées. Chaque page est ensuite passée trois fois, avec une relecture complète, une seconde relecture à l'aveugle (sans voir les premiers verdicts), puis un arbitrage en cas de désaccord. Seules les réponses jugées **sûres** sont dans ce fichier. Les réponses incertaines, simplement possibles ou refusées n'y sont pas. Une définition garde toutes ses réponses sûres, certaines ont donc une ligne et d'autres cinq.

Chaque réponse est écrite deux fois.
- `answer` est la forme de grille, en majuscules de A à Z, sans accents, espaces ni traits d'union, comme on remplit les cases.
- `answer_display` est la bonne graphie, par exemple TÉRAOCTET, SOIXANTE-QUATRE ou À JAMAIS.

### Colonnes

| colonne | description |
|---|---|
| `clue_id` | Identifiant stable de la définition |
| `clue` | La définition telle que cherchée par les joueurs, orthographe légèrement corrigée |
| `answer` | Forme de grille de la réponse (A à Z) |
| `answer_display` | Réponse avec accents, traits d'union et espaces |
| `length` | Nombre de lettres de `answer`, donc nombre de cases |
| `answer_words` | Nombre de mots de `answer_display` |
| `category` | Type de définition par mots-clés (`general`, `geography`, `person`, `plant_animal`, `abbreviation`) |
| `split` | `train` ou `test` |
| `url` | Page de la définition sur lapetitecase.fr, avec toutes les solutions par nombre de lettres |

Lisez le fichier avec `pd.read_csv(path, keep_default_na=False)`. Sans cette option, pandas transforme de vraies réponses comme `NA` (le sodium) ou `NONE` en valeurs manquantes.

### À Quoi Ça Sert

- **Résoudre une définition avec un nombre de lettres imposé.** On donne `clue` et `length` au modèle, il doit trouver le mot. On mesure la bonne réponse au premier rang et dans les cinq premières sur `test`.
- **Tester des modèles de langue en français.** Les définitions de mots fléchés mélangent synonymes, jeux de mots, culture générale, mots étrangers, verbes conjugués et abréviations. Il faut comprendre le français, pas seulement le traduire.
- **Construire un dictionnaire inverse**, d'une courte définition française au mot qu'elle décrit.
- **Générer des grilles de mots fléchés ou de mots croisés** avec des définitions qui sonnent juste.
- **Étudier le lexique français et la polysémie.** Un mot a plusieurs définitions, et une définition plusieurs mots.

Le [carnet de démarrage](https://www.kaggle.com/code/cuivrax/french-crossword-clues-solver-baseline) propose une base simple, un TF-IDF sur les n-grammes de caractères, puis la définition d'entraînement la plus proche dont la réponse a la bonne longueur. Elle trouve **5,6 % des réponses au premier rang et 9 % dans les cinq premières**. La ressemblance de surface ne suffit presque jamais.

### Limites

C'est un échantillon, une définition peut donc avoir d'autres bonnes réponses absentes ici. Certaines définitions sont très courtes (« Merle », « Creton ») et restent ambiguës sans les lettres croisées. La colonne `category` vient de mots-clés, pas d'un étiquetage manuel, et la plupart des définitions tombent donc dans `general`.

### Licence Et Citation

**CC BY 4.0.** Vous pouvez utiliser, partager et adapter ces données, y compris pour un usage commercial, en citant **La Petite Case** avec un lien vers **[lapetitecase.fr](https://www.lapetitecase.fr)**.

Jeu associé, **[Dictionnaire Mots Fléchés | French Crosswordese](https://huggingface.co/datasets/lapetitecase/dictionnaire-mots-fleches)**, les 2 000 mots courts qui remplissent les grilles.

### Essayer Et Retrouver Les Données

Toutes les définitions de ce jeu se cherchent dans le Space gratuit [Solution Mots Fléchés](https://huggingface.co/spaces/lapetitecase/french-crossword-solver). Les mêmes données sont aussi sur [Kaggle](https://www.kaggle.com/datasets/cuivrax/mots-fleches-definitions-french-crossword-clues), avec un carnet de démarrage.

Lancez le carnet de démarrage dans [Google Colab](https://colab.research.google.com/drive/1D-ir6m01Q19pgKi2-QdZGvR2Fa-cKyIE) en un clic, sans compte ni clé pour charger les données.


---

**Part of [Verbarium](https://github.com/verbarium)**, open word data for word games and language tools. Data by [La Petite Case](https://www.lapetitecase.fr/). Also on [Kaggle](https://www.kaggle.com/datasets/cuivrax/mots-fleches-definitions-french-crossword-clues) and [Hugging Face](https://huggingface.co/datasets/lapetitecase/mots-fleches-definitions).
