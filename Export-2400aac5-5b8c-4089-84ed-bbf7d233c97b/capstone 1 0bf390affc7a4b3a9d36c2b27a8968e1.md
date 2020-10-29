# capstone 1

> I'm a Data Scientist based in Miami.

# ☎️ Contact information

📧 Email address

🐦 Twitter

🔗 LinkedIn

---

# **👩🏻‍💻** What is Grit exactly?

## From Wikipedia:

In psychology, grit is a positive, non-cognitive trait based on an individual's perseverance of effort combined with the passion for a particular long-term goal or end state (a powerful motivation to achieve an objective). This perseverance of effort promotes the overcoming of obstacles or challenges that lie on the path to accomplishment and serves as a driving force in achievement realization. 

Grit was defined as "perseverance and passion for long-term goals" by psychologist Angela Duckworth and colleagues, who extensively studied grit as a personality trait. They observed that individuals high in grit were able to maintain their determination and motivation over long periods despite experiences with failure and adversity. They concluded that grit is a better predictor of success than intellectual talent (IQ), based on their evaluation of educational attainment by adults, GPA among Ivy League undergraduates, dropout rate of cadets at West Point US Military Academy, and ranking in the National Spelling Bee.

---

# 🛠 The Scales

## 💻 The data set included 2 tests called scales and a set of biographical questions.

- This data was collected through an on-line personality test in 2014.
- This data set has around 4720 observations in it with 98 columns and it is a mix between categorical and numerical values.

The first personality test was big five scales from the international personality item pool.  I learned from the official IPIP scale website that the five types tested are 

1. Extroversion Personality - is the personality trait of seeking fulfillment from sources outside the self or in community. High scorers tend to be very social while low scorers prefer to work on their projects alone.
2. Neuroticism Personality - is the personality trait of being emotional.
3. Agreeable Personality - reflects much individuals adjust their behavior to suit others. High scorers are typically polite and like people. Low scorers tend to 'tell it like it is'.
4. Conscientious Personality - is the personality trait of being honest and hardworking. High scorers
tend to follow rules and prefer clean homes. Low scorers may be messy and cheat others
5. Open Personality - is the personality trait of seeking new experience and intellectual
pursuits. High scores may daydream a lot. Low scorers may be very down to earth.

The following items were rated on a five point scale where 1=Disagree, 3=Neutral, 5=Agree (0=missed). All were presented on one page. Example questions include, 

1. I am the life of the party.
2. I am relaxed most of the time.
3. I feel little concern for others.
4. I am full of ideas.

Next came the Grit Scale test. There was 12 questions that were rated on a five point scale where 1=Very much like me, 2=Mostly like me, 3=Somewhat like me, 4=Not much like me, 5=Not like me at all, Example questions include,

1. I have overcome setbacks to conquer an important challenge.
2. New ideas and projects sometimes distract me from previous ones.
3. My interests change from year to year.
4. Setbacks don't discourage me.

Finally the online survey included questions about themselves, age, gender, voted, married, family size, religion, orientation, race, hand, English native, gender, urban, education.

---

## 🚧 Importing and Cleanup

1. The data came in a CSV with accompanying codebook for how the test where graded.
2. I noticed some rows were missing the country column so I calculated the percent of the entire data set that was missing values and it was only 44/4270, or 1.041% so dropped those. This left me with 4226 rows to work with.

    ![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled.png)

---

## 🗣 Initial Questions and Exploration

### Questions

### Did gritter people spend more time taking each test?

### Are Left handed people gritter than right handed people?

### Do married people have higher grit?

### Can we predict grit from personality test?

### Exploration

1. First I created a five totals DataFrame with the scale totals of all the different traits so I can find correlations between traits of the IPIP test. Findings were not what I was expecting. No correlation between any of the traits. The test makers did a good job of making sure that each trait was significantly different from each other to make it so that none of the traits are correlated.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%201.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%201.png)

2. I did the same for the Grit Scale questions and found that only a pair of questions were correlated over 0.5 and that was question 7 and 8:

7. I often set a goal but later choose to pursue a different one.

8. I have difficulty maintaining my focus on projects that take more than a few months to complete.

3. There was two times more females in the study than males and less than 1% selected other.

4. 40% of the participants were under 20, and 74% were under 30. I'll come back to why this is important to note at the end. 

5. 

---

# 📜 Hypothesis tests

### Are Left handed people gritter than right handed people?

The first test I wanted to answer was does being lefty effect grit?

Hypothesis test set up:

