<!-- ![nlbse 2024](nlbse2024.png) -->

# NLBSE'24 Tool Competition on Issue Report Classification

## Team
- Gabriel Aracena, CS Student
- Kyle Luster, CS Student
- Fabio Marcos de Abreu Santos, PhD Machine Learning Professor

## Introduction

The issue report classification competition consists of building and testing a set of multi-class classification models 
to classify issue reports as belonging to one category representing the type of information they convey.

It was provided a dataset encompassing 3 thousand labeled issue reports 
(as bugs, enhancements, and questions) 
extracted from 5 real open-source projects. 
We were invited to leverage this dataset for evaluating our classification approaches and compare the achieved results against proposed baseline approaches based on Sentence-Transformers.

We tuned and evaluated the multi-class classification models using the provided training and test sets.

> Please refer to the [tool competition page](https://nlbse2024.github.io/tools/) to read more about the tool competition and learn how to participate.

## Dataset

A dataset of 3 thousand publicly-available issue reports is extracted.

Each issue report contains the following information:
- Repository
- Label
- Title
- Body

Each issue is labeled with one class that indicates the issue type, namely, `bug`, `feature`, and `question`.

Issues with multiple labels are excluded from the dataset.

The dataset is then split into a training set (50%) and a test set (50%).

> The dataset has already been extracted to avoid costs on your end, please keep reading to find hyperlinks to both the training and test set.

## Training

We utilized the OpenAI API to fine-tune the gpt-3.5-turbo model for each repository.
In total, 5 models were fine-tuned and evaluiated against its correspondent testing dataset.


## Evaluation

Submissions are evaluated based on their class-detection performance over the provided [test set](https://raw.githubusercontent.com/nlbse2024/issue-report-classification/main/data/issues_test.csv?token=GHSAT0AAAAAACG4EVQDKGFUQA2CR27PPS2SZI633MA). 
The classifier should assign one label to an issue. Just like the training set, the test set is balanced.

Participants must evaluate their project classifiers on the test set of the respective project and report the results in their submission.

**Important:** you may apply any preprocessing or feature engineering on this dataset except sampling, rebalancing, undersampling or oversampling techniques.

Repository classification performance is measured using the F1 score over all the three classes (averaged). Cross-repository performance is measured as the arithmetic mean of the five repository F1 scores.

A submission (i.e., paper) in the tool competition must provide, for each of the 5 repositories and cross-repo:
- Precision, for each class and cross-class average
- Recall, for each class and cross-class average
- F1 score, for each class and cross-class average

Cross-class aggregation can be done using both the macro and micro averaging method, the result will be the same since the dataset is balanced.

Cross-repo aggregation is done using the arithmetic mean.

Please note that whilst all of the above measures must be provided for acceptance, the submissions will **only** be ranked by their cross-repo F1 score.

> You can use the table from the baseline below as a template for your evaluation.

## Baselines

Participants are encouraged, but not required, to use the baseline as a template for their submission. Each template downloads the dataset, performs basic preprocessing, trains a set of classifiers and evaluates them on the test set.

### [SetFit]

| Repository            | Label         | Precision | Recall | F1         |
| --------------------- | ------------- | --------- | ------ | ---------- |
| facebook/react        | bug           | 0.9048    | 0.9500 | 0.9268     |
| facebook/react        | feature       | 0.8491    | 0.9000 | 0.8738     |
| facebook/react        | question      | 0.8652    | 0.7700 | 0.8148     |
| facebook/react        | average       | 0.8729    | 0.8733 | 0.8718     |
| | | | | |
| tensorflow/tensorflow | bug           | 0.9565    | 0.8800 | 0.9167     |
| tensorflow/tensorflow | feature       | 0.8558    | 0.8900 | 0.8725     |
| tensorflow/tensorflow | question      | 0.7885    | 0.8200 | 0.8039     |
| tensorflow/tensorflow | average       | 0.8669    | 0.8633 | 0.8644     |
| | | | | |
| microsoft/vscode      | bug           | 0.8485    | 0.8400 | 0.8442     |
| microsoft/vscode      | feature       | 0.7627    | 0.9000 | 0.8257     |
| microsoft/vscode      | question      | 0.8916    | 0.7400 | 0.8087     |
| microsoft/vscode      | average       | 0.8343    | 0.8267 | 0.8262     |
| | | | | |
| bitcoin/bitcoin       | bug           | 0.7604    | 0.7300 | 0.7449     |
| bitcoin/bitcoin       | feature       | 0.8723    | 0.8200 | 0.8454     |
| bitcoin/bitcoin       | question      | 0.6455    | 0.7100 | 0.6762     |
| bitcoin/bitcoin       | average       | 0.7594    | 0.7533 | 0.7555     |
| | | | | |
| opencv/opencv         | bug           | 0.7619    | 0.8000 | 0.7805     |
| opencv/opencv         | feature       | 0.8842    | 0.8400 | 0.8615     |
| opencv/opencv         | question      | 0.8100    | 0.8100 | 0.8100     |
| opencv/opencv         | average       | 0.8187    | 0.8167 | 0.8173     |
| | | | | |
| overall               | bug           | 0.8464    | 0.8400 | 0.8426     |
| overall               | feature       | 0.8448    | 0.8700 | 0.8558     |
| overall               | question      | 0.8001    | 0.7700 | 0.7827     |
| overall               | average       | 0.8305    | 0.8267 | **0.8270** |
