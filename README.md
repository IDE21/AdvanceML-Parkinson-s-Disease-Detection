# Parkinson's Disease Detection from Voice Features

Tree-based classifiers (Decision Tree, Random Forest, Gradient Boosting) that predict Parkinson's disease from 22 voice measurements such as fundamental frequency, jitter and shimmer.

> ⚠️ **Research and education only.** This is not a medical device and must not be used for clinical diagnosis.

## Results (80/20 split, reported in the notebook)

| Model | Train acc. | Test acc. | Validation acc. |
|---|---|---|---|
| Decision Tree | 0.996 | 0.975 | 0.967 |
| Random Forest | 1.000 | 0.987 | 0.977 |
| Gradient Boosting | 1.000 | 0.983 | 0.977 |

Read these numbers together with the limitations below.

## Dataset (`data/dataset.csv`)

- 1,195 rows × 24 columns: `name` (recording ID), 22 voice features, and the target `status`.
- The first 195 rows match the format of the [UCI Parkinson's dataset](https://archive.ics.uci.edu/dataset/174/parkinsons) (recordings from 32 people). The other 1,000 rows appear to be synthetic: their `status` values are fractions between 0 and 1 rather than 0/1.

## Limitations

1. **Synthetic rows:** `status` is not binary for 1,000 rows, so the binary-classification setup needs a clear rule for these rows (or they should be removed).
2. **Subject leakage:** each person has several recordings. A random row split puts the same person in train and test, which inflates accuracy. A grouped split by subject (`S01`, `S02`, …) gives a fairer estimate.
3. Train accuracy of 1.000 shows the models overfit.

Planned: re-run with only the 195 real recordings and a subject-grouped split.

## Run it

```bash
pip install -r requirements.txt
jupyter notebook "Parkinson's_Disease.ipynb"
```

The notebook was written for Colab and reads `/content/dataset.csv`. Locally, change that path to `data/dataset.csv`.

## License

Code: [MIT](LICENSE). The original voice data is from the UCI Machine Learning Repository (Little et al., 2008).
