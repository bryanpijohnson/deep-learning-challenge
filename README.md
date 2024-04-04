# Bryan Johnson's GWU Module 21 - Deep Learning Challenge READ ME File

## The files for this assignment can be found at the following repo:
https://github.com/bryanpijohnson/deep-learning-challenge

## Within the repo link, you will find the following folders and files to be reviewed and graded:

- **README.md** - that is this file :)
    - The report required for this assignment can be found at the bottom of this file.
- **AlphabetSoupCharity_Initial.ipynb** - this is the original Starter File, for which I created the initial analysis
- **AlphabetSoupCharity_Optimization1.ipynb** - this is the 1st optimization attempt, which uses the Keras Tuner to find the best model for the data, using the same pre-processed data from the initial file
- **AlphabetSoupCharity_Optimization2.ipynb** - this is the 2nd optimization attempt, which also uses the Keras Tuner to find the best model for the data, after pre-processing the data a different way
- **Resources** - folder that holds the following folders/files
    - **AlphabetSoupCharity.h5** - the saved model for the initial file
    - **AlphabetSoupCharity_Optimization1.h5** - the saved model for the Optimization1 file
    - **AlphabetSoupCharity_Optimization2.h5** - the saved model for the Optimization2 file

## Overview

The purpose of the analysis was to help create a tool for Alphabet Soup that can "help it select the applicants for funding with the best change of success in their ventures." We were given a CSV file of over 34,000 organizations have had been awarded funding from previous years, and whether or not the money was used effectively.

## Initial Run

### Data Preprocessing

Initially, we were told to remove the `EIN` and `NAME` columns as there was a large amount of values in each of those columns and presumably, they wouldn't matter to the model. These were initially not considered features or targets.

I then looked at the other categorical columns and saw that 2 of them had more than 10 values: `APPLICATION_TYPE` and `CLASSIFICATION`. For both columns, I looked at the value counts and determined a cut-off value that we would rename as "Other". Here are the values that I chose for those columns:

- **APPLICATION_TYPE**: fewer than 500 entries
- **CLASSIFICATION**: fewer than 1000 entries

I then used `pd.get_dummies` to create the columns to translate the categorical columns to numerical. This gave me overall number of 44 columns. Using the `IS_SUCCESSFUL` column as the target, this left 43 columns for the features.

### Compiling, Training, and Evaluating the Model

As we were initially instructed to use 2 hidden layers, I opted to use a large amount of nodes in each layer, specifically 80 nodes in the first layer and 30 nodes in the second layer.

Using the `binary_crossentropy` value for loss, the `adam` optimizer, and looking to maximize `accuracy`, I trained and then evaluated the model on the test data. This gave me an accuracy score of 72.89% with a 56.31% loss.

## Optimizing Runs

For the second round of models, my thought was to use the Keras Tuner to hopefully get better results. I used the exact same pre-processing as I had in the initial run, and thought that the Keras Tuner might do a better job of maximizing the accuracy on the data.

I used the same function that we created in class, but modified the values to allow for many more epochs for each of the runs. When it ran, it completed over 500 Trials and saved them in the Resources/Optimizer_1 folder. The loss was 54.70% and the accuracy was 73.17%.

I then realized that it wasn't the model that needed more tuning, but the pre-processing needed to be done better. I realized that not only did I bin too much of the categorical data, but I also should have kept the `NAME` column and binned that as well. (I considered keeping the `EIN` column, but each row had a unique value, and adding over 34K columns with only one 1 in)

### Data Preprocessing

### Compiling, Training, and Evaluating the Model

## Results