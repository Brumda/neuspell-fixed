<h1 align="center">
<p>NeuSpell: A Neural Spelling Correction Toolkit
</h1>

This is a fork of the [NeuSpell library](https://github.com/neuspell/neuspell), 
but of the pip version and not the one listed on GitHub (it was too late when I realized that they aren't the same).

The pretrained models have to be downloaded from [this link](https://drive.google.com/drive/folders/1jgNpYe4TVSF4mMBVtFh4QfB2GovNPdh7)
and even then they sometimes get **UnpicklingError: invalid load key, '<'.** and can take several tries to get right.
One key needs to be deleted from the state_dict for the BERT model to work (this change is implemented, but automatic downloading is not fixed).

I got the ELMO-SC-LSTM working only in an environment with these versions:
- python=3.9
- pytorch=2.0.1
- spacy=3.5.3
- pydantic<1.9.0 
- allennlp==2.10.1

the rest of the requirements don't matter, as long as they're all compatible, and BERT works with the latest version. 

List of additional changes:
- wandb was added to the fine-tuning script (False by default, can be turned on by argument)
- the condition for saving models after each epoch was fixed
- added option to provide your own validation set to the fine-tuning
- the evaluation for BERT and ELMO-SC-LSTM now also return the values, not only printing them
- the model size calculation was fixed
- rule-based space correction was implemented for ELMO-SC-LSTM (works with rules for normal text)
- convoluted space correction was implemented for BERT (works by leveraging offsets from tokenizer
and input sentence to approximate the spacing in the prediction)

Both space corrections can be turned off with an argument.

Some other minor changes were implemented, but they are not worth mentioning.

Both BERT and ELMO-SC-LSTM were further fine-tuned on the [GitHub Typo Corpus](https://github.com/mhagiwara/github-typo-corpus)
and are available at my [Hugging Face](https://huggingface.co/brumda)