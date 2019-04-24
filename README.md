# bidaf-keras
Implementation of [Bidirectional Attention Flow for Machine Comprehension](https://arxiv.org/abs/1611.01603) in Keras 2

# What is this project abour?
Machine Comprehension is a task in the field of NLP & NLU where the machine is provided with a passage and a question, and the machine tries to find an answer to the asked question from that given passage, by understanding the syntax and semantics of human language (here, English) and by establishing and understanding the relations betweeen the passage and the question.

We have implemented a model suggested in the paper Bidirectional Attention Flow for Machine Comprehension by a team of allennlp, popularly known as BiDAF.

## Usage
This project is available for use as a complete module. You can use this project via command-line arguments or by importing functionalities from it.:

- **Usage via command-line arguments:**
  
  To see the usage info, run `python3 -m bidaf --help`.

  Using this module via command-line arguments will provide you with limited functionalities. To get the real power, we recommend using it by importing its functionalities.
  
  The CLI mode will provide you with two basic functionalities: train and predict.
  
  - **Train:** To get usage information for training models, run `python3 -m bidaf train --help`
    
    For example:
    
    ```
    python3 -m bidaf --model_name=bidaf_50.h5 --do_lowercase train --epochs=1 --steps_per_epoch=1 --validation_steps=1
    ```
  
  - **Predict:** To get usage information for running predictions on a model, run `python3 -m bidaf predict --help`
    
    For example:
     ```
     python3 -m bidaf --model_name=bidaf_50.h5 --do_lowercase predict --passage "This is tree." --question "What is this?" --return_char_loc --return_confidence_score
     ```
   
  **Note** that, some parameters like "--do_lowercase" are dependent on some other parameters like "--model_name". For example, if the model is trained to perform predictions on lowercase inputs, it might not work well if the inputs are not in lowercase.
  
  If you still have any queries on the need/use of any CLI argument, open an issue and we will reach you as soon as possible.
  
- **Usage by importing functionalities:**
  
  You can use the module by importing it in many different ways. So, we will just mention two example code snippets from which you will gain most of the knowledge required.
  
  - **Train:**
    ```
    from bidaf.models import BidirectionalAttentionFlow
    from bidaf.scripts import load_data_generators
    bidaf_model = BidirectionalAttentionFlow(400)
    bidaf_model.load_bidaf("/path/to/model.h5") # when you want to resume training
    train_generator, validation_generator = load_data_generators(24, 400)
    keras_model = bidaf_model.train_model(train_generator, validation_generator=validation_generator)
    ```
  - **Predict:**
    ```
    from bidaf.models import BidirectionalAttentionFlow
    bidaf_model = BidirectionalAttentionFlow(400)
    bidaf_model.load_bidaf("/path/to/model.h5")
    bidaf_model.predict_ans("This is a tree", "What is this?")
    ```
  **Note** that the above are the simplest code snippets. You can explore all functionalities available by looking at the parameters avaiable at different level. If you can't understand the parameters, just open an issue here. We may write the usage of all parameters in future if required.
    
  **Also note** that, in the above snippets, `bidaf_model` is just an object of class `BidirectionalAttentionFlow` and not the real Keras model. You can access the Keras model by using `keras_model = bidaf_model.model`.

## Pre-trained Models
- **Model Name:** [bidaf_50.h5](https://drive.google.com/open?id=10C56f1DSkWbkBBhokJ9szXM44P9T-KfW)
  
  **Model Configuration:**
    - lowercase: True
    - batch size: 16
    - max passage length: None
    - max question length: None
    - embedding dimension: 400
    - squad version: 1.1

- **Model Name:** [bidaf_10.h5](https://link.to.model.will.be.updated.soon)
  
  **Model Configuration:**
    - lowercase: True
    - batch size: 16
    - max passage length: None
    - max question length: None
    - embedding dimension: 400
    - squad version: 1.1

## Features/Improvements in future releases
- Provide two modes for preprocessing: Strict and Moderate.
- Measure accuracy of model with Moderate mode.
- Support for use via command line
- GUI support
- Database support

## What you can do with this project
- Train/Retrain this model with your own dataset.
- Use the pretrained model for extending your own model or to try this one out.
- Modify the code of this model to develop a new model architecture out of it.

## To-do list
- Make this project as a portable module and publish it on pypi

I don't know which things should I keep in mind to do this (such as how to create a setup.py file, what are the other files needed/essential for publishing, how these files help, etc.). If you have such points that I should keep in mind, consider contributing to this project. Also, if you have time to implement it in this project, submit your work with a pull request on a new branch.

Thoughts, samples codes, modifications and any other type of contributions are appreciated. This is my first project in Deep Learning and also first being open source. I will need as much help as possible as I don't know the path I need to follow. Thank you..


## Warnings
- There's a dependency flaw in our project. The package we used to generate word embeddings, pymagnitude, hasn't yet added suport for fixed length inputs - https://github.com/plasticityai/magnitude/issues/50. Hence, trying to use this model with fixed length input will throw an error. We have looked into their source code and found the problem. We have forked that repo, fixed the issue and then generated a pull request but it seems like the author is no more maintaining that project. So, we have to wait. Till then, you may use the patched version of that package to make this functionality work. You can find it here - https://github.com/ParikhKadam/magnitude/tree/patch-1
- If the author is no more supporting this project, we are planning to maintain our forked version in future. But we don't know how to publish such a forked version on PyPI. You can help us in case you know it. Or wait until we learn xD.

## Issues
- Open:
  1. ...
- Solved:
  1. https://github.com/tensorflow/tensorflow/issues/24519
  2. https://github.com/keras-team/keras/issues/11978
  3. https://github.com/keras-team/keras/issues/12263

## My team
- [Dharanee Patel](https://github.com/dharaneepatel15/)
- [Zeel Patel](https://github.com/zeelp898/)

## Our Guide
- [Prof. Tushar A. Champaneria](https://github.com/tacldce/)

## Special Thanks to the researchers of BiDAF
- Sir, [Minjoon Seo](https://github.com/seominjoon/) for helping me out personally
- The team of allenai (http://www.allenai.org/)
