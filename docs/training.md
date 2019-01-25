---
layout: default
---

# Training

## Training new models --- short version

The default command for training the parser pipeline is:

    python3 train_models.py --name name --train_file /path/to/train.conllu --devel_file /path/to/devel.conllu --embeddings /path/to/embeddings.vectors

This will train the tagger, parser and lemmatizer models, and save everything into a directory models_%name. Training and development data must be in the CoNLL-U format, and pre-trained word embedding must be in the word2vec text format. Default parameters for each component are defined in the templates/ directory, you are free to tune the hyperparameter values in these config files.

## Tokenizer

**Currently, the tokenizer model must be trained separately by using UDPipe v1.2.0**, see UDPipe installation instructions [here](http://ufal.mff.cuni.cz/udpipe/install). After downloading/installing UDPipe, a tokenizer model can be trained with:

    /path/to/udpipe --train model.output train.conllu --heldout dev.conllu --tokenizer="dimension=64;epochs=100;initialization_range=0.1;batch_size=50;learning_rate=0.005;dropout=0.1;early_stopping=1" --tagger=none --parser=none

After training, the tokenizer model must be copied into the models_%name/Tokenizer/tokenizer.udpipe.

    cp model.output models_%name/Tokenizer/tokenizer.udpipe

## Running the parser with your new models

Now you should be able to run the pipeline with your new models:

    cat myfile.txt | python3 full_pipeline_stream.py --conf models_%name/pipelines.yaml parse_plaintext > myfile.conllu

## Training new models --- long version

In case of any problems with the train_models.py, here is a list of required steps for training new models:

TODO
