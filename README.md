# Data Science Daily Discoveries

This is a daily diary to keep me focussed and moving. 
For ~74 days (over 3 months) I will upload something related to learning 
Python, git and other tools useful for data science. 

I'm using the [Jupyter Notebook](http://jupyter.org/) with the Anaconda (2.4.1) 
Python (2.7.11) up to ~ day 35, and Python 3.5 thereafter.

UPDATE: extending past my 3 months. 

------------------
#### Day 82

##### Inferential Statistics

See [this workbook](/tutorials/inferential_stats/081-Inferential.ipynb)
- r and rsquared. Made a OLS model to explore the relationship between two variables. 
- [Brilliant tutorial](https://stanford.edu/~mwaskom/software/seaborn/tutorial/distributions.html) for exploring data distributions and 
relationships in seaborn.

- if the 95% confidence intervals of the pearson correlation coefficient include 0 then we have to accept the null hypothesis that the 
correlation we see is due to chance. You should also look at the P-value for the t-statistic - is it less than alpha = 0.05?

- [This workbook](/tutorials/inferential_stats/082-Flights.ipynb) for calculating the gradient of a regression line, using the std of both 
x and y (using n-1)

------------------

#### Day 81

##### Inferential Statistics

- Standard deviation of the sample mean distribution is also called the Standard error. Calculated std/sqrt(n) where std = standard 
deviation of the population and n = no. of samples
- Z-Score is how many standard deviations your observed mean is, away from the population mean. What is the probability that this observed 
mean is randomly selected? - Look up your Z-Score on the [Z-table](https://s3.amazonaws.com/udacity-hosted-downloads/ZTable.jpg). 
- See [workbook in python 3](tutorials/inferential_stats/081-Inferential.ipynb)

------------------
#### Day 80

##### Statistics
###### Variance and Standard Deviation
- It is usually better to use standard deviation rather than variance because SD is expressed in the same units as the mean. 
- Use sum(var)/n-1 to give the best estimate of the true variance. Where var = (x-meanx)^^2, for each point in the sample. n 
underestimates, n-2 overestimates, see [Khan 
academy](https://www.khanacademy.org/math/statistics-probability/displaying-describing-data/sample-standard-deviation/v/another-simulation-giving-evidence-that-n-1-gives-us-an-unbiased-estimate-of-variance)
- Only use n-1 when looking at the variance of a sample. 
- When calculating standard deviation use n. 

###### Chi-squared (kai squared). Goodness of fit.

- For categorical variables.
- Work out the critial Chi-squared value based on degrees of freedom (n-1) and a chosen significance level (e.g. 0.05). Calculate the 
Chi-squared statistic from the sum((obs-expected)^^2)/expected) for each value. See [Khan academy 
video](https://www.khanacademy.org/math/statistics-probability/inference-categorical-data-chi-square-tests/chi-square-goodness-of-fit-tests/v/pearson-s-chi-square-test-goodness-of-fit)

------------------
#### Day 79

##### Probability

- D-Separation(Reachability): [Active and Inactive 
triplets](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/487138290923#) Udacity vid.
- Some [good tips](https://www.youtube.com/watch?v=iutkLjeGc6w) for using PyCharm.


------------------
#### Day 78

- AUC - Area Under Curve: Second most popular metric for classification techniques, after accuracy. If you use probabilities to assess the 
accuracy of your classification, you need to set a threshold at which the classification label becomes 1 or 0. AUC considers all possible 
thresholds to get the optimal true positive/false positive rates rates when you compare *true* class labels with your *predicted* class 
labels.

- Use a linear model for high-dimensional, sparse data, such as Bag of Words.

- Gradient Descent

- Simple Linear Regression - find a function (build a model) which can describe the relationship between two variables. Find the unknown 
coefficients using Least Squares or Gradient Descent. Minimizing the sum of squared errors is equivalent to maximizing the likelihood of 
the observed data.

------------------
#### Day 77

##### Kaggle Word Vecs #3

**Sentiment prediction using Word Vectors**

- Using average vectors over a paragraph yielded ok results, not as good as bag of words.
- Tf-idf weighting determines how important a word is to a particular document in a collection of documents or a corpus.
- `scikit.learn` `TdidfVectorizer` has a similar interface to CountVectorizer used in [075-BOW.ipynb](tutorials/KaggleNLP/075-BOW_1.ipynb).
- Folks at Kaggle found [no score improvement](https://www.kaggle.com/c/word2vec-nlp-tutorial/details/part-3-more-fun-with-word-vectors) in 
using either the average vectors or TF-idf methods with the vectors over Bag of Words in tutorial #1.

**Clustering**

- Using K-means clustering to assign each word a cluster "id". This means each word will belong to a cluster with a particular meaning. 
- In Bag of Words we created a matrix [reviews,words] where the top 5000 words were the columns and the rows were the count of how often 
each word occurred in that particular review.
- Uses K-means to cluster the words into meaning. Then Bag of Words to create a term-document matrix but with cluster numbers, so in theory 
the words are classed by meaning, rather than simply frequency. Then, Random Forest again, using the original classification to train the 
model. 
- The clustering approach is not much better than the original BOW because they both end up as BOW and lose the word order which is quite 
important.
- Kaggle Tutorial suggests [Paragraph Vector](http://cs.stanford.edu/~quocle/paragraph_vector.pdf).
- Another high-scoring kaggler suggests: [Tutorial from fastml.com](http://fastml.com/classifying-text-with-bag-of-words-a-tutorial/) with 
improvements and higher score. [Github](https://github.com/zygmuntz/classifying-text) for it.


------------------
#### Day 76

##### Codecademy git

- Played around with the free lessons [here](https://www.codecademy.com/learn/learn-git)
- `git log` shows all the previous commits
- `git HEAD` shows the details of the current commit
- `git checkout HEAD filename` if you make changes in the working directory you don't want to keep.
- `git reset HEAD filename` if you accidently change, and stage, a file and just want to go back to it's previous version (while keeping 
other staged changes)
- `git reset SHA` where SHA = first 7 characters of the commit key. This removes all commits, back to that one. 
- `git checkout master` - switch back to master branch, from another branch.
- `git merge fencing` - you are inside master when you give this command to *fast forward* master to fencing.
- `git branch -d branch_name` : delete a branch once you have merged it with master and resolved any conflicts.

**collaborating with git**

- `git clone remote_host local_dir` : in future `remote host` is referred to as `origin`
- `git remote -v` gives the details of the location and names of the remote repos.
- `git fetch` this checks to see if someone has changed the remote repo. These are now on the origin/master branch and not my *local* 
master.
- Steps for collaborative working:

    1) Fetch and merge changes from the remote    
    2) Create a branch to work on a new project feature     
    3) Develop the feature on your branch and commit your work     
    4) Fetch and merge from the remote again (in case new commits were made while you were working)     
    5) Push your branch up to the remote for review     
    
- `git push origin your_branch_name` : after you've made changes to your own working copy of origin (via a branch  you push that branch to 
the remote repo for someone to decide whether to merge it or not. 

##### Kaggle Word2Vec

- When appending a list of lists to another list of lists must use `+=` instead of `append`
- Python logging.

**Outline**

- Find the meaning of a word based on the words around it. Can be usef on hundreds of billions of words.
- Read in and clean the data similar to [bag of words](tutorials/KaggleNLP/075-BOW_1.ipynb) but keep stop words as they help determine the 
context. Output all the reviews/text as a list of sentences
- Make a model with the sentences. `model = word2vec.Word2Vec(sentences, num_features=....etc)`
  - Use `model.init_sims(replace=True)` if no further training.
- Save model with a meaningful name:  
`model.save(model_name)`    
- To reload the model later: `Word2Vec.load()`. All working [here](tutorials/KaggleNLP/076-word_vectors.ipynb)


------------------
#### Day 75

##### Kaggle Bag of Words #1

**overview**

- Data Cleaning and text processing
  - Apply a function to each document which uses `BeautifulSoup` and `re` to make a list of words without stopwords, for each doc
  - Append these new clean reviews to make a nested list
- Get features from the data
  - sklearn's feature extraction `CountVectorizer` is a bag-of-words tool
  - We create a 2D vectorizer object (term-document matrix). We are shown how to query this matrix.
- Fit a Model (an object name forest) the data using `RandomForestClassifer` with the term-document matrix
- Apply `forest` model object to test data (clean and processed as above beforhand) like so:   
   `result = forest.predict(clean_test)`
- The main issue I have found with `textmining` module is that you can't specify the number of words you want to keep from all the possible 
words. Perhaps it is not useful for a problem which requires that. 
- All working in [075-BOW.ipynb](tutorials/KaggleNLP/075-BOW_1.ipynb).


------------------
#### Day 74

##### DS from Scratch NLP

- `Counter()` is a dictionary which contains key:value pairs which the value is the number of times key appears.
- To find a value in a nested list: use `enumerate` and `for` loops. See [here](/DSFromScratch/Chap20/074-Natural_Language.ipynb).

- Parts I understand of **Topic Modeling**
  - The aim is to work out what topics a user is interested in given a list of software-related words
  - We assign each word a *random* topic and decide there will be 4 distinct topics. So a random number 0-3 is assigned to each word
  - We create functions to populate conditional distributions p(w|t) and p(t|d). Four weightings are assigned to each word in each 
document- one for each topic. 
` - These weighting are used to choose a new topic for each word. 
- The part I don't understand:
  - How how the weights are used to pick a new topic for each word. Something about minimising a combination of weights? The answer is 
probably in [this paper on Latent Dirichtlet Allocation](http://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf)
  - A recommended library for implimenting LDA is [Ida](http://pythonhosted.org/lda/) - the example there shows how to use it to get a 
user-defined number of topics from a body of text. 
  - [Gensim](http://radimrehurek.com/gensim/tutorial.html) - sold as "unsupervised semantic modelling from plain text"

##### Kaggle Bag of Words

- punctuation such as `!!!` or `:-(` are removed in this example, but consider using them in sentiment analysis.
- "tokenization" is lower-casing and splitting up words in a passage.
- store words which are not in a list of other words:
`words = [w for w in words if not w in stopwords.words("english")]` i.e. get rid of the little words "a", "the".. etc in words. `words` is 
now a cleaner piece of text.
- searching a `set` is much faster than searching a `list` - so convert when you can!
- `sklearn.feature_extraction.text.CountVectorizer` can be used to fetch the raw data from files, create tokens and remove stop words.
- This [stackoverflow](http://stackoverflow.com/questions/15899861/efficient-term-document-matrix-with-nltk) explains to me more clearly 
what is in a `term-document matrix` and suggests using the 
[textmining](https://pypi.python.org/pypi/textmining/1.0) package.


------------------
#### Day 73

##### NLP #2 Udacity Intro to AI

- **Smoothing** is needed to account for when p(f|label) is zero. When a particular word(f), with classification(label) does not appear in 
a training set at all. This is likely to happen and does not mean the word will not occur in reality. 
- `nltk.probability` contains classes for different smoothing techniques.
- Sentence structure
- [PCFG](https://classroom.udacity.com/courses/cs271/lessons/48734403/concepts/487300760923#): Probabilistic Context-Free Grammar e.g. 
`P(VP->V,NP,NP|lhs=VP) = 2`
- [LPCFG](https://classroom.udacity.com/courses/cs271/lessons/48734403/concepts/487161760923#): Lexicalized Probabilistic Context-Free 
Grammar e.g. `P(VP->V,NP,NP|V=gave) = 0.25` LPCFG deals with specific words rather than just categories.

##### NLP DS from Scratch

- Scraping from a website using BeautifulSoup
- Bigram, Trigram and Grammar models. Briefly touches on top down and bottom up approaches - also discussed 
[here](https://classroom.udacity.com/courses/cs271/lessons/48734403/concepts/486736210923#)
- Gibbs sampling - when you want to produce a random sample where you only know conditional distributions
- Using two `for` loops in one line:
  - `distinct_words = set(word for document in documents for word in document)`
- Workbook [here](/DSFromScratch/Chap20/073-Natural_language.ipynb) (still need to understand the Topic Modelling part)

------------------
#### Day 72

##### DS from Scratch

**Chap 13 Naive Bayes**
- [Implimentation](/DSFromScratch/Chap13/072-NaiveBayes.ipynb) of a Naive Bayes spam filter. Scikit.learn has the same filter named 
[`bernoulliNB`](http://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.BernoulliNB.html). In the 
[notebook](/DSFromScratch/Chap13/072-NaiveBayes.ipynb):
  - Building a Naive Bayes Classifier. Includes `class NaiveBayes` with methods `train` and `classify` and external functions 
`tokenize`,`count_words`,`word_probabilities` and `spam_probabilities`
  - Test the classifier. Split the data into `test` and `train`. Create `classifier` object. Train the classifier object on `train`.
  - Feed the classifier object `test` and then use `Counter` to store the results in those that are p > 0.5 of being spam.
  - use `filter` to look at the 1) non spam messages most likely to be labelled "spam" and 2) spam messages most likely to be labelled "ham"
  - `sorted` with a key=function argument to sort the list based on it's bayes's probability.
  - As stemmer function could be added to improve classification i.e. "cheap" and "cheapest" - "est" could be removed.
Naive Bayes assumes that the probabilities of different words appearing in spam are independent. Although this is an unrealistic assumption, 
in general the results are good. 

#### Udacity NLP #1

- [Gzip](https://classroom.udacity.com/courses/cs271/lessons/48641663/concepts/486487210923) - shows very simple shell code to identify 
what language a document is in, using compression techniques.
- [Segmentation](https://classroom.udacity.com/courses/cs271/lessons/48641663/concepts/483697940923#) - Naive Bayes is good for this. 
[Code](https://classroom.udacity.com/courses/cs271/lessons/48641663/concepts/486467250923) is relatively simple to impliment.
- [Markov might be better than Naive Bayes](https://classroom.udacity.com/courses/cs271/lessons/48641663/concepts/487124070923#) for 
recognising when words should go together.

------------------
#### Day 71

##### Udacity - Probabilistic Inference

- Enumeration and speeding up enumeration
- Variable Elimination
- To go from P(R,T) to P(T) use **+** and for P(T)P(L) to P(L,T) use **x**
- "Berkson Paradox" - conditioning on a common effect causes two previously uncorrelated variables and independent variables to become 
dependent and correlated! See example of [rain, sprinkler and 
sidewalk.](https://medium.com/@akelleh/understanding-bias-a-pre-requisite-for-trustworthy-results-ee590b75b1be#.vskweklb2)
- [Likelihood weighting](https://classroom.udacity.com/courses/cs271/lessons/48743138/concepts/484039270923#)
- [Gibbs sampling](https://classroom.udacity.com/courses/cs271/lessons/48743138/concepts/486964720923#) - uses all 
evidence, not just upstream evidence. Sample from one variable at a time, conditioned on all the others.

**NLP #1**

- Language models can be *probabilistic, word-based and learned* or *tree structured, logical and based on grammatical rules*
- Markov Assumption considers nearby words.

------------------
#### Day 70

##### Udacity - Bayes networks and Bayes Rule 

- Example: cancer test. Much easier to use a table to work out the different parts of the equation. Shown 
[here](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/487183980923#).
- Complimentary probability, Independent Probability, 
[here](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/484254390923#) 
- Dependent probability and Bayes Rule [here](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/479785610923#)
- [Conditional Dependence] (https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/482305330923#)
- How many parameters are needed to specify a network? 
[Here](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/487276210923#)
- D(directional) seperation - Active triplets and Inactive triplets. A useful way to work out what node is dependent on what. 
[Here.](https://classroom.udacity.com/courses/cs271/lessons/48624746/concepts/487193580923#)


------------------
#### Day 69

##### DS From Scratch: NLP

- Bigrams: using pairs of words to simulate a sentence of words.
- Trigrams: same as above but grouping words together in threes
- Gibbs sampling (not quite grasped yet). Notebook [here](/DSFromScratch/Chap20/069-Natural_Language.ipynb)

Will do the Naive Bayes chapter, before coming back and finishing this.

- `P(X1=1,X2=2|S)` - Probability that word X1 and X2 are in a spam message
- P(S|X=x) - Probability that a message is spam given word x is present
- To avoid *underflow* (computer not coping with floats close to 0) instead of multiplying lots of probabilities together, for p1 \*...\*pn we use the equiv:
    - `exp(log(p1)+...+log(Pn))
- *smoothing* used to avoid a problem such as: "data" vocab word only occurs in nonspam of the whole training. So P("data"|S) = 0. Any message with "data" is given p=0. Even "data on cheap viagra and rolex watches".
This is avoided by adding pseudocount k i.e. `P(Xi|S) = (k+spamcount_wordi)/(2k + spamcount)` and reversed for `P(Xi|notS)`(probability word 
i not in spam). For "data" this means `P("data"|S)=1/100` = 0.01 so we can still assign a nonzero to messages with "data".
[working so far](/DSFromScratch/Chap20/069-NaiveBayes.ipynb)

##### git

- Great introduction to git [here](https://try.github.io/levels/1/challenges/1)
- [Next steps](http://gitreal.codeschool.com/?utm_source=github&utm_medium=codeschool_option&utm_campaign=trygit)

------------------
#### Day 68

##### Statistics (khan)

- With a small sample size ( < 30) the sample sd is a poor estimate of the pop sd. You can't assume a normal distribution for the sample. 
- Use a two-sided T-table because we are symmetric about the mean.
- Approximate standard error from samp sd/ sqrt(n)
- Find how many sds you need to be 95% confident (look up with degrees of freedom (n-1))
- multiply t-value by standard error to give the value +/- above below pop mean you are 95% confident in.
- Video 
[here](https://www.khanacademy.org/math/probability/statistics-inferential/confidence-intervals/v/small-sample-size-confidence-intervals)

##### Algorithms

- Chain, Ring, Grid and Planar graphs have a number of `edges`(m) which is linear with the number of `nodes`(n). i.e. m `$\in\Theta$(n)` 
- In Big `$\Theta$` notation `$\in$` symbolises that a function "is in" or has membership in a set of functions describes on the rhs.
- number of nodes, `n`, is always to the power of 2 in Hypercubes.

##### Titanic

- Wanted to use groupby to plot my histograms but unfortunately a couple of things aren't working: [no 
titles](https://github.com/pydata/pandas/issues/12452) for each group and layout keyword [doesn't 
work](https://github.com/pydata/pandas/issues/12450). Looks like they're still being worked on. 

- Remember to include axis = 1 with `pd.concat` to ensure it adds an extra column, and not just more rows.
- Workbook [here](Titanic/notebooks/068-Titanic_Rconvert.ipynb)



------------------

#### Day 67

##### Algorithms 

- `log$_2$n` = how many times do we have to divide n to get 1? i.e. `log$_2$4 = 2` and `log$_2$6 = 2.5`.
- Problem set 1: Create Graph With Eulerian Tour. Answer [here](tutorials/algorithms/scripts/L1_EulerianPath.py).
- Problem set 1 Qu 10: Find Eulerian Tour Answer [here](tutorials/algorithms/scripts/L1_Eulerian_Q10.py)
- [Workbook](tutorials/algorithms/notebooks/067-Lesson1Qu10.ipynb) for experimenting with these problems

##### Statistics (Khan)

- Confidence intervals:
  - Estimate the probability that the true population mean lies within a range around a sample mean 
[here](https://www.khanacademy.org/math/probability/statistics-inferential/confidence-intervals/v/confidence-interval-1)
  - Describe how to calculate a 99% confidence interval for the proportion of teachers who felt computers are an essential tool 
[here](https://www.khanacademy.org/math/probability/statistics-inferential/confidence-intervals/v/confidence-interval-example)


------------------
#### Day 67

##### Linux

- `xdg-open filename` to open any file with it's default application
- Swap has been decreased by 10GB to increase system space to 20GB. First (Windows) partition is very full - need to check what is in 
there.

##### Summarizing text

- [Smmry](http://smmry.com/) easy online tool. Use this for pdfs.
- Downloaded [TextTeaser](https://github.com/DataTeaser/textteaser) from github. Only takes text. If I could convert pdfs to text myself I 
could use this.

##### Social Network Analysis

- [Social Circles](http://jasss.soc.surrey.ac.uk/12/2/3.html) paper.
- [NetworkX](http://networkx.github.io/) is a python library for the "creation, manipulation, and study of the structure, dynamics, and 
functions of complex networks."
- [Social Network Analysis](http://jasss.soc.surrey.ac.uk/12/2/3.html) on Udacity.

##### Udacity Algorithms

- Exploring [some simple algorithms](tutorials/algorithms/notebooks/Lesson1.ipynb) in Lesson 1.


------------------

#### Day 66

##### SQL - Tournament Project

- My final scripts which can monitor a swiss-pairings style tournament can be found 
[here](https://github.com/SophMC/SQLtutorials/tree/master/Relational_Databases_Udacity)
- I learned how to set up a database, and make inserts for new players, make updates for changes in the players standings, their scores 
etc, and how to perform all of these things from a python script. 

##### Titanic

- Have determined that MICE might be better after all, after looking at some frequency distributions, instead of mass distributions! 
[Here](Titanic/notebooks/066-Titanic_Rconvert.ipynb)


------------------
#### Day 65

##### Central Limit Theorem

- With CLT you can can calculate the `Standard Error of the Mean` which is the Std of the sample mean distribution.    
To find the confidence intervals above/below a mean work out how many stds that interval is above or below the mean.    
E.g what is the confidence that a population mean is 2 years +/- a mean of 40? If we work out that the `standard error of the 
mean` is 1.5 (using `std_error = std_pop/sqrt(n_samples)`), where `std_pop` is 
substituted with `std_samp` then 2 years is 1.33 standard deviations from the mean. Looking up 1.33 in the Z-score table gives 0.41. 2 
years +/- = 0.82, or 82%. We are 82% sure that the mean falls within +/- 2 years of 40 year. 


##### SQL - Tournament Project

- `CREATE DATABASE tournament` first, then run the `tournament.sql` inside psql run the CREATE TABLE (and other) commands using 
`\i tournament.sql` . 


------------------
#### Day 64 

##### DS from Scratch Chap 5: Statistics

- *Correlation* : correlation is measuring the relationship between your two variables all else being
equal. If your data classes are assigned at random, as they might be in a well-designed
experiment, “all else being equal” might not be a terrible assumption. But when there
is a deeper pattern to class assignments, “all else being equal” can be an awful assumption.

##### Central Limit Theorem


- Any distribution that has a well-defined mean and variance will become increasingly normally distribution as sample size ---> infinity.
- The frequency distribution of sample means from the above sample with well defined mean and variance is called:   
"Sampling Distribution of the Sample Mean"
- [Udacity](https://classroom.udacity.com/courses/st101/lessons/48720345/concepts/487245360923)
- [Khan Academy (very 
good!)](https://www.khanacademy.org/math/probability/statistics-inferential/sampling-distribution/v/sampling-distribution-of-the-sample-mean
)

##### Comparing different Imputation methods for Titanic

- Filled in the missing values for Age with three different methods and compared their cross validation scores using a RandomForest 
classifier [here](Titanic/notebooks/064-Compare_imputations.ipynb).
- I'm not sure if the marginal gains from using the more complex methods were really worth it.  


------------------
#### Day 63

##### Relational Databases (Udacity)

- Ran into problems with the webpage. One was the pg_config.sh file had not been run and the other was in the script where I had 
`pg = c.fetchall()`. This turned the database into a list which couldn't be closed with `pg.close`. 
- Instead included c.fetchall in     
`posts =[{'content': str(row[1]), 'time': str(row[0])} for row in c.fetchall()]`
- Have to change `VALUES (%s) " % (content))` to `VALUES (%s) " ,(content,))` to make sure posts will not be executed as an sql statement!


Steps to get the web server running and to test some posts out:   
- The pg_config.sh file had not been run I think, which resulted in `posts` table being missing from `forum` db.
  - `cd ~/Desktop/fullstack/vagrant`
  - `vagrant up`
  - `vagrant ssh`
  - `cd /vagrant/`
  - `python forum.py`: in theory you can now open the webpage at `localhost:8000`
  - `vagrant halt` when finished.

#### Linux basics

- `ls -l pg_config.sh` : check the ownership of `pg_config.sh`
- `chmod 744 pg_config.sh` : change ownership so that Owner=rwx, Group=r, World=r
- More details on `chmod` codes in [here](http://www.linux.org/threads/file-permissions-chmod.4094/)
- `sh pg_config.sh` to run the file.

#### DS from Scratch: Chap 5: Basic Statistics

- The *variance* is the sum of the squares of each values difference from the mean divided by n-1
- The *covariance* is the sum of the variance for two variables at the same point. Can be easily skewed by how much data you have.
Nearly always better to use *standard deviation* `sqrt(variation)`.
- Some code and notes [here](DSFromScratch/Chap5/063-Chap5Statistics.ipynb).

------------------
#### Day 62

##### Relational Databases (Udacity)

- To close a connection to a server via port 8000: `sudo fuser -k 8000/tcp`
- Have to use python 2.7 with this course
- By simply adding a comma after `content` we can be sure it will be recognised as plain text and not an SQL command: `c.execute("insert 
into post(content) values ('%s') " %(content,))`

------------------

#### Day 61

##### MICE Imputation

- The issue with MICE is that is expects numpy arrays, not pandas DataFrames, in `X_completed[missing_mask] = average_imputated_values`
- My work around solution to get it to work [here](Titanic/notebooks/061-MICE.ipynb) is not scalable as apparently that kind of masking in 
pandas does not work consistently. 
- In future may be better to change the dataframe to a numpy matrix, perform `MICE` imputations, then turn back into a dataFrame:       
Change a `full_dums` dataFrame to a numpy array `fda` :     
`fda = full_dums.as_matrix()`     
`solver = MICE(verbose=0)`   
`fdac = solver.complete(fda)`      
This gets `fdac` array back to a labelled dataFrame:      
`full_dums_filled = pd.DataFrame(fdac, columns = [x for x in list(full_dums)])`
  


------------------
#### Day 60

##### Titanic

- `Mice.py` gives an error in the `complete` method of that class. Defined a new class for `MICE` in 
[059-Titanic_Rconvert](Titanic/notebooks/059-Titanic_Rconvert.ipynb) which allows us to create a new `complete` method for Mice (now called 
MyMice) and to diagnose what the problem is with the Mice code in `fancyinput`.

##### SQL

- Lessons 1 and 2 from [Intro to Relational Databases](https://www.udacity.com/course/intro-to-relational-databases--ud197) on Udacity. 
- Covers `PRIMARY KEY`, `SELECT`, `INSERT` and `JOIN`. `OFFSET` is new to me: how far into the results you want to display.

------------------
#### Day 59

##### ThinkBayes

- Chapter 6: Decision Analysis
- `class EstimatedPdf(Pdf)` takes a sample of data and makes a guassian_kde out of it. It provides method `Density(self, x)` which allows 
you to evaluate the density at any given value x using the samples kde. This is used when you call `MakePmf()` method of parent `class 
Pdf(object)` which takes a list of discrete values.     
E.g.   `pdf = EstimatedPdf(prices)` 
`pmf = pdf.MakePmf(xs)`  # call MakePmf method on the pdf object
  - `xs` is a list of discete values you use to make the pmf. 

##### Titanic

- must provide `index = False` when you write a dataframe to csv in `to_csv`, otherwise you end up with `Unnamed: 0` when you read it in 
again.
- use `fig, axes = plt.subplots(ncols=3, nrows=2, figsize=(12, 4))` to set subplots. You can reference their positions with 
`full['Age_IS'].plot.hist(alpha=0.5, ax=axes[0, 1])`
- Not quite able to get fancyimpute's MICE function to work, but I can extract the imputed values from the code and see if they are worth 
keeping. Next step - compare those values with my imputed values from earlier notebooks.
- [Today's notebook](Titanic/notebooks/059-Titanic_Rconvert.ipynb)

------------------
#### Day 58

##### ThinkBayes

- Prior = what does the historical data tell us the price might be?
- Update = after seeing the prizes, what do we think the price might be?
- Posterior = The two above give us a posterior distribution, but what do we do with it? Optimal bidding.
  - How to compute the optimal bid based on the players best guess. The optimal bid is price which maximises the 
expected return.
  - It is important to remember we are combining **two** sources of information: historical data about 
past showcases and guesses about the prizes you see.  
[Working here](tutorials/ThinkBayes/058 - Chap6_Optimization.ipynb)

##### Titanic

- Can use the test data to help fill in missing values. Previously I was just using training alone.
- Only look at the non-nan values in a column: `full['Cabin'].dropna()`
- installed `fancyimpute` so I can try out Multiple Imputation using Chained Equations (MICE) to fill in missing values.
- Make a new column with just the letter extracted i.e. from `C53` we get `C`: 
`full['Deck'] = full['Cabin'].str.extract('(?P<letter>[ABCDEF])')`
- Making a box and whisker in pandas: `bp = full.boxplot(column=['Fare'], by = ['Embarked','Pclass'])`
- Todays working [here](Titanic/notebooks/058-Titanic_Rconvert.ipynb)


--------

##### ThinkBayes

- Working on [Chap 6: Decision Analysis](tutorials/ThinkBayes/057 - Chap6DecisionAnalysis.ipynb)
Steps:
- *Model the Player* as a price-guessing instrument with known error characteristics. We incorporate those characteristics using historical 
data and computing a CDF of the differences between players bids and prices.
- *Likelihood* - make a new Suite class which includes defining the Likelihood. Uses the hypothetical price of the showcase (we don't know 
this, this is what we want to calculate) and the players guess and their error (price - bid).
  - for error given by price-bid, this is then check in the player model - we carry forward the proportion of error to model-player-error.
- *Update* - make a copy of the prior then invokes likelihood on each hypothesis (don't understand this bit), the multiplies the priors by 
the likelihoods and renormalizes.

##### Titanic

- Histogram! How to plot two bars from different arrays, next to each other.
- [Documentation](http://matplotlib.org/1.4.1/api/axes_api.html?highlight=axes.hist#matplotlib.axes.Axes.hist) on matplotlib axes.hist()
- Mosaic plot from `statsmodels.graphics.mosaicplot`. Working [here](Titanic/notebooks/057-Titanic_Rconvert.ipynb)

##### SQL

- Started setting up VirtualBox(no probs) and Vagrant(still working on) to enable me to do the project for the Udacity course.

------------------
#### Day 56

##### ThinkBayes

- The mechanics behind representing PDFs in thinkbayes is discussed in **Representing PDFs** part of **Chap 6: Decision Analysis**.
My notes and code are found [here](tutorials/ThinkBayes/056-RepresentingPDFs.ipynb).
  - **Kernel Density Estimation(KDE)** is an algorithm which takes a sample of data and finds an appropriately smooth pdf that fits 
the data. 
- Decision Analysis - given a posterior distribution, choose a bid that maximised the contestent's expected return. Steps:
  - Model the contestents, using `error = price - guess`.
  What is the likelihood that contestent's estimate is off by `error`? Use historical data to make `diff = price - bid` CDF.
  - Write the Likelihood
  - Write the Update
  - Use the posterior distribution from the above to create "Optimal bid" - maximises expected return.
- If all you need is a mean of maximum likelihood estimate, it may not be Bayesian that you need. 

##### Data Science Python

- OOP - created an equivalent to built-in `set()` with `class Set`
- using \__repr\__ in a class to determine what the class object printout will be
- using `partial` functions.
- If you apply multiple argument functions to `map()` in python 3, this returns a `map object` which you must use list comprehension on:    
`>def multiply(x, y): return x * y`    
`>products = map(multiply, [1,2], [4,5])`    
`>[x for x in products]`    
`>[4,10]`   
- filter()
- reduce() not built-in to python 3 use `from functools import reduce`
- \*args for unnamed arguments such as `x = [1, 2]` and \**kwargs for named arguments such as `y = { "z" : 3 }` can be combined together in 
a function such as: `func(*x, **y)` 
- All this working in [056-Chap2](DSFromScratch/Chap2/056-Chap2.ipynb).


------------------
#### Day 55

##### Titanic

- Joined up the training and test set in the beginning before doing the feature engineering! It will be split at the end again.
- `df.replace` is an important one for substituting several values at the same time i.e. 
`full['Title'].replace(to_replace = ['Mlle','Ms'], value = 'Miss',inplace=True)`

------------------

#### Day 54

##### Data Science Python

- a `set` is a collection of *distinct* elements
- `sort()` and `sorted()`
- controlling the work flow conditionally with `if`
- using `continue` and `break` in a loop
- list comprehensions 
  - in a list: `squares = [x * x for x in range(5)] #[0, 1, 4, 9, 16]`
  - in a dictionary: `square_dict = {x : x * x for x in range(5)}`
  - can include multiple fors: 
  `pairs = [(x,y) for x in range(10) for y in range(10)] # 100 pairs (0,0) (0,1)....(9,8),(9,9)`
- I am unsure about `generators` and `yield`
- `range()` in python 3 is a generator object.
- Generating random numbers with: `random.random()`, `random.seed()`, `random.choice()`, `random.randrange()`, 
`random.shuffle()`, `random.sample()`
- From the re module
  - `re.match` for beginning of strings
  - `re.search` for anywhere in string
  - `re.split("[ab]", "carbs"))`  # split on a or b to give ['c','r','s']
  - `re.sub("[0-9]", "-", "R2D2")])) # replace digits with dashes`
All working in [this notebook](DSFromScratch/Chap2/054-Chap2.ipynb)

------------------

#### Day 53

#### Titanic ML

[Another](https://www.kaggle.com/rahamoon/titanic/titanic/run/258564) interesting python/pandas feature engineering script to pick apart.
- I have improved my ranking to 1487 through [this](Titanic/notebooks/053-Titanic_new.ipynb) feature engineering. The [.py 
script](Titanic/bin/clean_test_53.py) which applies the same processes to test data. 
- [Here](Titanic/notebooks/053-DecisionTree_submit.ipynb) I try implimenting different ML techniques (DecisionTreeClassifier, 
RandomForestClassifier, GradientBoostingClassifier) 
- some ["tips"](http://scikit-learn.org/stable/modules/tree.html#tips-on-practical-use) for using scikit.learn Decision Trees

- As far as I can tell, there are two approaches to testing your model
  - split up your training data into test and training using `train_test_split()` and use `clf.score(X_test, y_test)`. Some knowledge may 
"leak" from the test set into the training set and there is risk of overfitting.
  - Use `sklearn.cross_validation.cross_val_score(clf, X, y, cv= 10)` where X and y are the original training data. `cv=10` is the number 
of times the dataset is split and it is split differently each time. This method is recommended.
      - From here you can use scores.mean() and scores.std() to check the validity of the score.

- Print out values rounded to 3 dp `print(["%.3f " %s for s in scores_std])`
- Could also use an F1 score with `scoring = 'f1_weighted'` in `cross_val_score` but I need to look into this. F1 measures a test 
accuracy, considering both precision and recall.


**Decision Trees**
- decision node: directs with a question
- leaf node: gives us a prediction
- A "greedy" algorithm will, at each step, immediately choose the best option. However, there may be a better tree with a worse-looking 
first move.


------------------
#### Day 52

##### Titanic ML

- Remove one part of a string from column 'Name' and make it into a key to search through "Title_Dictionary" in order to put into a new 
column, 'Title'.      
  `df['Title'] = df['Name'].apply(lambda x: Title_Dictionary[x.split(',')[1].split('.')[0].strip()])` 
- Should use a groupby object when finding the mean/median etc based on several groups. 
- `pd.get_dummies` splits up categorical data, i.e. male/female in df['Sex'] gets turned into:  
`Sex_female  Sex_male`     
`0   0.0         1.0`     
`1   1.0         0.0`      
- Point Biserial Correlation: used when one variable is dichotomous (jointly exhaustive and mutually exclusive), such as Gender. 
- Spearman - can use `scipy.stats.spearmanr(a, b=None, axis=0)`. Returns: r, p-value. Unlike Pearson, Spearman does not assume that both 
datasets are normally distributed.

- It's easy to make a dataFrame out of a dictionary 
- It is a good idea to make a dataFrame before visualising. 

- Use **Cross Validation** : `sklearn.cross_validation.cross_val_score(clf, X, y...)` to work out how many features you need to use.
- [Workbook](Titanic/notebooks/052-Titanic_new.ipynb) with the above.

------------------
#### Day 51

##### SQL

- Completed (and understood) Qu 13 on the Joins [Movie tutorial](http://sqlzoo.net/wiki/More_JOIN_operations). Now stuck on 16.

##### Think Bayes

- Baysian methods are most useful when you carry the posterior distribution into the next step of the analysis to perform some kind of 
decision analysis, or some kind of prediction.

------------------
#### Day 50

##### SQL

- More Joins using [this](http://sqlzoo.net/wiki/More_JOIN_operations) tutorial. Stuck on Qu. 13.

##### Think Bayes - Euro problem

- Beta distribution: Allows an update with two additions.
- Conjugate priors and distributions: If the prior and posterior distributions are in the same family.
- Swamping the priors: Given enough data, people with different priors will tend to converge on the same posterior.
- Cromwell's rule: Don't give a hypothesis a prior probability of 0, if there is ANY chance of it occurring. If p(H) = 0, p(H|D) will 
always be 0, no matter the data.
- [Notebook](tutorials/ThinkBayes/050-Euro.ipynb) with the Euro Estimation problem.

##### Titanic

- [Played around](Titanic/notebooks/050-pandas_vis.ipynb) trying to visualise the data with histograms to work out which features 
are important. 
- Overplotted subsections of histograms on each other, i.e. Age for survived/died.
- seaborn statistical package has some nice functions for plotting features. 
- resubmitted, changing column "FareBin" to "Fare" so that it matched the training set. It didn't make any difference. 

------------------
#### Day 49

##### Think Bayes

**Estimation**

- An example equation in Markdown:      
`\begin{equation} PMF(x) \:\alpha \left(\frac{1}{x}\right)^\alpha \end{equation}`
- [Locomotive example notebook](tutorials/ThinkBayes/049-Locomotive.ipynb). How many trains are there operating in a particular area? We 
investigate the possible ways to answer this. First using a set prior (i.e 1000 or 500) which gives a very uncertain number. This is 
improved by:      
a) adding more data (seeing more trains) 
or b) improving the prior (can we start out with a more realistic prior).                 
To use b, we introduce the power law into the hypothesis prior which provides a better first guess. 

**Credible Intervals and Cumulative Distribution Function (cdf)**

- A credible interval is the values between which there is a 90% chance that the unknown value falls between them.
- Use a cdf, rather than a pmf if computing several interval values at the same time. These two methods are 
shown [here](tutorials/ThinkBayes/049-Credible_intervals_cdfs)

#### Titanic Random Forest

- Have to remove any null values and turn the whole dataframe into floats. Remove or convert string columns.
- Repeated the data clean-up exercise for the training set, and in a [stand-alone 
script](Titanic/bin/clean_test.py) for the test-set, before calculating the [survival predictions using 
RandomForest](Titanic/notebooks/049-Titanic_RandomForest.ipynb).
 
------------------
#### Day 48

##### SQL

- Some good tutorials at [SQLZOO](http://sqlzoo.net/). Have made a new repository especially for 
SQL [here](https://github.com/SophMC/SQLtutorials).
- HAVING is used on GROUP BY objects, as WHERE can't be.


------------------
#### Day 47

##### Think Bayes

**Estimation**

- Investigating the probability you roll a 4,6,8,12 or 20 sided die, given the number (or list of numbers) that is rolled.
- Using numbers for hypotheses, create concrete class type (Dice) and write a new Likelihood method. Full explanation and working 
[here](tutorials/ThinkBayes/047-Dice.ipynb).


##### Titanic: Machine Learning

- Rewrote the [first tutorial](Titanic/notebooks/045-Titanic.ipynb) in pandas, and I much prefer it. Notebook [here](Titanic/notebooks
/047-pandas_prediction.ipynb).
- Some particularly useful snippets
  - `df.isnull().sum()` : null value count for each column
  - `df['Farebin'] = df['Fare'].map(binfare)` : using map to apply a function to each value in a column
  - `len(df[(df['Pclass'] == 2) & (df['Farebin'] == 1)])` : count how many rows match these criteria.

##### SQL  

- To read in a textfile delimited by spaces:      
`LOAD DATA LOCAL INFILE '../winds.txt' INTO TABLE Biskra FIELDS TERMINATED BY ' ';`
- To create a windspeed table:      
`CREATE TABLE Biskra (year integer(4), month integer(2), day integer(2), hour integer(4), ws float(10));`


------------------
#### Day 46

##### Think Bayes

- Making a framework for the Monty Hall problem. Notes on how this is done are in 
[this notebook.](tutorials/ThinkBayes/046-MontyHall_framework.ipynb)
- [Instructions](tutorials/ThinkBayes/046-ImplimentingSuite.ipynb) on how to impliment a Suite of hypotheses to create class Monty from 
[thinkbayes.py](tutorials/ThinkBayes/thinkbayes.py). Very useful!
- Using Suite from thinkbayes.py to calculate probability that an m&m came from a particular bag. I can't quite follow the code but have 
written notes in [this workbook.](tutorials/ThinkBayes/046-Suite_m&m.ipynb)
- **Suite** is an *abstract* type
- [**Monty**](tutorials/ThinkBayes/046-ImplimentingSuite.ipynb) is a *concrete* type: A class which extends an *abstract* parent class and 
provides an implementation of the missing methods. For example, Monty extends Suite, so that it inherits Update and provides Likelihood.

##### Titanic Machine Learning

- A good few more tips on using Pandas for data cleaning in [this Titanic tutorial workbook](Titanic/notebooks/046-Titanic_pandas.ipynb) 
(annotated by me):
  - Filling in columns with nans with "probable" values. The success of your ML could depend on the techniques you use to do this.
  - Keeping track of values which were filled in with "probable" values. 
- To do: rewrite the [first tutorial](Titanic/notebooks/045-Titanic.ipynb) in pandas.
- `df.isnull().sum()` : count number of null values in each column.


------------------
#### Day 45

##### Think Bayes

- [This workbook](tutorials/ThinkBayes/045-Cookie_framework.ipynb), using the "Cookie" problem, contains the code necessary to compute 
POSTERIOR probabilities for a suite of hypotheses, as well as being able to update these POSTERIOR probabilities with new data. 

##### Titanic Machine Learning

- I understand [this](https://www.kaggle.com/c/titanic/details/getting-started-with-python) Titanic python tutorial better now. We use the 
training set (with Survived) column to develop a model. Then apply the model to the test set with the final goal to produce an indexed list 
of prediction for each passenger. 
- Working [here](Titanic/notebooks/045-Titanic.ipynb), for a model which is based on gender, class (1st,2nd,3rd) and price (4 bins of $10) 
and produces the following prediction in [genderclassmodel.csv](Titanic/genderclassmodel.csv)
- Can't quite get the final model to print out. 

##### SQL

- Working through [24 SQL Interview Questions](https://www.toptal.com/sql/interview-questions) and 
[KhanAcademy](https://www.khanacademy.org/computing/computer-programming/sql) - great interface for learning SQL. 
- When comparing a value to Null, you must us `is`, not `=`. e.g. `null is null`, not `null = null`.


------------------

#### Day 44

##### Exercism Ex 6 - Word Count

- 'Write a program that given a phrase can count the occurrences of each word in that phrase'
- My solution [here](tutorials/exercism_py3/word_count/wordcount2.py). I couldn't get it to pass the [last 
test](tutorials/exercism_py3/word_count/word_count_test.py). It has trouble detecting the space in the 
russian characters. 
There is no `str.decode()` in python 3 as everything is decoded from UTF-8 already. I need to look through more of other peoples 
submissions. [For example](tutorials/exercism_py3/word_count/wordcount3.py) this works but I'm not sure why 
yet. 

------------------
#### Day 43 

##### Bayes's Theorem

- Cookie problem and Monty Hall Problem from [Think Bayes](http://www.greenteapress.com/thinkbayes/thinkbayes.pdf)
- Have started using the module [ThinkBayes.py](tutorials/ThinkBayes/thinkbayes.py) written by the author, to follow the Computation 
Statistics: Distributions chapter. Have converted bits of it from python 2 to python 3. i.e. `itervalues()` to `values()`.
- [Cookie problem notebook](tutorials/ThinkBayes/043-Distributions.ipynb), using pmf module. 

##### Machine Learning - Titanic Kaggle comp

- Going through [the tutorial](https://www.kaggle.com/c/titanic/details/getting-started-with-python) using python 3, to become acquainted 
with open(), read_csv(), next() standard python modules, rather than pandas.  
- [Notebook](Titanic/notebooks/Titanic_explore.ipynb) with the first step: creating a gender-based model. Consistst of Passengerid and 
Survived, though I am confused, as it should perhaps be Sex because it is binary 1 or 0 for female/male.


------------------
#### Day 42

##### Bayes's Theorem

- Learned the following terms from [Think Bayes](http://www.greenteapress.com/thinkbayes/thinkbayes.pdf).
  - Conditional and Conjoint probability
  - How to derive Bayes Theorem
  - Diachronic Interpretation
    - Specify a 'suite' of hypotheses that are *Mutually Exclusive* and *Collectively Exhaustive*
    - Then you can use the *law of total probability*

##### Windspeed

- Resolved and closed github [issue](https://github.com/SophMC/notechain/issues/3) with DateTimeIndex.


------------------
#### Day 41

Make a website for your project with [Github pages](https://pages.github.com/). An example 
[here](http://cs109.github.io/2015/pages/projects.html).

[Building a data science portfolio](https://www.dataquest.io/blog/data-science-portfolio-project/).

##### K-means

- I don't fully understand each step in [this example](tutorials/K-means/MNIST.ipynb) of using PCA and Kmeans with sklearns [digits 
dataset](http://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_digits.html) but I've tried to unpick most of it and 
annotated it a bit further. 
- `np.linspace(start,stop,num)` where num = num of equally spaced samples
- `np.tolist` Return the array as a (possibly nested) list.

##### Windspeed

- Finally managed to convert a MultiIndex into a dateTime index for date data. Full working 
[here](windspeed/notebooks/041-Tidjika_faya.ipynb).      
  `df['date_time'] = df[['year', 'month']].apply(lambda x: pd.to_datetime('/'.join(x)), axis=1)`
- The plot format is looking much better, though I still don't have the xaxis in the format I want.
At the moment it is like [this](windspeed/plots/WSahel.png) and I want the month and year to be displayed on top of each other. 

##### Exercism Ex 5

- Counting the differences between two dna strands
- Got to [my solution](tutorials/exercism_py3/Ex5_hamming/hamming.py) fairly quickly. 
[Here](tutorials/exercism_py3/Ex5_hamming/hamming2.py) is a two-liner using `zip()`.

------------------
#### Day 40

##### Windspeed

- If there is an observation at 1200 and 1224, these both get converted into the time index:
`1987-04-04 12:00:00`. This leads to duplicate values in the Index (bad!).
These are found with the code `wind.index.value_counts()`.   
- dropped duplicated rows based on the 'date_time' column. 
- This fixed the mysterious `ValueError: cannot reindex from a duplicate axis` which occurred at Niamey.
- All groups are printing plots now, but still need to fix an error with the xaxis at Tidjika and Faya.
- [Working script](windspeed/scripts/040-group_tseries.py) and the above problem [investigation](windspeed/notebooks/040-Niamey_issue.ipynb)

##### Kmeans

- Once the optimal number of clusters is found from the elbow curve plot, you can split the data into the number of clusters. If 
you you have 3 clusters, your data is split into 3 classes. Like, walking, standing, sitting etc. in the Samsung example. 
- [kmeans.py](tutorials/K-means/kmeans.py) is a good example of making your own function so that you can easily change variables 
in a plot. What I have been trying to do for windspeed. 
- The process is similar to Linear, Logistic and Random Forests:
  - Set up the model (Linear `sm.OLS()`- , Logistic - `sm.Logit()`, Random Forests - `sk.RandomForestClassifier()`, Kmeans - `KMeans()`)
  - Fit the model to some data (model.fit())
  - Make predictions using (model.predict())


##### Exercism Ex 4

- Mapping dna sequence to rna sequence.
- Used a dictionary to map letters `d={'G':'C','C':'G','T':'A','A':'U'}`
- used `''.join([d[m] for m in p])` to loop over input such as 'GCTTA' and return it as 'CGAAU'
- [My submitted solution](tutorials/exercism_py3/dna/dna.py)
- [Another solution](tutorials/exercism_py3/dna/dna2.py) using `str.maketrans(intab, outtab)` - A very easy way to substitute characters.

------------------
#### Day 39

##### K-means - [notebook](tutorials/K-means/039-kmeans_exploredata.ipynb)

- Create a list of code books and distortions(tuples in KM).        
- Extract code books to a list of their own(centroids).    
- Each code book has [n_cluster, n_features], where n_features is the number of columns.     

Here it gets  a little tricky

- For each cluster set (ie. using 1,2,...10 clusters) we make a distance matrix (D_k). Shape=[n_rows,n_clusters]. I'm not sure where 
different features (columns) disappear to in this step.     
- For each cluster set we have an accompanying indices-of-mins(cIdx) and values-of-mins(dist) matrix.
- We find the average min for each cluster set `avgWithinSS = [sum(d)/X.shape[0] for d in dist]`. This will be used to find the k "elbow" 
(where the improvement from increasing the number of clusters starts to drop off.)

##### Windspeed

- Script was getting stuck at Ouargla as there was no data in my sub-set period.
- Have put an assertion in to warn that a station will be skipped if no data. 
- [Script](windspeed/scripts/039-group_tseries.py) after today.

------------------
#### Day 38

##### Python 3

**Ex 3 Pangrams**
- [set()](https://docs.python.org/3/library/stdtypes.html#set) creates class object which you can use to query the unique values in a list. 
   
e.g. `set(list) >= set(other)` or `list.issuperset(other)` : is every element of other found in list? 
     ``
- `s.lower()` is the key to dealing with non-english letters in the line:   
`return len(list(set(letters.lower())))== 26` in my submission [here](tutorials/exercism_py3/pangram/pangram.py).      
Also need `# -*- coding: UTF-8 -*-` at the beginning of the script.    
- use \u to insert a unicode character       
- `re.sub(pattern,repl,string)`       
  `letters = re.sub('[^a-zA-Z]','',s)` to get rid of anything not a letter.   
- My submission was heavily influenced by this [amazingly short 
one](tutorials/exercism_py3/pangram/pangram2.py) which helped me work my solution out.
I started out lots of [unnecessary code](tutorials/exercism_py3/pangram/pangram_detailed.py).

##### SQL

- DELETE FROM tablename : deletes all the records in a table, but the table name and column constraints remain.  
- DROP TABLE tablename : if you want to completely remove the table.
- Now on to [SQL Course 2!](http://www.sqlcourse2.com/) which focuses entirely on the SELECT command.

##### Windspeed

- In the read_file functions of [p3group_tseries](windspeed/scripts/038-group_tseries.py) I've made two small functions to calculate the 
mean over each group, while returning nan if the group has less than 10 obs. Should these small functions (meanf,sdf) be inside or outside 
read_file?
I read in only read_file into the [following notebook](windspeed/notebooks/038-group_tseries.ipynb) and somehow it still accessed meanf and 
sdf.

- One way to drop month from the tuple creating the messy xaxis (see [here](windspeed/plots/038-62124Sebha.png)) is to drop the month level 
from the MultiIndex created when using groupby. droplevel() is one of a [few 
methods](http://pandas.pydata.org/pandas-docs/stable/api.html#multiindex) that can be applied to MultiIndex objects
`wind_group.index = wind_group.index.droplevel(['month'])`   
Now gives an xaxis with just year, [here](windspeed/plots/038-62124Sebha_2.png), though 1995 is missing.

##### Linux

- `eog image.png` in the terminal to quickly view an image. 

##### K-means clustering

- Started K-means analysis [here](tutorials/K-means/038-kmeans_exploredata.ipynb)
- numpy array [attributes](http://docs.scipy.org/doc/numpy-1.10.1/reference/arrays.ndarray.html#array-attributes) 
and [methods](http://docs.scipy.org/doc/numpy-1.10.1/reference/arrays.ndarray.html#array-methods).


------------------
#### Day 37

##### SQL

- Practised INSERT INTO and UPDATE into table.

##### Windspeed

- More working in [this notebook](windspeed/notebooks/037-group_stations.ipynb) to plot:      
  - Different time slices from a groupby object.      
  - Several subplots within one figure.         
- Implimented the above in [my script](windspeed/scripts/037-group_tseries.py), trying to use oop. Can't get it to run.

------------------
#### Day 36

##### SQL

- `LIKE` is powerful, similar to grep.    
  `SELECT first, city`   
  `FROM empinfo`            
  `WHERE first LIKE 'Er%';`  select from rows first and city in tabel empinfo where the first two letters are Er.
  
- CREATE TABLE: don't forget to fill in the right data type for each column:               
`CREATE TABLE myemps_smc (first varchar(15),last varchar(20),title char(10),age number(2),salary number(8));`

##### Windspeed

- Solved my problem of aggregating grouped columns based on the number of observations going into each group. See working 
[here](windspeed/notebooks/036-group_stations.ipynb) in the last cell.

##### Python 3

- exercism.io: 
  - Ex 2 - Determing if a year is a leap year. [My (revised) answer](tutorials/exercism_py3/leap/year4.py). A [crazy short 
one](tutorials/exercism_py3/leap/year5.py) which passes the test. So many fascinating and different ways to do this. 

##### K-means clustering

- Overview. Used to discover natural groupings in data. An example of "unsupervised" learning where we don't have any original 
classification to "train" the data. [Experimented](tutorials/K-means/Iris_explore.ipynb) with the known groupings of Iris data. 
- K-means can be used to:
  - determine ambiguous terms in a document. Is a Jaguar a car or an animal? What words cluster nearby? What is the whole document about?
  - Initial exploration when training samples are not available.

------------------
#### Day 35

##### Git

- To find a particular commit, just add commit/commitnum to the end of your URL i.e.:    
`https://github.com/SophMC/notechain/commit/d61ca5f`

##### Conda python 3 environment

To create a python 3 environment to work on:           
`conda create -n py3 python=3.5 anaconda` : creates an environment named py3, using version 3.5       
`source activate py3` : activates the py3 env            
`source deactivate` : back to old env         
`conda remove -n py3 --all` : remove py3 environment          

##### Python 3

- exercism.io, exercise 1 "Hello World". Not as simple as I initially thought.     
[My answer](tutorials/exercism_py3/hello-world/hello_world.py) was much longer than the two lines that most of the others ([an 
example](tutorials/exercism_py3/hello-world/hello_world2.py)) which made the tests pass but didn't do exactly what [the 
instructions](tutorials/exercism_py3/hello-world/README.md) asked. 

- no longer a dedicated `xrange()` in python 3. `range(start, stop[, step])` does the business.


##### Random Forest - black box method

- `rfc.feature_importances_` gives the relative importance of each feature in the forest. Sum=1.     
- plotting two confusion matrices next to each other using:         
`fig = pl.figure()`    
`fig.add_subplot(121)` : (122) for the second plot. 1x2 grid, 2nd plot.        
`pl.matshow(test_cm,fignum=0)` : fignum=0 was the key point to prevent a new fig being created.

- In the end the black-box model is easier because you don't have to read the documentation or spend any time wrangling the column names.
- It gives greater accuracy/precision but adding domain knowledge allows you to focus in on the relative importance of the features which 
are important to you, depending on you are trying to find out. 
- [Black Box notebook workings](tutorials/Samsung/notebooks/035-Samsung_analysis_blackbox.ipynb).

------------------
#### Day 34

##### Random Forests

- Create an instance of the class RandomForestClassifier (rfc). We then have a large number of methods that can be applied.
- RandomForestClassifier fits a number of decision tree classifiers on various sub-samples of the dataset and uses averaging to 
improve the predictive accuracy and control over-fitting.
- Methods `predict()`, then `score()` - in that order are applied to our object, rfc.
  - `rfc.predict(X)` - takes input samples, X, and returns the predicted class
  - `rfc.score(X,y)` - returns the mean accuracy of predict(X) with respect to y (true labels for X)
- Attributes such as 
  - `oob_score_` - model accuracy estimate
- Two different ways to drop the mystery "unnamed column"
  - `samtrain = samtrain.drop(samtrain.columns[0], axis=1)`
  - `samtrain.drop(samtrain.columns[0], axis=1, inplace=True)`            

All this working is in [this notebook](tutorials/Samsung/notebooks/034-Samsung_analysis.ipynb).
 
##### Windspeed plotting

- Select a column by integer `wind.iloc[:,3]` --> select all rows in 4th column. How can iloc be combined with multiIndex?

##### Python

- To learn Test Driven Development(TDD) I set up the exericsm.io [command line interface](http://exercism.io/cli) so I can [practise python 
problems](http://exercism.io/languages/python) and get feedback on them.  Installing 
[linuxbrew](http://linuxbrew.sh/) seemed the easiest way to get it all set up right. 

-------------------
#### Day 33

[Data Tau](http://www.datatau.com/) - Hacker news for data science.

[Good list](https://github.com/ujjwalkarn/DataSciencePython) of Python resources for data science

##### Windspeed plotting

- Can't work out how to apply `map()`, `filter()` or `apply()` to my messy groupby object.    
Instead of `mean` and `std` passed to agg() in the following line:     
`wind_group = group['ws','ws_0','ws_06','ws_12','ws_18'].agg(['mean','std','count'])`    
I want to pass functions in their place which would only assign the mean for the group, if count > 10, otherwise assign nan. 
- The difficulty is navigating the different levels of indices (year and month) and columns (for each of 'ws', 'ws_06'..etc. there is 
another level with mean, std and count. See all this unintelligible working [here](windspeed/notebooks/033-group_stations.ipynb).


##### Random Forests (Samsung data)

- Worked out that the remap_col() function was made by the author - I made accessible copy of the randomforests.py module to 
get the function.     
- Started working with sklearn.ensemble.RandomForestClassifier to build a random forest model. Will upload the workbook when it is finished 
tomorrow.


##### SQL 

-CREATE INDEX speeds up finding values in a table.     
Syntax: `CREATE INDEX index_name ON table_name (column_name)(or col1,col2,col3)`    
  `CREATE UNIQUE INDEX` to create a unique index on the table

- Go through [this tutorial](http://www.sqlcourse.com/) and do the exercises. There is also an [more advanced 
one](http://www.sqlcourse2.com/), which I have covered some material from. 


-------------------
#### Day 32

[DataKind](http://www.datakind.org/) looks like a good place to find an interesting project to work on. 


##### SQL - Qu 19

- `CREATE TRIGGER name when event ON tablename action`. Another way of enforcing integrity (similar to constraints).
- In theory my Qu 19 solution should work, but it doesn't. I checked with the author and he says there may be a bug. Investigate 
tomorrow.

##### Random Forests

*data cleaning*

- I *can* access samtrain.csv etc...from github. Not sure it is possible to get it into the correct format with the 
information in the tutorial.
- Tomorrow email author and continue with the analysis now I have correctly formatted data.

##### Windspeed plotting

- getting my head around `map()` and `filter()` and using lambda to make functions in them. Still can't get these things to work with 
grouped dataframes though. 

-------------------
#### Day 31

[CrowdFlower](https://www.crowdflower.com/)
Sentiment analysis which encorporates human intelligence to identify nuances in the sentiment of text.    
Used as a benchmark by MonkeyLearn to [evaluate their 
performance](https://blog.monkeylearn.com/sentiment-analysis-apis-benchmark/?utm_source=Email&utm_medium=Intercom&utm_content=FP&
utm_campaign=22-sentiment-analysis-benchmark) against other platforms such as MetaMind, AlchemyAPI, Aylien, Idol and Datumbox

##### SQL - Qu 18

- UNION: Combines queries, discards duplicates.   
- UNION ALL: Same as UNION, keeps duplicates.     
- INTERSECT: Only returns rows which match.   
- EXCEPT: performs set subtraction (those which don't match the SELECT statement).

#### Random Forests

*Data cleaning*

- [Final go](tutorials/Samsung/notebooks/031-Samsung_cleanup.ipynb) at reducing variables to the list in the tutorial. 

#### Windspeed plotting

- [My failed attempts](windspeed/notebooks/031-group_stations.ipynb) to create a grouped dataFrame where counts less than 10 are turned 
into Nans, without a loop. Will just do it will a loop tomorrow. 

-------------------

#### Day 30

##### Random Forests

*Data cleaning*

- Stick to `df.replace` and `df.contains` for dataFrames, as opposed to python `re` module, which would need loops.
- Worked out how to search for two different words within one string:
  
    `df[df.name.str.contains('Body.*Mag')]`

- Almost there with [this workbook](tutorials/Samsung/notebooks/030-Samsung_cleanup.ipynb) - have changed strings and dropped rows with 
certain expressions. There is still work to do as my list of remaining names is not the same as that 
[here](http://nbviewer.jupyter.org/github/nborwankar/LearnDataScience/blob/master/notebook/C2.%20Random%20Forests%20-%20Data%20Exploration.ipynb) 
in the tutorial.

##### SQL

- I got Qu 17 to work with [my own solution](SQL/galaXQL_17.sql)!
- Practised using GROUP BY, INNER and LEFT OUTER JOIN and understand them much better. 

##### Windspeed plotting

- Got the first function of [my .py script](windspeed/scripts/030-group_tseries.py) working (read_file) so that I can access it in [jupyter 
notebook](windspeed/notebooks/030-group_stations.ipynb).

##### General Python

- To add a path to a directory with modules that you want to call on:

`import sys`     
`sys.path.append("path/to/Modules")`        
`print sys.path`
   
It's better to have fewer of these though, and store most of your modules in the same place. 

- STUCK - if I restart the Jupyter kernel (which I think I have to do everytime I update the module group_tseries) then it no longer 
finds the module

-------------------

#### Day 29 

##### Random Forests 

*Theory*

- Out of Bag (oob) error: Using the subset that is left out of the bootstrapping sampling to test the decision trees (models). As accurate 
as using a test set the same size as the training set.

*[Data cleaning](tutorials/Samsung/notebooks/029-Samsung_cleanup.ipynb)*

- Did some initial search and replace in Kate of [this list](tutorials/Samsung/data/features_copy.txt) of 
variable names
- Removed duplicate columns using df.drop_duplicates().
- Removed "()", "-" and numbers from the list of names.

##### SQL

- ALTER TABLE tablename alteration(RENAME TO, ADD COLUMN, RENAME COLUMN TO, MODIFY COLUMN, DROP COLUMN)
- Show the columns in a table:
  - SQLlite - PRAGMA table_info(tablename)
  - MySQL - SELECT * tablename.INFORMATION_SCHEMA.COLUMNS (There is a long list of other things that can be queried other than COLUMNS)
- GROUP BY and HAVING (an equivalent to WHERE, applied to the grouped data) (Ex 17)
- Couldn't do Qu 17 myself - must learn and understand the solution (copied!)
 

--------------------
#### Day 28

##### SQL 

- CREATE TABLE tablename(columnname datatype constraints). (Qu 14)
- constraints: PRIMARY KEY, NOT NULL, UNIQUE, FOREIGN KEY, CHECK
- To fill the table: INSERT INTO tablename(column1,column2) VALUES(column1value, column2value). (Qu 15)

##### Random Forests 

*Theory*

- **Classification**: Task of assigning objects to one of several pre-defined categories.   
- **Bootstrapping**: Random sampling WITH replacements. Repeatedly sampling from the same sample.    
- **Bootstrap Aggregation (Bagging)**: Each model in an ensemble has an equal weight. Each model is built in parallel. Example: Random 
Forest.   
- **Boosting**: Can be better than Bagging. Models are built sequentially and learn where previous models were strong/weak and weight them 
accordingly. Example: AdaBoost

--------------------
#### Day 27

##### Markdown

- use \$a_2$\ to create maths symbols $a_2$
- [Guide](https://en.wikibooks.org/wiki/LaTeX/Mathematics) for writing equations in Tex.

##### Lending Club Linear Regression

- Finished [the workbook](tutorials/026-Linear_Regression_Analysis.ipynb). Didn't show how to make predictions using the model.

##### Lending Club Logistical Regression

- Using the Log Function to predict the probability that score x will lead to a win.
- Log Function = Logit function combined with Linear Model.    
  1) Work out the coefficients for multivariate linear regression    
  2) Plug the variables(we want to query) and coefficients(worked out in step 1) into Z(equation of a straight line)     
  3) Calculate the probability of Z using p(Z) = 1 \ 1+ e^(Z)       
- Plotted how probability varies with Loan amount and FICO score (changing the colour/symbols). See 
[here](tutorials/027-Logistical_regression.ipynb)


--------------------

#### Day 26

##### SQL [tutorial](http://sol.gfxile.net/g3/)

- INNER JOIN, OUTER JOIN (Qu12)
- CREATE VIEW (Qu13)

##### Lending Club Linear Regression 

- Modelling Interest rate as a function of Loan Amount and FICO Score. Steps:
  - Put the pandas columns into seperate variables. Turn these into 2D arrays and into columns eg `x1=np.matrix(fico).T`
  - Put the two idependent vars into a stacked 2D array `x = np.column_stack([x1,x2])`
  - Add a constant (a column on 1s) to x:  `X = sm.add_constant(x)`. X is now x.
  - Create an ordinary least squarts model with `model = sm.OLS(y,X)`, y=response, X=independents+constant
  - Apply a fitting method to the model. `f = model.fit()`
    - There is now a list of attributes to f, such as `f.params`(coefficients), `f.pvalues`
    
Full notes and working [here](tutorials/026-Linear_Regression_Analysis.ipynb).



--------------------
#### Day 25

##### SQL [tutorial](http://sol.gfxile.net/g3/)

- Best to use transations (BEGIN; ROLLBACK) when using UPDATE or DELETE
- COALESCE(value1,value2,value3) returns the first non-NULL value in a list
- Using UPDATE with WHERE to only update columns if they meet a criteria
- Can't get my head around the query:     
  `SELECT COUNT() FROM stars, (SELECT AVG(intensity) AS ai2 FROM stars, (SELECT AVG(intensity) AS ai FROM stars) WHERE intensity > ai) WHERE 
intensity > ai2` --> count the stars that have higher than average intensity of only those stars that have higher than average intensity.

##### Indexing tutorial

- Using `isin()` together with `all()` to select particular values from particular columns in a DataFrame.
- Using `where()` to select values, change them inplace and change them with values from other columns.

##### Windspeed groups

- `type(obj)`  to find the object type.
- Improved the code by adding the 06,12 etc values to the wind dataframe, then grouping them all at the same time. 
`wind['ws_06']= wind['ws'][wind['hour'].isin([6])]`     
`group = wind.groupby(['year','month'])`        
`wind_group = group['ws','ws_0','ws_06','ws_12','ws_18'].aggregate([np.mean,np.std])`        
Now these will be much easier to plot against each other. Can even use a loop to do it. 

#### Todo list

- [These are](TOdo.md) the learning resources I am in the process of working through. This is the very minimum I would 
like to get through in the next couple of months!

--------------------
#### Day 24

##### SQL [tutorial](http://sol.gfxile.net/g3/)

- Must use brackets around a query using OR.      
  `SELECT * FROM stars WHERE starid>1000 AND starid <2000 AND (class=0 OR class=1)`
- `<>` for NOT.    
- `ORDER BY ..` for ascending `ORDER BY .. DESC for descending`
- BEGIN;..queries...ROLLBACK to "undo"
- INSERT INTO .. with SELECT..

##### Indexing tutorial

- `list('abcdef')` splits up the string into a,b,c,d,e,f. Good to remember! 
- selecting from df using lambda function 
  - `criterion = df2['a'].map(lambda x: x.startswith('t'))`   
    `df2[criterion]`
    
##### Windspeed group plots

- nearly broken the back of this, hope to complete tomorrow.

--------------------
#### Day 23

##### SQL

- Using REGEXP(RLIKE) to find patterns. Using ^ and $ to specify beginning and end.
- '[abd]' finds any values which have a, b or d in them. '[0-9]' to find a number.
- Going to do [this](http://sol.gfxile.net/g3/) tutorial from now on.

##### Index tutorial

- Working through the Pandas [basics of indexing](http://pandas.pydata.org/pandas-docs/stable/indexing.html). Need to get a good grounding 
in this. Notebook found [here](tutorials/023-indexing.ipynb).

##### Windspeed group plots

- Working on a script which produces a panel of plots for a group of stations in one output file. 


--------------------
#### Day 22

#####boxplot with width = counts

My annotated working through a tutorial [here](tutorials/022-boxplot_counts.ipynb).

Applied to a subsection of windspeed data [here](windspeed/notebooks/022-windspeed.ipynb).
  - used `ax.set_xticklabels()` to add a counts label to each tick.     
  - splitting up tuples to get counts `counts = [len(v) for k,v in windg]` where windg = grouped object 

#####datetime

- pd.to_datetime and datetime both need year, month and day. I don't think it is possible to just do with year and month.

#####SQL
- You can extract parts of a date from a column (type=date) using functions YEAR(), MONTH() and DAYOFMONTH()
- An empty string in a cell IS NOT NULL. so " " IS NOT NULL = 1 (true)
- Use LIKE instead of = and NOT LIKE instead of !=
- Find names with a w in table pet: `SELECT * FROM pet WHERE name LIKE '%w%';`
  - % is like * or `wildcard`
- Find something with 5 characters; '_____' (5 _ underscores)

--------------------

#### Day 21

#####MySQL

`mysql -u root -p --local-infile` if you want to load local files into a database.
  
Today covered:
- Making a new database (CREATE DATABASE)
- Select database to work on (USE ..). Don't need semi colon ';'
- Making a table in a database (CREATE TABLE)
- Inserting values into the table (INSERT INTO table VALUES (list of values))
- Loading data from a locally stored text file into the table (LOAD DATA)
- Changing a record in the table (UPDATE table SET .. WHERE ..)
- Selecting unique values form a column (SELECT DISTINCT column FROM table;)   
Finished with [datetime selections](http://dev.mysql.com/doc/refman/5.5/en/date-calculations.html)


--------------------

#### Day 20

#####MySQL

- Installed version and client 5.5, using [this 
tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-14-04)

- To remove current version, to make way for new version (5.6 - 5.7 is available too) follow 
[this](http://askubuntu.com/questions/489815/cannot-install-mysql-server-5-5-the-following-packages-have-unmet-dependicies)  

- To log in `mysql -u root -p` and it will ask for a password.

#####windspeed plotting 

- Make index a datetime object - easier to slice when plotting i.e.     
`wind.index=wind['date_time']`        
`year_sub = wind['1997':'2001']`          
`plt.plot(year_sub.date_time,year_sub.ws)`      

- I want to create a box and whisker plot, with the number of observations on top for each box and whisker. The issue is sharing the x-axis 
between the two sets of data. Its nice to use pandas for making the boxplot (very easy to create groups), but very hard to then plot a line 
of counts which correspond to each boxplot (labelled with a MultiIndex!).

- Violin plots might be an interesting alternative. 

Workings [here](windspeed/notebooks/020-windspeed.ipynb)

--------------------
#### Day 19

#####MySQL   

Learned some basics:
- Noticed lots of similarities to ideas from python oop. 
- SQL has classes with attributes, these are similar to python class attributes.
Python class methods are called associations in SQL and the associated class is a child of the parent (which the child inherits attributes 
from)    
- Each row is a tuple.   
- Super Key (SK), Primary Key(PK), Foreign Key(FK), Candidate Key(CK), surrogate PK and substitute PK.    


#####windspeed plotting

- Opened an issue on creating the datetime index from a grouped dataframe and `reset_index()`
- Could still achieve the above using a loop.
- Some overplotting of different frequency data and shaded error region

Notebook found [here](windspeed/notebooks/019-windspeed.ipynb).

*To do* - make a script to group stations, make panels of plots, and output them to a file per group. 

--------------------
#### Day 18

#####windspeed plotting

- Used `reset_index()` to add a datetime index to a dataframe created from a groupby() object with monthly averages.
- First tried to do the above with a loop and MultiIndex- it worked fine.
- Subsections can be selected by specifying datetimes as strings e.g.    
`w['mean']['1998-05':'1998-10'].plot(yerr=w['std'])`. 
- Plotted some error bars and a shaded error "band"

Have added an [updated version](windspeed/notebooks/018_2-windspeed.ipynb) of this because the datetime index was wrong and I have no idea 
how it worked [here](windspeed/notebooks/018-windspeed.ipynb).

--------------------
#### Day 17

#####windspeed plotting

- Select rows based on two different conditions in two different columns. 
I was nearly there before - just needed brackets around each condition!  
`onemonth = wind[(wind['year']== 1984) & (wind['month'] == 3)]`
This selects rows from march in 1984.   

- Grouping and averaging data using `df.groupby` and `.aggregate([np.mean,np.std])`.  

- Using lambda to define a function to pass to transform():   
  `f = lambda x: x.mean()     
   transformed = grouped.transform(f)` 

- Some very simple code for plotting a comparison between an averaged dataset and it's original:
`compare = pd.DataFrame({'Original':wind['ws'], 'Transformed':wind['mean_ws']})`   
`compare.plot()`

- Experimented a little with plotting std error bars. 

[Notebook](windspeed/notebooks/017-windspeed.ipynb) with the working


--------------------
#### Day 16

#####windspeed plotting

- Used pandas plotting. `df.plot` is a wrapper for `plt.plot(df)`.    
- Plotted density functions (kind='kde') of ws at different times of day.  
- Overplotted several lines in one plot.    
- Added a legend.     
- Specified the colour of each line.    

Averaging timeseries data:

- resampling using resample() is handy with datetime information, but you have to turn it into an index. There are two steps here, first you 
have to make object with resample, then apply `.agg()` do do the statistics (mean, std).     
- couldn't upsample the mean and std for each month to the same irregular original array, though it is very easy to make it 
into a regularly spaced array. Could do that, then match it to the original array. 
- Or, use groupby `grouped = wind.groupby(['year','month'])` though I haven't worked out if this is actually doing what I want, and if it 
is possible to upsample it to the original array.

[See the notebook](windspeed/notebooks/016-windspeed.ipynb) for the working.

--------------------

#### Day 15 
#####Markdown

I configured Kate to extend the line length limit to 140, up from 80. This should reduce the problems from long web links.

#####Monkey Learn visualisation

Enriching the [raw data](monkeylearn/indeed_edin.csv) with Monkeylearns API, 
with the help of pandas and requests in python, found 
[here](monkeylearn/015-selectdata.py) led to this plot in plot.ly: [Industries which hire data scientists in 
England](https://plot.ly/~SophMC/6/industries-employing-data-scientists-in-england-indeedcouk/).  


#####Plot.ly

I can produce a graph in ipython notebook and it will appear on the plot.ly 
account online, along with a table with the data.    
This is publicly available, privacy is paid for.




--------------------------
#### Day 14
#####Import.io

I'm trying to work through a short 
article which uses import.io (to scrape 
lists from the web) and Monkeylearn (to get data from text using machine 
learning) to ["Create an Employment Analytics Visualization in Less Than 10 
Minutes"]
(https://blog.monkeylearn.com/how-to-create-an-employment-analytics-visualization-in-less-than-10-minutes/). It's definitely taken 
me more than 10 mins due to lots of teething 
problems with import.io.

- Can use [magic import.io](https://magic.import.io/examples) to very quickly 
get up to 20 consecutive pages.

- Better to input the values manually in the [extractor 
page](https://dash.import.io/) if you have more than 20 pages. Use excel to 
change the last digit i.e.

```http://www.indeed.co.uk/jobs?q=data+scientist&l=England&start=10
http://www.indeed.co.uk/jobs?q=data+scientist&l=England&start=20
http://www.indeed.co.uk/jobs?q=data+scientist&l=England&start=30
```

It took 7mins to scrape the data from 203 pages. 




--------------------------
#### Day 13 

#####Windspeed Plotting
`list(df)` - really nice way to show dataframe column names

[New script](windspeed/scripts/013-ws_tseries.py) where I am trying to practise 
using OOP methods with classes. Whether it is suitable or not for the problem I 
am not sure. So far, the script does the following (you can download [3 data 
files](windspeed/data) to try it with):

* Shows you a list of N African stations from which you can pick the index.
* Gives you options to; 
    - Give descriptive statistics
    - Make a time series plot to view 
    - Save a copy of the plot

The few final things I want to get into this script before I will move on:

* Plot the timeseries in monthly bins (error bars)
* Make a nice plot with 4 timeseries on the same plot from obs at 00,06,12 and 
18
* Design a test script (really need to practise this!)

I will test the ideas out in a notebook first before trying to organise them in 
a script with classes and methods. 

---------------------------

#### Day 12

#####Web App Building

A [very primative game](gothonweb) which can take an input and move to another 
page, based on the user input. It only works for the first two rooms. I think 
you will pretty much die whatever input you put after that. 

Instructions:  
* Download /notechain/gothonweb recursively.
* Inside /gothonweb entering: `python
bin/app.py` should return `http://0.0.0.0:8080/` to the terminal.
* Copy `http://localhost:8080/game` into your address bar.
* Follow the game!

The [tutorial](http://learnpythonthehardway.org/book/ex52.html) suggests a lot 
more refining but spent as much time on this as I want to.

#####Windspeed plotting
I want to make a script using and classes and functions which can: 
- Allow a file to be selected by the user from a list of files in the directory 
- This will then be plotted as a timeseries of windspeed, split 4 lines of 
winds at 00,06,12 and 18.
- The graph will be output into a image file.

So far I have made [this mess](windspeed/notebooks/012-ws_tseries.py). Maybe functions 
and classes are just not needed for this task, or maybe I don't really have a 
clue on how to apply them. 

---------------------

#### Day 11
#####Plotting windspeed


Opened an [issue](https://github.com/SophMC/notechain/issues). Not able to use 
`df.query()` as apparently `numexpr` is not supported. 

The following working is in 
[011-windspeed.ipynb](windspeed/notebooks/011-windspeed.ipynb).   
`%matplotlib inline` ensures plots display in the notebook

`plt.plot(xaxis,yaxis)` `plt.xlable()` `plt.show()`   
Change size of x ticks `plt.rc("font", size=7)`

Three different ways to use `pd.astype()`

To make a sub-set of data (a more limited method):  
1) create a mask `row_mask = wind['year'].isin([1985,1986])`  
2) apply mask to the df or column `wind['year'].loc[row_mask][0:5]`

Better to apply one criteria at a time and make a new data fram each time:  
`years_sub = wind[wind['year'].isin([1998,1999,2000,2001,2002])]`   
`highwind_sub = years_sub[years_sub['ws'] > 8]`   
This way you can apply conditions to select a subset. Can't do that using 
isin().


----------------

#### Day 10
#####Plotting Windspeed

Solved my [issue](https://github.com/SophMC/notechain/issues/1) on the 
timestamp problem.
Here is [some working](windspeed/notebooks/010_1-windspeed.ipynb) on the way to finding 
it out. 
Tips to remember:   

Double brackets to ref several columns at once:
`print wind[['year','month','day']][0:5]`

`index_col=False` stops pandas using the first column as the index:    
`wind = pd.read_csv(datafile, sep=" ", names=column_names, index_col=False )` 

Having a quick squint at discrete values
`for x in range(0,4): print wind[column_names[x]].unique()`

This didn't work. Anything above 12 in the hour column only recognised the 
second digit, i.e. 2 in 12, 8 in 18.   
`p = pd.to_datetime(year + month + day + hour, yearfirst=True, utc=True, 
format='%Y%m%d%H') ; print p` 

`0   1984-03-10 06:00:00`  
`1   1984-03-11 02:00:00`  
`2   1984-03-11 08:00:00`  
`3   1984-03-20 06:00:00`  
`4   1984-03-21 02:00:00`  
`dtype: datetime64[ns]`  


-----------------

#### Day 9

Opened an [issue](https://github.com/SophMC/notechain/issues/1) on the 
timestamp problem.

----------------


#### Day 8
#####Web App Building

Exercise 52 from [Learning Python the Hard 
Way](http://learnpythonthehardway.org/book/ex52.html). I think I will be 
working on this a few days more before uploading something that you can test 
out. 

#####Plotting windspeed 

My [first attempt](windspeed/notebooks/008-windspeed.ipynb) to read in [windspeed 
data](windspeed/61401BirMoghrein_allwinds.txt) with the format:   
`year, month, day, time, ws`         
I wanted to combine the first four columns into a new timestamp column but this 
has proved difficult. I tried to use read_csv but as the time data were in the 
format 600, 1200, 1800 it wasn't recognised when reading in.   
Next, I created the timestamp after reading in the data but there were problems 
with the input requiring a string and I can't seem to change the dataFrame 
objects to strings to allow it to do this. 

-----------------


#### Day 7
#####Web App Building
Exercise 52 from [Learning Python the Hard 
Way](http://learnpythonthehardway.org/book/ex52.html)

Nothing to show yet as only have the first room working. Need to work out how 
to take the input from the form to lead onto the next room.

$ is used to specify python expressions in html, using web.py
$elif cannot be used. Replace with $else and $if.
You must place a `__init__.py` inside a directory if you wish to use 
`from bin.app import app` to run app_tests.py nosetests on app.py which is 
inside /bin

-----------------

#### Day 6
#####Web App Building
[Exercise 51](firstform) from [Learning Python the Hard 
Way](http://learnpythonthehardway.org/book/ex51.html)

Instructions:  
* Download /notechain/firstform recursively.
* Inside /firstform entering: `python
bin/app.py` should return `http://0.0.0.0:8080/` to the terminal.
* Copy `http://localhost:8080/hello` into your address bar.

-----------------

#### Day 5 
#####Pandas Data Analysis
The following actions are found 
[here](LendingClub/004-LendingClub.ipynb):  

* Removed % signs and "months" and converted the rest into a number.  
* Removed null values with `df.dropna()`. Investigate null values by saving 
them in a new df.  
* Removed data above the 95th percentile by using conditional statements for 
  each column. There must be a cleaner way to do it than this:

`no_outliers = nonan[(nonan[columns[0]] < p[0]) & (nonan[columns[1]] < p[1]) &
(nonan[columns[2]] < p[2]) & (nonan[columns[3]] < p[3]) & (nonan[columns[4]] < 
p[4]) & (nonan[columns[5]] < p[5])]` 
  
* Saved the new dataframe with `to_csv()`. 
* Eyeballed the difference before/after cleaning with a subset of columns in 
`scatter_matrix`

IMPORTANT: `df.count()` only returns non-nans.

---------------

#### Day 4 

#####Git:  
If you remove from local directory you must do this before the changes will be 
made on the remote repository:   
`git rm filename`
`git commit -m "message"`
`git push`

#####Building Web Apps: 
I made [this](http://learnpythonthehardway.org/book/ex50.html) work, only after 
working out (google useless!) where to put a line continuation in 
index.html  
`$if greeting:
    I just wanted to say <em style="color: green; font-size: 
2em;">$greeting</em>.`

Did not fit in one line in my editor. When I shortened it to one line it 
worked. An \ was needed between the message and the html emphasized text.

`$if greeting:
    I just wanted to say \    
<em style="color: green; font-size: 2em;">$greeting</em>.`

##### More Data Analysis in Pandas: 
Started [plotting the data](LendingClub/004-LendingClub.ipynb) with  
`df.plot(kind = 'box'), df.hist() and scatter_matrix(df)`

To suppress the printing of the object before a panel of plots
`_ = df.hist()` etc.


--------------

#### Day 3  
%timeit : time how long a command takes to run.  
More pandas practise [here](LendingClub/003-LendingClub.ipynb).   
`df.dropna(), df.isnull(), df.any(), df.sum()`

--------------


#### Day 2                                                                       
More pandas practise [here](LendingClub/002-LendingClub.ipynb). 
Re-discovered the 
usefulness of cheatsheats. Now have a number of functions for exploring the 
data.    
`df.head(), df.unique(), df.describe(), df.iloc(), df.count(), 
df.isin(), np.where()`

--------------

#### Day 1                                                                
I learned some [git commands](001-git-basics.md) and [played around 
with some data](pandas-notebooks-csv/001-LendingClub.ipynb) in ipython using 
DataFrames (df) in pandas library. 
`df.columns(), df.index(), df.dtypes()`

-------------

