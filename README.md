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

> The dataset has already been extracted by the commitee of the competition.

## Training

We utilized the OpenAI API to fine-tune the gpt-3.5-turbo model for each repository.
In total, 5 models were fine-tuned and evaluiated against its correspondent testing dataset.

## Reproducibility

To reproduce the results one will need to create an OpenAI API key. If you don't have an OpenAI account, create one for free. Then go to https://platform.openai.com/docs/overview on the left side select "API Keys". Then click on "+ Create new secret key" and name it how you want. After the key is created you can paste it in [jupyter notebook](issueclassificationgpt.ipynb) where it says "open-ai-key" on cells 11 and 47. Since jupyter notebooks save the outputs and results there is no need to create your own open ai key though.

**Please follow the instructions in the markdown on the Jupyter Notebook. DO NOT press "Run all cells" doing that won't work since a lot of cells will depend on API calls that take some time to process, even after it is executed.** 

## Results

### [Open AI API]

| Repository            | Label         | Precision | Recall | F1         |
| --------------------- | ------------- | --------- | ------ | ---------- |
| facebook/react        | bug           | 0.8333    | 0.9500 | 0.8878     |
| facebook/react        | feature       | 0.8557    | 0.8900 | 0.8725     |
| facebook/react        | question      | 0.9024    | 0.7400 | 0.8132     |
| facebook/react        | average       | 0.8635    | 0.8600 | 0.8579     |
| | | | | |
| tensorflow/tensorflow | bug           | 0.9072    | 0.8800 | 0.8934     |
| tensorflow/tensorflow | feature       | 0.9318    | 0.8200 | 0.8723     |
| tensorflow/tensorflow | question      | 0.7913    | 0.9100 | 0.8465     |
| tensorflow/tensorflow | average       | 0.8768    | 0.8700 | 0.8708     |
| | | | | |
| microsoft/vscode      | bug           | 0.8511    | 0.8000 | 0.8247     |
| microsoft/vscode      | feature       | 0.8131    | 0.8700 | 0.8406     |
| microsoft/vscode      | question      | 0.7980    | 0.7900 | 0.7938     |
| microsoft/vscode      | average       | 0.8207    | 0.8200 | 0.8198     |
| | | | | |
| bitcoin/bitcoin       | bug           | 0.7339    | 0.8000 | 0.7656     |
| bitcoin/bitcoin       | feature       | 0.8318    | 0.8900 | 0.8599     |
| bitcoin/bitcoin       | question      | 0.7381    | 0.6200 | 0.6739     |
| bitcoin/bitcoin       | average       | 0.7679    | 0.7700 | 0.7665     |
| | | | | |
| opencv/opencv         | bug           | 0.7288    | 0.8600 | 0.7890     |
| opencv/opencv         | feature       | 0.9091    | 0.8000 | 0.8511     |
| opencv/opencv         | question      | 0.8617    | 0.8100 | 0.8351     |
| opencv/opencv         | average       | 0.8332    | 0.8233 | 0.8250     |
| | | | | |
| overall               | bug           | 0.8109    | 0.8580 | 0.8321     |
| overall               | feature       | 0.8683    | 0.8540 | 0.8593     |
| overall               | question      | 0.8183    | 0.7740 | 0.7925     |
| overall               | average       | 0.8324    | 0.8287 | **0.8280** |

## Baselines

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
