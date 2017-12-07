# social graph and interactions

## Introduction
Our goal is to recommend you some movies based on a movie dataset containing 4800 movies. We took that dataset from the website(https://www.kaggle.com/tmdb/tmdb-movie-metadata).
Based on your favorite actor, the movie genre ou like or your favorite movie we will give you some recommendations. We will first use a network of movies and then use the natural language processing to give you the best advises.

Here is some basic statistics about our dataset:
To give an insight about it, we plot just below the average budget over years

![test](https://user-images.githubusercontent.com/26303508/33716337-15ecfbc8-db56-11e7-9ddd-311d2a1460a0.png)

We can definitely see how the movie industry become a huge business over years. The superproductions are now mainstream production movie. That is why we want to make you recommendations not based on how popular is a movie or how expensive is another, we want to base our recommendations on facts, on similarity or on the network.


## The Network

In this part, we will create a Network to link movies if they have actors in common. Then, we will analyze the network and also run the Louvain Algorithm to see if we can isolate communities.

The first part is about loading and formatting the data to our need for this project. I won't detail it here (cf. the notebook).

The network that we create is given below. It contains a lot of movies linked together and some outliers ("small" movies with unexperienced actors who only played in 1 movie).

![network](https://user-images.githubusercontent.com/19948466/33676245-81088c8e-dab5-11e7-8f54-b7ea06697258.jpeg)

It has 4800 nodes and 253 502 edges.

What characterize a high degree movie ? 
We see with the plot below that they is a positive correlation between ratings and the degree. Basically, a movie with a high degree stars famous and experienced actors (larger budget), it will be more likely to receive good ratings from the public. 

![degree_vs_ratings](https://user-images.githubusercontent.com/19948466/33676305-b9d2d25e-dab5-11e7-9947-271b74a9a861.jpeg)

Can we recommand some movies to anyone who has a favorite actor ? 
From a given actor, we look into our Network and we return the 10 movies containing this actor with the highest degree.

Here is an example with Tom Hanks, we get 10 recommandations : 

 - "Catch Me If You Can"
 - "Cars"
 - "Saving Private Ryan"
 - "Toy Story 3"
 - "The Green Mile"
 - "The Things That You Do!"
 - "Cloud Atlas"
 - "Philadelphia"
 - "Road To Perdition"
 - "Apollo 13"

### Communities

We have been able to isolate 11 communities in this Network for a modularity equal to 0.24 which means that the partition is correct.
Basically, actors often are "specialized" in a genre and they also work with the same directors several times throughout their life. It explains why actors who shoot together once are more likely to shoot again together in the future.

This is just a trend and not a rule that applies most of the time. That is why the modularity is not that high (<0.3).



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

![test](https://user-images.githubusercontent.com/26303508/33667114-3e25708a-da9c-11e7-958a-f6be9b2d78f6.png)

This picture just help find the genre which correspond to you and also to change your mind about multiple genre that was too sad of too feel good movie.

### Word Cloud

We know that the picture above don't give you much advises about the movie genre, only a grade can not change your mind or help you finding the best movie genre.

So in order to advise you the best way, for each genre we will provide a word cloud to give even more informations. 
We used the description of each movie to generate a word cloud which represent the most common word for all synopsis of each class of movie.
Just below, we generate several word clouds corresonding respectively to 'Romance, 'Science Fiction', and 'Western'.

![wordcloud1](https://user-images.githubusercontent.com/26303508/33665263-a172d282-da96-11e7-9b7c-22fe258792f1.png)

![wordcloud2](https://user-images.githubusercontent.com/26303508/33665284-b2e33368-da96-11e7-9b72-4689b33a24b1.png)

![wordcloud3](https://user-images.githubusercontent.com/26303508/33665298-c17d48d2-da96-11e7-84d2-c85660e6d99d.png)


### Movies recommendations

- In that part, we will recommend you some movies based on the sysnopsis of a movie you discover (which is not in the database) or based on the title of the movie you like if he is in the database

We will have to :
- whether copy past the synopsis of the ovie you like in "decription"
- whether choosing a movie between 0 and 2799 in the database

Based on you choice we will give you 10 recommendations of movie you should see.

The way we recommend you some movies is based on similarity measure between the synopsis of the movies. We used the cosine similarity measure.

We generate a tf-idf vector for each desciption movie which are almost vectors of words frequency used to describe the movie. Then we calculate the similarity measure between all the movies and extract the 10 best greater measures. Those 10 greatest similarity measures will give you the top 10 recommendations.
We can not know all the movies so that type of recommandations on our big datbase is a really interesting tool because we don't affect any weight to most well known movies like it could be the case for the famous movie website. Our tool is only based on natural language processing.

Here are some exmaples of recommendations that could be made by our programm:
if we pick "The hunchback of notre Dame", we will get those 10 recommendations

 - 'Thinner', 0.14703841369422399
 - 'The Jacket', 0.10481602520699629
 - 'As Above, So Below', 0.10021137108609002
 - 'Lady in White', 0.092211899360291949
 - 'How to Fall in Love', 0.084259047898571637
 - 'Teenage Mutant Ninja Turtles', 0.083761183404710171
 - 'Bandslam', 0.08286061276703427
 - 'Along the Roadside', 0.080059806107607878
 - 'Iguana', 0.079031048777254531
 - 'Clash of the Titans', 0.078171475896677611


Moreover, we can also find some recommendations based on movies which are not the database, let us take the movie "The Verdict" and its imdb description ('A lawyer sees the chance to salvage his career and self-respect by taking a medical malpractice case to trial rather than settling')

Runningour programm, we get those 10 recommendations
- 'A Civil Action', 0.13769887550011084
- "The Devil's Advocate", 0.11572449393749507
- 'The Conspirator', 0.11313793020077545
- 'Misconduct', 0.10843221926403357
- 'I Am Sam', 0.10358217097305766
- 'Obsluhoval jsem anglickle', 0.095934093109751428
- 'Revolution', 0.095647005209171354
- 'Hellboy', 0.095360032677248574
- 'Thinner', 0.093940296393182243
- 'Sweet November', 0.093184298215508443
- 'Gandhi, My Father', 0.088553122762747738


We can see that sometimes the recommendations are far from what we expected but it is based on the word that were used in the description so a single word can be really determinant in some case. 
We see in the last example that the movie "Gandhi" is recommended if we liked "The Verdict", it is mainly due to the justice desire of the main characters in the two movies.


To conclude, you will understand that our programm is really powerful in the way he looked sometimes deeper into words to find some similarities with other movies but of course sometimes it overfits to much and we can find some completely different movies. This is the problem of short description movie, they can not tell all about the movie in the synopsis otherwise there is no longer interste in watching it. 
