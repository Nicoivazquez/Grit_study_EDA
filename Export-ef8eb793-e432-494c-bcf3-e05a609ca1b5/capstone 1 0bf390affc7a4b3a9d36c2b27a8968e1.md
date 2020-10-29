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

## 💻 The data set included 3 tests called scales and a set of biographical questions.

- This data was collected through an on-line personality test in 2014.
- This data set has around 4720 observations in it with 98 columns and it is a mix between categorical and numerical values.

The first personality test was big five scales from the international personality item pool.  I learned from The official IPIP scale website that the five types tested are 

1. Extroversion Personality
2. Neuroticism Personality
3. Agreeable Personality
4. Conscientious Personality
5. Open Personality

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

### Exploration

1. First I created a five totals DataFrame with the scale totals of all the different traits so I can find correlations between traits of the IPIP test. Findings were not what I was expecting. No correlation between any of the traits. The test makers did a good job in making sure that each trait was significantly different from each other to make it so that none of the traits are correlated.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%201.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%201.png)

2. I did the same for the Grit Scale questions and found that only a pair of questions were correlated over .5 and that was question 7 and 8:

7. I often set a goal but later choose to pursue a different one.

8. I have difficulty maintaining my focus on projects that take more than a few months to complete.

3. There was two times more females in the study than males and less than 1% selected other.

4. 40% of the participants were under 20, and 74% were under 30. I'll come back to this at the end. 

5. 

---

# 📜 Hypothesis tests

The first test I wanted to answer was does being lefty effect grit?

Hypothesis test set up:

 I wanted my power to be 95% witch means I needed an effect size of 0.27. Then I looked looked at Grit scale and lefty graph. 

In order to do hypothesis testing our distribution must be normally distributed. I checked that the grit scores are normally distributed using the D'Agustino t-test and we got that grit scales scores were not normal. 

## Stop 🛑

## Bootstrap

- Bootstrapped the sample 5,000 times.
- Then I could continue since the bootstrap created a a normal distribution. # why?
The hypothesis test is now
    - our null hypothesis is that $\mu_\text{lefty} = \mu_\text{righty} = 0 $
    - our alt hypothesis is that $/mu_/text{lefty} > 0
- I then have to divide the data between left and right handed people, then subtracted the resample means. I then plotted those recorded differences in means on the below graph with the 95th percentile confidence interval.
- In the end we can't really say that there is a difference in means, because zero is in our 95th percentile confidence interval. We fail to reject the null hypothesis that there is a difference in grit between the two groups.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%202.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%202.png)

The 95th percentile is from -0.4190254629629622 0.5660666099773265

- Testing to see if married people have more grit?
- The hypothesis test is now
- our null hypothesis is that $\mu_\text{non-married} = \mu_\text{married} = 0$
- our alt hypothesis is that $/mu_/text{married}$ > 0
- I then have to divide the data between non-married and married people, then subtracted the resample means. I then plotted those recorded differences in means on the below graph with the 95th percentile confidence interval.
- In the end we can't really say that there is a difference in means, because zero is in our 95th percentile confidence interval. We fail to reject the null hypothesis that there is a difference in grit between the two groups.

![capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%203.png](capstone%201%200bf390affc7a4b3a9d36c2b27a8968e1/Untitled%203.png)

---

# 📚 Inferential Regression

## OLS

OLS 

---

# Conclusion

### Key findings

- Being lefty or righty doesn't matter
- Being married doesn't matter

### Caveat

It is important to note that all these findings come with a certain caveat, which is that this findings are not representative of people from all walks of life. Mainly because most of the answers where from America, and majority from 20 something year old college students. So it is important to make note of that.

### Next steps

If I was going to take this project further I would use the model I made using inferential Regression and combine a large 1 million plus row IPIP data set and try to predict grit scores from personality.
