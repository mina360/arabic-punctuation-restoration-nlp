# Arabic Punctuation Restoration using NLP

An NLP project for restoring punctuation marks in Arabic text using sequence labeling models, classical deep learning architectures, pretrained embeddings, and transformer-based transfer learning.

## Project Overview

This project was developed as part of a fifth-year Natural Language Processing course.

The goal of the project is to predict missing punctuation marks in Arabic text. Given an Arabic sentence without punctuation, the model predicts the punctuation mark that should appear after each token.

The task is formulated as a token-level sequence labeling problem.

## Target Punctuation Marks

The project predicts the following labels:

```txt
_   No punctuation
،   Comma
؛   Semicolon
:   Colon
؟   Question mark
!   Exclamation mark
.   Period
```

## Main Features

* Arabic text normalization and preprocessing.
* Handling Arabic punctuation variants.
* Removing diacritics.
* Normalizing Arabic letters and digits.
* Handling UN document codes and special formatting cases.
* Lazy loading and streaming over large text files.
* Train/validation split at file level to reduce data leakage.
* Exploratory Data Analysis before and after cleaning.
* Vocabulary building from training data only.
* Token-level label extraction.
* Sequence chunking and padding.
* Class weighting for imbalanced punctuation labels.
* Inference function for restoring punctuation in new Arabic text.

## Models Implemented

### 1. BiLSTM with Random Embeddings

A baseline sequence labeling model using trainable random embeddings.

### 2. BiLSTM with FastText Arabic Embeddings

A BiLSTM model initialized with pretrained Arabic FastText embeddings.

Two settings were explored:

* Frozen FastText embeddings.
* Fine-tuned FastText embeddings.

### 3. BiLSTM + CRF

A BiLSTM model with a Conditional Random Field layer to model dependencies between output labels.

### 4. Transformer-based Token Classification

Transfer learning using pretrained Arabic transformer models, including:

* AraBERT
* CAMeLBERT

The transformer models were fine-tuned for token classification.

## Dataset

The project uses an Arabic punctuation dataset based on UN Arabic text data.

The dataset is not included in this repository due to size considerations.
The notebook includes the required commands for downloading and preparing the dataset in Google Colab.

## Evaluation

The models were evaluated using:

* Accuracy
* Macro F1-score
* Weighted F1-score
* Punctuation-only F1-score
* Confusion matrix
* Classification report

## Reported Results

The best transformer-based experiments achieved strong performance on the validation/test split.

Example reported results:

| Model                      | Accuracy | Overall Macro F1 | Punctuation-only Macro F1 | Present Punctuation Macro F1 |
| -------------------------- | -------: | ---------------: | ------------------------: | ---------------------------: |
| CAMeLBERT Mix              |   0.9717 |           0.7078 |                    0.6965 |                       0.7937 |
| AraBERTv2                  |   0.9727 |           0.7072 |                    0.6970 |                       0.7928 |
| CAMeLBERT Classical Arabic |   0.9707 |           0.7060 |                    0.6902 |                       0.7914 |

> Note: Accuracy is high because the no-punctuation label is very frequent.
> Punctuation-only F1 and present-punctuation macro F1 are more informative for this task.

## Project Structure

```txt
arabic-punctuation-restoration-nlp/
  notebooks/
    arabic_punctuation_restoration.ipynb

  README.md
  requirements.txt
  .gitignore
```

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/mina360/arabic-punctuation-restoration-nlp.git
cd arabic-punctuation-restoration-nlp
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Open the notebook:

```bash
jupyter notebook notebooks/arabic_punctuation_restoration.ipynb
```

Or run it directly on Google Colab.

## Notes

* The notebook was developed and trained mainly on Google Colab.
* Some cells use Google Drive paths for saving vocabularies, models, and intermediate files.
* The trained model checkpoint is not included in the repository.
* The dataset and FastText embeddings are downloaded or prepared inside the notebook.
* This is an academic NLP project, not a production-ready punctuation restoration service.

## Example Use Case

Input text without punctuation:

```txt
هل يمكنني السفر غدا اريد معرفة حالة الطقس
```

Expected output:

```txt
هل يمكنني السفر غدا؟ أريد معرفة حالة الطقس.
```

## Disclaimer

This project is intended for educational and research purposes. The restored punctuation may not always be linguistically perfect, especially for long, ambiguous, or domain-specific Arabic texts.