- I wanted my significance level to be at a = 0.05.
- My null hypothesis is that there is no difference in the average grit score of lefty and right-handed people. $\mu_\text{lefty} = \mu_\text{righty}$
- My alt hypothesis is that lefty people have more grit $\mu_\text{lefty} > \mu_\text{righty}$
- In order to do hypothesis testing our distribution must be normally distributed. I checked that the grit scores are normally distributed using the D'Agustino t-test and we got that grit scales scores were not normal.

## Stop 🛑

## Bootstrap

- In order to Bootstrap, I first need to divide the data between left and right handed people. Then I can bootstrap the two groups.
- Bootstrapped the samples 5,000 times.
- Then I could continue since the bootstrap created a normal distribution from the means of each resample. # why?
The hypothesis test is now:
    - Our null hypothesis is that $\mu_\text{lefty} = \mu_\text{righty} = 0$
    - Our alt hypothesis is that $/mu_/text{lefty} > 0
- Now I subtracted the resample means. I then plotted those recorded differences in means on the below graph with the 95th percentile confidence interval.
- In the end, we can't really say that there is a difference in means because zero is in our 95th percentile confidence interval. We fail to reject the null hypothesis that there is a difference in grit between the two groups.

Simply put we can't confidently say there is a difference in means.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%202.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%202.png)

### Do married people have higher grit?

- Testing to see if married people have more grit?
- The hypothesis test is now:
    - our null hypothesis is that $\mu_\text{non-married} = \mu_\text{married} = 0$
    - our alt hypothesis is that $/mu_/text{married}$ > 0
- First to divide the data between non-married and married people, resample, then subtracted the resample means. I then plotted those recorded differences in means on the below graph with the 95th percentile confidence interval.
- In the end, we can't really say that there is a difference in means because zero is in our 95th percentile confidence interval. We fail to reject the null hypothesis that there is a difference in grit between the two groups.

Simply put we can't confidently say there is a difference in means.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%203.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%203.png)

---

# 📚 Inferential Regression

## OLS

Using personality traits to predict grit scores

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%204.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%204.png)

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%205.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%205.png)

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%206.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%206.png)

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%207.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%207.png)

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%208.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%208.png)

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%209.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%209.png)

Results

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2010.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2010.png)

To test if the residuals are normally distributed, the common practice is to use a qq-plot (for quantile-quantile-plot). The Q-Q plot plots the quantile of the normal distribution against that of the residuals and checks for the alignment of the quantiles. This tests to see if the model is linear and if there are any outliers. 

what qq plot looked before

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2011.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2011.png)

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2012.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2012.png)

homosecdatisy - variance stays constant - Plot the residuals of the models against the predicted values.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2013.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2013.png)

Multicollinearily: These tests if the independent variables are not highly correlated with each other. using the VIF - the Variance inflation factor. I was looking for numbers under 10. 

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2014.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2014.png)

### On to predicting grit from test time, age and education.

- To use test time and education, I had to clean up the data some more. I had some test times that were to long and probability meant that the person was either unfocused or got up to do something between. I dropped those and then for I did dummy variables in order to be able to have different coefficients for each one.

results: 

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2015.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2015.png)

- with an R-squared:	0.014 this means that only 1.4% of the variance is explained by this model. This does not give me confidence in the predictions I can make from this model.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2016.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%2016.png)

## Inferential linear regression- aka predicting from model

- 5 assumptions needed to do inferential linear regression
    1. Normal
        1. d'agustin and pearson normal test. stats.normaltest(df or arr). look for high p value. low p value fails Ho which is p < a.
    2. Linear - qq plot
    3. outliers
    4. homosecdatisy - variance stays constant - Plot the residuals of the models against the predicted values.
    5. Multicollinearily - the independent variables are not highly correlated with each other
        1. the Variance inflation factor is how you test for this if you need to. VIF
        2. you should remove the biggest VIF and then test again to see if they lower
        below 10.
    6. 
    - Confounding in Regression.
        - Always graph so you can see if you are making a mistake
        - remember that corelation does not imply causation but only assosiation.
        - ex:

---

# Conclusion

### Key findings

- Being lefty or righty doesn't effect grit score
- Being married probability doesn't mean you have more grit
- When trying to build a model
- People have complicated histories. This leads to personalities of all types no matter their backgrounds.

### Caveat

It is important to note that all these findings come with a certain caveat, which is that this findings are not representative of people from all walks of life. Mainly because most of the answers where from America, and majority from 20 something year old college students. So it is important to make note of that.

### Next steps

If I was going to take this project further I would use the model I made using inferential Regression and combine a large 1 million plus row IPIP data set and try to predict grit scores from personality.