# social graph and interactions

## Introduction

Description of the dataset et blabla




## The Network
Make recommendations in that part based on the degree of the nodes


## Sentiment Analysis

In that part, we will give some movie recommendations based on the sentiment decription of movies.

Before recommending you any movies you will need to see what kind of movies fits with your mood of the moment, your personnality or the persons you want to watch with. 
Therefore we will give you some insight about the genre of movie you would like to watch. 
- First, we will first give you some sentiment grades of each genre of movie.
- Then, we will create a word cloud to provide the most comon word that you can find for each movie genre.

### sentiment grades

In our dataset conatining 4 800 movies, we will extract a sentiment grade for each genre of movie. We have 20 unique movie genres which are 'Action', 'Science-Fiction','Romance','Wester','TV movies and so on. 
Based on the LabMT wordlist dataset we will give a sentiment grade of each movie genre. The more the grade is high the more the sentiment is positive. 
The list consists of 10222 words with their average happiness score obtained using Amazon's Mechanical Turk which is a crowdsourcing internet marketplace. The word list was created by using four sources of text; Twitter, Google Books, Music lyrics from 1960 to 2007 and the New York times from 1987 to 2007. The authors then asked the users of Mechanical Turk to rate each word on a nine point interger scale and from this they obtained 50 independent evaluations per word.

Now that we have the sentiment grade over the genre, you can have an idea about the feeling that a type of movie will bring to you

![test](https://user-images.githubusercontent.com/26303508/33664760-06bc63d0-da95-11e7-999c-0eb8a8cd80c5.png)

This picture just help find the genre which correspond to you and also to change your mind about multiple genre that was too sad of too feel good movie.


### Word Cloud

We know that the picture above don't give you much advises about the movie genre, only a grade can not change your mind or help you finding the best movie genre.
So in order to advise you the best way, for each genre we will provide a word cloud to give even more informations. 
We used the description of each movie to generate a word cloud which represent the most common word for all synopsis of each class of movie.
Just below, we generate several word clouds corresonding respectively to 'Romance, 'Science Fiction', and 'Western'

