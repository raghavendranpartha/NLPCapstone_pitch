---
title       : NLP next word prediction algorithm
subtitle    : Data Science Capstone Project
author      : Raghavendran Partha
data        : "Jan 24 2016"
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---


## Objective

- The goal of the project is to create an application (found <a href = "https://raghavpartha.shinyapps.io/NLPshinyapp/"> here </a>) that serves as a next-word prediction algorithm
- Based on the user input, an English phrase, the algorithm predicts the next-word of the phrase
- The algorithm implemented here is the <a href = "http://www.aclweb.org/anthology/D07-1090.pdf">stupid-backoff </a> algorithm, popular in the field of Natural Language Processing
- The algorithm is trained on three large English language datasets freely available at <a href = "http://www.corpora.heliohost.org/statistics.html#EnglishUSCorpus"> HC corpora </a>, and consists of English sentences and phrases from blogs, twitter, and news articles

--- .class #id

## Data cleaning

- The full dataset is not directly amenable to constructing a next-word prediction algorithm considering its size. 
     * Randomly sample 33% of each dataset and use this as the corpus for training the next-word prediction algorithm. 

- Data cleaning
     * Separating sentences on the same line into distinct lines
     * Removing any punctuation marks, trailing and heading whitespaces
     * Removing non-alphabetical words such as emoticons, and converting all words to their lowercase forms
     
- The three cleaned datasets are then combined into one large corpus

--- .class #id

## ngrams model and stupid backoff

- Construct ngrams (n consecutive words) of sizes 1, 2, 3, and 4, from the training dataset, and store the prediction for each ngram as the word succeeding the ngram in the dataset
- Create a frequency table, which stores the number of times each prediction is assigned to a particular ngram -> database of ngrams
- Stupid backoff
     * Split the query phrase into ngrams of sizes 1 to 4, such that these ngrams end with the last word of the query 
     * Starting with the largest ngram, lookup the presence of the ngram in our database
     * The next-word prediction is simply the most frequently occuring word succeeding the ngram 
     * If the ngram is not present, delete the first word of ngram leading to a n-1 gram and lookup in database
     * Repeat till no ngram matches, in which case the most frequent word in the dataset is returned

--- .class #id

## Sample app usage

- Enter the text phrase in the first input section on the left panel
- Use the slider to select the maximum number of predictions you want the algorithm to make
- Click Predict!

<div style='text-align: center;'>
    <img height='400' src='scrshot.png' />
</div>
