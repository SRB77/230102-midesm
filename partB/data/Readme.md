

# Dataset Information

## Why this folder contains a toy dataset

The experiments in **Task 2 and Task 3** use a **toy subset of the IMDB movie review dataset** instead of the full dataset.

The original IMDB dataset contains **25,000 training reviews and 25,000 testing reviews**, which is unnecessarily large for a reproduction assignment. To make experiments faster and easier to reproduce, a smaller dataset was created.

The toy dataset contains **2000 randomly sampled reviews** from the IMDB training set.

This subset is sufficient to demonstrate the **feature weighting schemes and sentiment classification experiments** implemented in this project.

---

## Original Dataset Source

The dataset used in this project comes from the **IMDB Movie Review Dataset** available through the HuggingFace datasets library.

> Maas, A. L., Daly, R. E., Pham, P. T., Huang, D., Ng, A. Y., & Potts, C. (2011)
> *Learning Word Vectors for Sentiment Analysis.*
> ACL 2011.

HuggingFace dataset page:

[https://huggingface.co/datasets/imdb](https://huggingface.co/datasets/imdb)

The full dataset contains:

| Split    | Samples |
| -------- | ------- |
| Training | 25,000  |
| Testing  | 25,000  |

Each review is labeled with sentiment:

| Label | Meaning         |
| ----- | --------------- |
| 1     | Positive review |
| 0     | Negative review |

---

## How the Toy Dataset Was Created

The toy dataset is created in **Task 2.1** using the following steps:

1. Load the IMDB dataset using the HuggingFace `datasets` library.
2. Convert the dataset into a pandas DataFrame.
3. Randomly sample **2000 reviews** from the training set.
4. Save the sampled dataset as a CSV file.

Example code used in `task_2_1.ipynb`:

```python
from datasets import load_dataset
import pandas as pd

dataset = load_dataset("imdb")
train_data = dataset["train"]

df = pd.DataFrame({
    "review": train_data["text"],
    "sentiment": train_data["label"]
})

toy_df = df.sample(n=2000, random_state=42)

toy_df.to_csv("data/imdb_toy_dataset.csv", index=False)
```

The `random_state=42` ensures that the same subset is generated every time, making the experiments reproducible.

---

## Dataset Location

The generated dataset is stored in this folder as:

```text
data/imdb_toy_dataset.csv
```

All experiment notebooks (`task_2_2.ipynb`, `task_2_3.ipynb`, `task_3_1.ipynb`, and `task_3_2.ipynb`) load the dataset from this file.

---

## Reproducibility

To regenerate the dataset from scratch:

1. Install dependencies from `requirements.txt`.
2. Run the notebook:

```text
task_2_1.ipynb
```

Running this notebook will automatically:

* download the IMDB dataset
* create the toy subset
* save it to `data/imdb_toy_dataset.csv`

No manual dataset download is required.

