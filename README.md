Predicting Effective Arguments
Final report
Runqi Wang
1. Problem Statement
In our real world, we have many comments. Is there any way that AI can judge how effective those comments are? In this project the dataset presented here contains argumentative essays written by U.S students in grades 6-12. The goal of this competition is to classify argumentative elements in student writing as "effective," "adequate," or "ineffective."
2. Data Wrangling
This dataset contains historic data for a variety of arguments from students. To view the data, the original Kaggle SQLite tables, or the import report using the Kaggle API click on the links below:
Kaggle Dataset
The main purpose of this project is to rank all stocks’ performance. So the simple plan for this project is:
Do research about train.csv 
Do some cleaning and EDA to training data
Transform all words into numerical data
Train a model with numerical words data
Apply the model on test.csv data
There are totally over 4k essays in the dataset. Some of them have 23 rows at most, some of them have only one. 
There are 7 types of discourse that are being annotated here. The data description for the competition provides more details:
Lead - an introduction that begins with a statistic, a quotation, a description, or some other device to grab the reader’s attention and point toward the thesis
Position - an opinion or conclusion on the main question
Claim - a claim that supports the position
Counterclaim - a claim that refutes another claim or gives an opposing reason to the position
Rebuttal - a claim that refutes a counterclaim
Evidence - ideas or examples that support claims, counterclaims, or rebuttals.
Concluding Statement - a concluding statement that restates the claims
"Evidence" is the most common type of discourse that is being annotated in this dataset.
There are three options of effectiveness: Ineffective, Effective, and Adequate. The data description provides more info: Human readers rated each rhetorical or argumentative element, in order of increasing quality, as one of:Ineffective, Adequate, Effective.
The graph for different features shows below:

For more interesting, we did a graph to show what words show more often in each type and effectiveness.

 
 
 
3. EDA
In this project, we do not need more features for prediction. We just need to transfer all words into numerical data. We combine discourse_test and discourse_effectiveness together as inputs. And we add [SEP] as a separation. We get something like below:

Then we transfer all those separated words into numbers.:

Also, we need to define a max length for all those sentences. For a dataset, most sentences are short like 10 words and only one sentence has 100 words, we have to define max length as 10. Because this long sentence’s extra 90 words won’t contribute a lot to the model. In this project, we define max length as 256. We get something like that:

For prediction we also need a mask for each sentences like that:

Also we change discourse_effectiveness to number, Ineffective: 0, Adequate: 1, Effective: 2. Those discourse_effectivenesses are y.
 
4. Modeling
In this project, we use Bert as a pre-trained model. The reason why we use this pre-trained model is 1. It's faster to use a pre-trained model to make prediction 2. Pre-trained models are easy to use to make that prediction. 3. Pre-trained models can get better performance over legacy methods. 4. It has the ability to process larger amounts of text and language.
5. Predictions
Finally, we apply all models to test datasets. And we get the effectiveness of all test’s text.



