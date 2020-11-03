# Grit Study EDA

> 👋 Hello, I'm Nico an Economist turned Data Scientist currently based in Miami. Feel free to contact me if you find yourself enjoying this project. Welcome.

# ☎️ Contact information

🐦 Twitter: [https://twitter.com/nicoivazquez](https://twitter.com/nicoivazquez)

🔗 LinkedIn: [https://www.linkedin.com/in/nicoletovazquez/](https://www.linkedin.com/in/nicoletovazquez/)

---

# **👩🏻‍💻** What is Grit exactly?

## From Wikipedia:

In psychology, grit is a positive, non-cognitive trait based on an individual's perseverance of effort combined with the passion for a particular long-term goal or end state (a powerful motivation to achieve an objective). This perseverance of effort promotes the overcoming of obstacles or challenges that lie on the path to accomplishment and serves as a driving force in achievement realization. 

Grit was defined as "perseverance and passion for long-term goals" by psychologist Angela Duckworth and colleagues, who extensively studied grit as a personality trait. They observed that individuals high in grit were able to maintain their determination and motivation over long periods despite experiences with failure and adversity. They concluded that grit is a better predictor of success than intellectual talent (IQ), based on their evaluation of educational attainment by adults, GPA among Ivy League undergraduates, dropout rate of cadets at West Point US Military Academy, and ranking in the National Spelling Bee.

[Ted Talk Angela Lee Duckworth: Grit: The power of passion and perseverance](https://www.ted.com/talks/angela_lee_duckworth_grit_the_power_of_passion_and_perseverance?language=en)

---

# 🛠 The Scales

## 💻 The data set included 2 tests called scales and a set of biographical questions.

- Data set from [openpsychometrics.org](http://openpsychometrics.org) and posted on Kaggle here: [https://www.kaggle.com/lucasgreenwell/duckworth-grit-scale-responses](https://www.kaggle.com/lucasgreenwell/duckworth-grit-scale-responses)
- This data was collected through an on-line personality test in 2014.
- This data set has around 4270 observations in it with 98 columns and it is a mix between categorical and numerical values.

The first personality test was big five scales from the international personality item pool.  I learned from the official IPIP scale website that the five types tested are 

1. Extroversion Personality - is the personality trait of seeking fulfillment from sources outside the self or in community. High scorers tend to be very social while low scorers prefer to work on their projects alone.
2. Neuroticism Personality - is the personality trait of being emotional.
3. Agreeable Personality - reflects much individuals adjust their behavior to suit others. High scorers are typically polite and like people. Low scorers tend to 'tell it like it is'.
4. Conscientious Personality - is the personality trait of being honest and hardworking. High scorers
tend to follow rules and prefer clean homes. Low scorers may be messy and cheat others
5. Open Personality - is the personality trait of seeking new experience and intellectual
pursuits. High scores may daydream a lot. Low scorers may be very down to earth.

The big five scale questions actually alternate in scoring. So I wrote a small function to sort the questions into the right score category and added the totals for each trait. Below are the histograms for each trait. Openness and Agreeableness look left skewed with a lot more people getting the max score. While Extroversion, Conscientiousness, and Neuroticism totals result in fairly bell shaped graphs.

![images/Untitled.png](images/Untitled.png)

The following items were rated on a five point scale where 1=Disagree,2= Moderately Disagree 3=Neutral,4=Moderately Agree , 5=Agree. All were presented on one page. Example questions include, 

1. I am the life of the party.
2. I am relaxed most of the time.
3. I feel little concern for others.
4. I am full of ideas.

Next came the Grit Scale test. There was 12 questions that were rated on a five point scale where 1=Very much like me, 2=Mostly like me, 3=Somewhat like me, 4=Not much like me, 5=Not like me at all, Example questions include,

1. I have overcome setbacks to conquer an important challenge.
2. New ideas and projects sometimes distract me from previous ones.
3. My interests change from year to year.
4. Setbacks don't discourage me.

Finally the online survey included questions about themselves such as: age, gender, voted, married, family size, religion, orientation, race, hand, English native, gender, urban, education.

---

## 🚧 Importing and Cleanup

1. The data came in a CSV with accompanying codebook for how the test where graded.
2. I noticed some rows were missing the country column so I calculated the percent of the entire data set that was missing values and it was only 44/4270, or 1.041% so dropped those. This left me with 4226 rows to work with.

    ![images/Untitled%201.png](images/Untitled%201.png)

3.  As mentioned above the big five scale questions actually alternate in scoring. So I wrote a small function to sort the questions into the right score category and added the totals for each trait. 

---

## 🗣 Initial Questions and Exploration

### Questions

### Did gritter people spend more time taking the test?

### Are Left handed people gritter than right handed people?

### Do married people have higher grit?

### Can we predict grit from personality test?

### Exploration

1. First I created a five totals DataFrame with the scale totals of all the different traits so I can find correlations between traits of the IPIP test. Findings were not what I was expecting. No correlation between any of the traits. The test makers did a good job of making sure that each trait was significantly different from each other to make it so that none of the traits are correlated.

![images/Untitled%202.png](images/Untitled%202.png)

2. I did the same for the Grit Scale questions and found that only a pair of questions were correlated over 0.5 and that was question 7 and 8:

        7. I often set a goal but later choose to pursue a different one.

        8. I have difficulty maintaining my focus on projects that take more than a few months to complete.

3. There was two times more females in the study than males and less than 1% selected other.

4. 40% of the participants were under 20, and 74% were under 30. I'll come back to why this is important to note at the end. 

---

# 📜 Hypothesis tests

### Are Left handed people gritter than right handed people?

The first test I wanted to answer was does being lefty effect grit?

Hypothesis test set up:

- I wanted my significance level to be at a = 0.05.
- My null hypothesis is that there is no difference in the average grit score of lefty and right-handed people. <a href="https://www.codecogs.com/eqnedit.php?latex=\inline&space;\dpi{120}&space;\mu_\text{lefty}&space;=&space;\mu_\text{righty}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\inline&space;\dpi{120}&space;\mu_\text{lefty}&space;=&space;\mu_\text{righty}" title="\mu_\text{lefty} = \mu_\text{righty}" /></a>
- My alt hypothesis is that lefty people have more grit <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;\mu_\text{lefty}&space;>&space;\mu_\text{righty}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;\mu_\text{lefty}&space;>&space;\mu_\text{righty}" title="\mu_\text{lefty} > \mu_\text{righty}" /></a>
- In order to do hypothesis testing our distribution must be normally distributed. I checked that the grit scores are normally distributed using the D'Agustino t-test and we got that grit scales scores were not normal.

## Stop 🛑

## Bootstrap

- In order to Bootstrap, I first need to divide the data between left and right handed people. Then I can bootstrap the two groups.
- Bootstrapped the samples 5,000 times.
- Then I could continue since the bootstrap created a normal distribution from the means of each resample.
The hypothesis test is now:
    - Our null hypothesis is that <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;\mu_\text{lefty}&space;-&space;\mu_\text{righty}&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;\mu_\text{lefty}&space;-&space;\mu_\text{righty}&space;=&space;0" title="\mu_\text{lefty} - \mu_\text{righty} = 0" /></a>
    - Our alt hypothesis is that <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;\mu_\text{lefty}&space;-&space;\mu_\text{righty}&space;\not=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;\mu_\text{lefty}&space;-&space;\mu_\text{righty}&space;\not=&space;0" title="\mu_\text{lefty} - \mu_\text{righty} \not= 0" /></a>
- Now I subtracted the resample means. I then plotted those recorded differences in means on the below graph with the 95th percentile confidence interval.
- In the end, we can't really say that there is a difference in means because zero is in our 95th percentile confidence interval. We fail to reject the null hypothesis that there is a difference in grit between the two groups.

Simply put we can't confidently say there is a difference in means.

![images/Untitled%203.png](images/Untitled%203.png)

### Do married people have higher grit?

- Testing to see if married people have more grit?
- The hypothesis test is now:
    - Our null hypothesis is that <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;\mu_\text{non-married}&space;-&space;\mu_\text{married}&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;\mu_\text{non-married}&space;-&space;\mu_\text{married}&space;=&space;0" title="\mu_\text{non-married} - \mu_\text{married} = 0" /></a>
    - Our alt hypothesis is that <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;\mu_\text{married}&space;-&space;\mu_\text{non-married}&space;\not=&space;0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;\mu_\text{married}&space;-&space;\mu_\text{non-married}&space;\not=&space;0" title="\mu_\text{married} - \mu_\text{non-married} \not= 0" /></a>
- First to divide the data between non-married and married people, resample, then subtracted the resample means. I then plotted those recorded differences in means on the below graph with the 95th percentile confidence interval.
- In the end, we can't really say that there is a difference in means because zero is in our 95th percentile confidence interval. We fail to reject the null hypothesis that there is a difference in grit between the two groups.

Simply put we can't confidently say there is a difference in means.

![images/Untitled%204.png](images/Untitled%204.png)

---

# 📚 Inferential Regression

## Using OLS to predict grit scores using personality traits.
<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;y&space;=&space;\beta_0&space;&plus;&space;\beta_1&space;f_1&space;&plus;&space;\beta_2&space;f_2&space;&plus;&space;\cdots&space;&plus;&space;\beta_k&space;f_k&space;&plus;&space;\text{noise}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;y&space;=&space;\beta_0&space;&plus;&space;\beta_1&space;f_1&space;&plus;&space;\beta_2&space;f_2&space;&plus;&space;\cdots&space;&plus;&space;\beta_k&space;f_k&space;&plus;&space;\text{noise}" title="y = \beta_0 + \beta_1 f_1 + \beta_2 f_2 + \cdots + \beta_k f_k + \text{noise}" /></a>

I wanted to predict grit scores using personality traits since personality tests are a dime a dozen while grit tests we have this one and its not as popular as other personality tests. In order to do this I used linear regression with 5 features, the big five traits.

![images/Untitled%205.png](images/Untitled%205.png)

Results: Using personality traits as features to predict grit scores.

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;grit&space;=&space;\beta_0&space;&plus;&space;\beta_1&space;O_1&space;&plus;&space;\beta_2&space;E_2&space;&plus;&space;\beta_3&space;N_3&space;&plus;&space;\beta_4&space;A_4&space;&plus;&space;\beta_5&space;C_5&space;&plus;&space;\text{noise}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;grit&space;=&space;\beta_0&space;&plus;&space;\beta_1&space;O_1&space;&plus;&space;\beta_2&space;E_2&space;&plus;&space;\beta_3&space;N_3&space;&plus;&space;\beta_4&space;A_4&space;&plus;&space;\beta_5&space;C_5&space;&plus;&space;\text{noise}" title="grit = \beta_0 + \beta_1 O_1 + \beta_2 E_2 + \beta_3 N_3 + \beta_4 A_4 + \beta_5 C_5 + \text{noise}" /></a>

![images/Untitled%206.png](images/Untitled%206.png)



I was not happy with the results from this model, with an <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;R^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;R^2" title="R^2" /></a>:0.076 this means that only 7.6% of the variance is explained by this model. This does not give me confidence in the predictions I can make from this model. 

To test if the residuals are normally distributed, the common practice is to use a qq-plot (for quantile-quantile-plot). The QQ plot plots the quantile of the normal distribution against that of the residuals and checks for the alignment of the quantiles. This tests to see if the model is linear and if there are any outliers. 

This is what QQ plot looked before with outliers:

![images/Untitled%207.png](images/Untitled%207.png)

What the QQ looks like after more data clean up:

![images/Untitled%208.png](images/Untitled%208.png)

Testing for homoscedasticity - Plot the residuals of the models against the predicted values. Look at the noise, no signal. variance stays constant thought.

![images/Untitled%209.png](images/Untitled%209.png)

Multicollinearity: These tests are to see if the independent variables are not highly correlated with each other using the VIF - The Variance Inflation Factor. I was looking for numbers under 10. 

![images/Untitled%2010.png](images/Untitled%2010.png)


### On to predicting grit from test time, age and education.

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;grit&space;=&space;\beta_0&space;&plus;&space;\beta_1&space;age_1&space;&plus;&space;\beta_2&space;time_2&space;&plus;&space;\beta_3&space;lhs_3&space;&plus;&space;\beta_4&space;hs_4&space;&plus;&space;\beta_5&space;bs_5&space;&plus;&space;\beta_6&space;gs_6&space;&plus;&space;\text{noise}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;grit&space;=&space;\beta_0&space;&plus;&space;\beta_1&space;age_1&space;&plus;&space;\beta_2&space;time_2&space;&plus;&space;\beta_3&space;lhs_3&space;&plus;&space;\beta_4&space;hs_4&space;&plus;&space;\beta_5&space;bs_5&space;&plus;&space;\beta_6&space;gs_6&space;&plus;&space;\text{noise}" title="grit = \beta_0 + \beta_1 age_1 + \beta_2 time_2 + \beta_3 lhs_3 + \beta_4 hs_4 + \beta_5 bs_5 + \beta_6 gs_6 + \text{noise}" /></a>

- To use test time and education, I had to clean up the data some more. I had some test times that were too long and probability meant that the person was either unfocused or got up to do something between,  I dropped those. Then I created dummy variables for education in order to be able to have different coefficients for each one.

Results: 

![images/Untitled%2011.png](images/Untitled%2011.png)

- The interesting part of these results is the surveyelapse time is the only feature with any significance. By multiplying the coefficient of surveyelapse with seconds you get the increase in grit score per second. .0063 times 60 seconds gives us about a 0.4 increase in grit score per minute taking the grit scale test.
- <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;R^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;R^2" title="R^2" /></a>:0.014 this means that only 1.4% of the variance is explained by this model
- I attribute this to people who tend to be more intentional with their time tend to take time reading the instructions of the test and are more introspective with their responses could lead to them scoring higher.
- Testing for homoscedasticity - Plot the residuals of the models against the predicted values. Look at the noise, no signal. Variance stays constant thought.

![images/Untitled%2012.png](images/Untitled%2012.png)

Multicollinearity: These tests are to see if the independent variables are not highly correlated with each other using the VIF - The Variance Inflation Factor. I was looking for numbers under 10.  

![images/Untitled%2013.png](images/Untitled%2013.png)

Again, with an <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;R^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;R^2" title="R^2" /></a>:0.014 this means that only 1.4% of the variance is explained by this model. This does not give me confidence in the predictions I can make from this model. 

---

# 👨🏻‍🏫 Bayesian Inference

- I started with the same questions as before do lefties get higher grit scores than righties?
- First I got to get the beta distribution parameters in order to do that I must separate the two groups from my sample. Once I did that I had 421 lefties and 3552 righties.
- I didn't like this sample difference for this test so I once again decided to bootstrap but this time I decided to make this a fair fight and made each sample for the two groups the same at 5000 points because the more samples we have (i.e. the larger (𝛼+𝛽)), then the smaller the variance of our beta distribution will be. I also bootstrapped the grit scores of both groups together to have a base to compare too. I resampled each group 1000 times.
- Once I had the 3 groups all ready to go I got the means of each individual to resample, leaving me with 1000 sample means for all 3 groups. In order to get the Beta Distribution, we need a success rate for lefties and righties having a higher sample mean than the base group.

The mean of the resample means are:

- 30.8596 mean total group
- 30.9281 mean lefty group
- 30.8997 mean righty group
- lefty parameters (a = 770, b = 230, mean = 0.77, Success = 770, total = 1000)
- righty parameters (a = 663, b= 337, mean = 0.663, Success = 663, total =1000
- Now comes time to graph the PDF of the distribution created from the parameters. On the y-axis, we have probability density, and on the x-axis of distribution we have probabilities Success rates). So we have relative probability of the Success rates of lefties and righties that beat out the average mean.
- Put all this together, the beta distribution models the probability of the success rate of having a higher grit score sample mean (which we are trying to figure out from our data).
- Back to the question at 'hand': What's the probability that lefties score better than righties?

    ![images/Untitled%2014.png](images/Untitled%2014.png)

- Let's figure out how much of lefties Beta distribution is to the right of righties.
- Let's run a quick Monte Carlo simulation. To do this I draw a large number of random samples from each distribution created above. I can then count the number of times lefty samples are greater than righties. I can do this 10,000 times within seconds with a computer.

    ![images/Untitled%2015.png](images/Untitled%2015.png)

---

# 🔚 Conclusion

### Key findings

- Being lefty might effect grit score. A more representative sample of the population is necessary.
- Being married probability doesn't mean you are any grittier.
- When trying to build a predictive model <a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{150}&space;R^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{150}&space;R^2" title="R^2" /></a> was very low and there was no clear signal at all. We might need more data in order to predict anything useful.
- People have complicated histories. This leads to personalities of all types no matter their backgrounds, more behavioral psychology data is needed.

### Caveat

It is important to note that all these findings come with a certain caveat, which is that these findings are not representative of people from all walks of life. Mainly because most of the answers were from America and the majority from 20 something-year-old college students. So it is important to make note of that. This also happens to be a self assessed personality tests. Which means that you yourself might say you are "Quick to give up" while a friend might label you "Hard working". 

### Next steps

Outside research on lefties earning less than righties if they don't go to college vs the lefties who go to college actually earn more.
[The evidence that lefties earn more.](https://slate.com/business/2006/08/the-evidence-that-lefties-earn-more.html)

If I was going to take this project further I would work on the model model I made using Linear Regression and combine a large 1 million plus row IPIP data set and try to predict grit scores from personality.  
