# DataBias

### For this project, we are testing if Perspective model has any biases. 

### In order to do so, we need these libraries and APIs:
#### - Pandas (for dataframes)
#### - Matplotlib (to visualize our data in the form of a graph)
#### - Google API Client (to connect with Perspective API)
#### - NTLK (not necessary, but used to filter out any redundant words when exploring the data)
#### - Perspective API (to give us our toxicity score for the comments)

### To explore the sample dataset, I loaded it into a dataframe 'df' and created new dataframes depending on if they were labeled toxic or not. (df_toxic for toxic comments and vice versa)

### To try and see what I was working with, I initially tried to remove any redudant words from the data using NTLK's stopwords and I made everything lowercase so I could see which toxic words were the most prevelant; however, I realized that I did not want to form my hypothesis from the results I got using this method.

### I then looked around the csv file and foundshorter words seem to have a greater accuracy than longer words in some cases, so I made my hypothesis based on that.

## Hypothesis: If the comment is long (more than 10 words), and if toxicity is near the end of text, then PerspectiveAPI will not mark the comment toxic even if it contains a string that it previous deemed toxic. PerspectiveAPI will mark the shorter (10 or less words) as toxic if obscenities are detected. 

### To prove my hypothesis, I need to figure out the amount of words (comment length) in the comment; additionally, I need to modify the comment to see if longer strings are incorrectly classified. I followed these steps to do this:

#### 1. Create a copy of df_toxic
#### 2. Create a new column called 'comment_length' using split() on each element of the dataframe
#### 3. Select only the comments that have less than 10 words and put them into a dataframe called tox and get 30 random samples from tox
#### 4. Find the initial score of the comment using Perspective API and put in a new column called initial_comment_score
#### 5. Add a string with positive words in front of the common text and find the score (puts in new column called modified_comment_score)
#### 6. See if the classification of the comment changes by comparing the modified_comment_score with the threshold calculated in variable 'threshold'

## In the end, my hypothesis was not entirely correct, but it had some resemeblance to the data. More than half the sampled comments changed from toxic to non-toxic after adding positive words before them. However, 13 of the 30 remained the same even after adding a 25 positive word string in front of the toxic comments. I think if I had more data points, there would be more of a clear picture on if my hypothesis was correct or not.

### What suprised me about my findings is that one of the scores actually increased after adding my custom string of positive words. Additionally, I though that the comments with the same amount of starting words would see their toxicity decrease the same amount, but that was not the case. I was suprised with how much the scores changed: some of them barely changed and others went down by 0.2. 

### A theory on why I got the results I have is that certain words or phrases are weighted more toxic than the others. Some words are deemed super toxic as PerspectiveAPI gave comments with that word an initial score of 0.9 and above. Because of the initial weights, even if I added a lot of positive words, it would be harder for the score to go below the threshold.

