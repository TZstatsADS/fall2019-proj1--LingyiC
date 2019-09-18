# Applied Data Science @ Columbia
## Fall 2019
## Project 1: A "data story" on the songs of our times

---

Please clone this repo and see the whole results from `Project1_lc3352.html` file in `lib` folder. I only add part of results here.

> In this "Data Story", we will use `processed_lyrics_lc.RData` dataset (generate by using `Text_Processing_lc.Rmd` file, which is different from the tutorial one and processing data more accurately than tutorial one) and `artists.csv` dataset. We add some new columns such as decade (1970s, 1980s, 1990s and etc.), category (band and single). <br> 
There are three parts, the first part is basic analysis. <br> 
1. In the first part, we will analyze our datasets and visualize basic information about our datasets. <br>
2. The second part will use lexicons in `textdata` package and do some sentimental analysis. <br>
3. In the Third part, we will take a look at `cleanNLP` package. <br>

<img src="./figs/title.png" width="500">

# Load Pakages and Processed Datasets
**Load libraries**

**load processed_lyrics_lc.RData**
I wrote Text_Processing_lc.Rmd file which is based on Text_Processing.Rmd to generate processed_lyrics_lc.RData. <br>
Processed lyrics are saved in "stemmedwords" column. 

---

# Basic Analysis 
## Artist 
### Basic Information
There are 2535 artists and 125501 songs in our dataset. <br>

### Artists with Highest Song Count
We list artists with highest song count in the table below. <br> 
Dolly Parton gets the highest song count which is up to 717. In addition, we divide our artists to two groups, one is "band' and the other is "single". We also display this information in our table. It seems that the category doesn't influence the output. <br> 

### "Band" or 'Single"?
To my surprise, the difference between songs from "band" and songs from "single" is not that enormous. 43% of our songs are from bands and the rest of songs are indie musicians.  <br> 
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-8-1.png" width="500">


## Lyrics
### Lyrics per Song 
We rank the length of songs and plot the last 10 and top 10. <br>
In this division, we use the original lyrics (not the stemmedwords). We can conlude that "I'm your bass creator" is shortest with around 175 words, while "Yes sir I will" contains around 35,000 words. <br> 

<img src="./doc/Project_final_files/figure-html/unnamed-chunk-9-1.png" width="500">
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-9-2.png" width="500">

### Popular Words in Lyrics
"love", "time", "baby", "day" and "life" are the most popular words among artists.  <br>
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-10-1.png" width="500">

#### Popular Words by Decades
Let's dig deeper into the popular words. We group the songs by year. We analyze them in different decades. We can find that "Love", "time", "baby" are timeless. They are always very popular in the 50 years.  <br>
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-12-1.png" width="500">


### TF-IDF analysis 
In this section, we use TF-IDF analysis to represent the information behind a word in a document relating to some outcome of interest. Tf-idf stands for term frequency-inverse document frequency, and the tf-idf weight is a weight often used in information retrieval and text mining. <br>
TF: term frequency, IDF is inverse document frequency <br>
TF-IDF = TF * IDF <br>

**TF-IDF across time** <br>
We can discover that "life", "eyes", "heart" are always important among these years. ("before 1970s" has very limited data, we can ignore it.)<br>
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-14-1.png" width="500">


## Distribution of Length <br>
In this section, we plot the distributions of word length and song length. 

### Distribution of Word Length  
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-15-1.png" width="500">

### Distribution of Song Length 
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-16-1.png" width="500">


# Sentimental Analysis
## Compare Different Lexicons
### Word Counts in Three Lexicons
In this section, we use `tidytext` package, a wondeful package to do text mining and sentiment analysis.  <br>
`get_sentiments` function in `tidytext` package provides four lexicons -- "afinn", "bing", "loughran", "nrc". However, we will not analyze "loughran" lexicon which is best suited for financial text. <br>

### Match Ratio in Three Lexicons
From the table below, we can observe that NRC lexicon has the highest match ratio, ~0.03996 and AFINN lexicon has the lowest match ratio, ~0.01091. 

## NRC Lexicon 
### Introduction to NRC lexicon 
In the previous section, we observed that NRC has highest match ratio and then we choose NRC Lexicon to analyze deeply in this section:  <br> 
NRC lexicon has 10 categories of sentiment:anger, anticipation, disgust, fear, joy, negative, positive, sadness, surprise, trust. 
Firstly, let's look at the NRC lexicon. Take "abandon" for an example, "abandon" has three labels -- "fear", "negative", "sadness". Each word in NRC lexicon has one or multiple labels. <br>

As the figure shown below, "negative" category has the largest amount of words, "surprise" category has the smallest amount of words. <br>
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-20-1.png" width="500">

> Then we use NRC lexicon to analyze our lyrics dataset. 

### Words in sentiments
In this section, we curious about the top 8 words in each sentiment category. From the figure below, it seems that "feeling" is in every category. <br>
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-21-1.png" width="500">

### Artists in Sentiments 
It's quite interesting that artist Eminem wrote most negative and most positive songs.<br>
![](./figs/Eminem.jpg)<br>

<img src="./doc/Project_final_files/figure-html/unnamed-chunk-22-1.png" width="500">

### Songs in Sentiments 
We can also anlyze songs in different sentiments. As figure shown below, "Silence Night" is the most positive song and "War" is the most negative. <br>
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-23-1.png" width="500">


### Decades in Sentiments 

Since the number of words is imbalanced in different decades as the figure shown above, we will compute the ratio. <br> 
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-24-1.png" width="500">

The bar charts show that songs written in 1970s (we ignore songs before 1970s) are most positive and songs written in 2000s decade are most negative. <br>
<img src="./doc/Project_final_files/figure-html/unnamed-chunk-25-1.png" width="500">

# NLP
We will take a look at `cleanNLP` package. <br>
The `cleanNLP` package is designed to make it as painless as possible to turn raw text into feature-rich data frames. <br>

# Conclusion 
In this "Data Story", we processed and analyzed song lyrics. There are several interesting findings: <br>
1. “Love”, “time”, “baby” are timeless. They are always very popular in the past 50 years. <br>
2. “life”, “eyes”, “heart” are always important among these years. <br>
3. Songs written in 1970s (we ignore songs before 1970s) are most positive and songs written in 2000s decade are most negative. This may be related to the events of that year. We can verify our hypothesis by introducing other datasets. <br>


# References
[1] https://www.tidytextmining.com/sentiment.html <br>
[2] https://statsmaths.github.io/blog/cleanNLP2-quickstart/ <br>
[3] https://www.datacamp.com/community/tutorials/sentiment-analysis-R#lexiconsandlyrics <br>
[4] https://www.kaggle.com/devisangeetha/sing-a-song-lyrics-is-here <br> 




---
<img src="figs/title1.jpeg" width="500">

### [Project Description](doc/)
This is the first and only *individual* (as opposed to *team*) this semester. 

Term: Fall 2019

+ Projec title: Lorem ipsum dolor sit amet
+ This project is conducted by [your name]

+ Project summary: [a short summary] Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

Following [suggestions](http://nicercode.github.io/blog/2013-04-05-projects/) by [RICH FITZJOHN](http://nicercode.github.io/about/#Team) (@richfitz). This folder is orgarnized as follows.

```
proj/
├── lib/
├── data/
├── doc/
├── figs/
└── output/
```

Please see each subfolder for a README file.

