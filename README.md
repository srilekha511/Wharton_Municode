# WhartonMunicode
A repository built off of [Andrej Karpathy's nanoGPT](https://github.com/karpathy/nanoGPT): a smaller scale version of ChatGPT able to run on your personal computer. 

This repository is part of a project at the Wharton School of the University of Pennsylvania aiming to adopt large language models - such as ChatGPT - for use in the legal space. It aims to lay foundational work for future implementation in this area. 

WhartonMunicode is designed, as the name suggests, to accept municipal codes as input. Input text to train the nanoGPT model was taken from [municode](https://library.municode.com/), a library containing over 3300 municipal codes for towns across the country. Below are beginner-friendly instructions for setting up and training the model on your own device. 

# Setup

These setup instructions are compatible for setting up and running this repository with Google Colab. However, these instructions nearly remain the same for setup in Jupyter Notebook or any other platform. 

First, mount Google Drive onto the Colab interface. This is necessary to facilitate the cloning of the repository. If you are working on Jupyter Notebook or any other platform, skip this step (Jupyter is based on the local files of your computer, not a cloud platform)

```
from google.colab import drive
drive.mount('/content/drive')
```

# Packages in Use

This repository implements the same packages as nanoGPT:

- [transformers](https://pypi.org/project/transformers/): HuggingFace package, contains pretrained models to perform tasks on text, vision, and audio
- [datasets](https://pypi.org/project/datasets/): HuggingFace package, allows for more efficient data pre-processing
- [tiktoken](https://github.com/openai/tiktoken): OpenAI's BPE tokenizer, takes in data and separates it into tokens for training
- [tqdm](https://tqdm.github.io/): Python package for progress bars
- [wandb](https://wandb.ai/site): "Weights and Biases", primarily used to track metrics such as accuracy and loss during model training and evaluation
- [numpy](https://numpy.org/): Essential Python library to operate on datasets in multidimensional array or matrix form
- [httpx](https://www.python-httpx.org/): Python web client package used to get data from websites
- [torch](https://pytorch.org/): Python library using the PyTorch framework, used for various machine learning applications from NLP to computer vision to deep learning models.

  ## Using these Packages

  Next, import these packages. This may take a few seconds to a minute or two depending on if these packages have been imported before, as well as the computing speed and power of your computer.

  ```
  pip install transformers datasets tiktoken tqdm wandb numpy httpx torch
  ```

# Working With WhartonMunicode

## Cloning Repository

Clone this repository to get a local copy in the platform of your choice. (Google Colab users will find the repository in the "Files" tab on the left hand vertical bar, while Jupyter Notebook users will find that the repository clones into the same folder path of the notebook)

```
!git clone https://github.com/srilekha511/Wharton_Municode
```
## Running prepare.py

If you are in Google Colab:

First change directories into the the municodes folder of this repository. Colab won't let you run files unless you are in the exact folder path containing it. Then, run the script prepare.py:
```
%cd /content/Wharton_Municode/data/municode
!python prepare.py
```

Your output should return the file path of the `train.bin` and the `val.bin`, most likely `/content/Wharton_Municode/data/municode`. The train.bin and val.bin files store the tokens of the training and validation files, respectively (tiktoken was used to tokenize the text to prepare it for training). 
The output should also print the number of training and validation tokens there are. For example, if we loaded in the municipal code for the city of Alvarado, Texas (the default dataset in this repository), it should print

```
train has 585,895 tokens
val has 64,881 tokens
```
The larger the number of tokens, the more data the machine learning algorithm can work with to make predictions. See `prepare.py` for a more in-depth explanation. 
