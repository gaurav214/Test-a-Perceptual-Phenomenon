# Test-a-Perceptual-Phenomenon
Statistics project done using Python 3_ Udacity

### Analyzing the Stroop Effect
Perform the analysis in the space below. Remember to follow [the instructions](https://docs.google.com/document/d/1-OkpZLjG_kX9J6LIQ5IltsqMzVWjh36QpnP2RYpVdPU/pub?embedded=True) and review the [project rubric](https://review.udacity.com/#!/rubrics/71/view) before submitting. Once you've completed the analysis and write up, download this file as a PDF or HTML file and submit in the final section of this lesson.

---
(1) What is the independent variable? What is the dependent variable?
---
Independent Variable: Stroop test(Congruent Words and Incongruent Words)
Dependent Variable: Response time of each participant

---
(2) What is an appropriate set of hypotheses for this task? Specify your null and alternative hypotheses, and clearly define any notation used. Justify your choices.
---
The appropriate hypothesis for this task is as follows:
1. Null Hypothesis(H0): There is no significant difference between the response times for Congruent test and Incongruent            test.    i.e. ( μc = μi)
2. Alternate Hypothesis (Ha): There is a significant difference between the response times for Congruent test and       Incongruent   test i.e. (μc != μi)

Where :
   μc = Population means for Congruent Words
   μi = Population means for Incongruent Words

In this case the participants are measured on the same dependent variable(response time) under two different conditions (Congruent Words and Incongruent Words),so to determine whether there is a statistically significant difference between these means, a paired t-test will be an appropriate statistical test to compare both means. 

---
(3) Report some descriptive statistics regarding this dataset. Include at least one measure of central tendency and at least one measure of variability. The name of the data file is 'stroopdata.csv'.
---
```
import pandas as pd

sd = pd.read_csv('stroopdata.csv')

#Calculating descriptive statistics for this dataset
print("Mean of each condition:")
print ("Congruent: {}    Incongruent: {}". format(sd['Congruent'].mean(),sd['Incongruent'].mean()))

print("\nMedian of each condition:")
print ("Congruent: {}    Incongruent: {}".format(sd['Congruent'].median(),sd['Incongruent'].median()))

print("\nStandard Deviation for each condition:")
print ("Congruent: {}    Incongruent: {}".format(sd['Congruent'].std(),sd['Incongruent'].std()))
```
#### Mean and median have larger difference in case Incongruent words, probably presence of outliers have strecthed the mean.

---
(4) Provide one or two visualizations that show the distribution of the sample data. Write one or two sentences noting what you observe about the plot or plots.
---

```
import matplotlib.pyplot as plt

plt.hist(sd['Congruent'], bins = 'auto')
plt.title("Frequency of Congruent")
plt.xlabel("Response time for Congruent")
plt.ylabel('Frequency')
plt.axvline(sd['Congruent'].mean() , color = 'g', linestyle = 'dashed', linewidth = 2)
plt.axvline(sd['Congruent'].median() , color = 'y', linestyle = 'dashed', linewidth = 2)
plt.show()
```
```
plt.hist(sd['Incongruent'], bins = 'auto')
plt.title("Frequency of Congruent")
plt.xlabel("Response time for Incongruent")
plt.ylabel('Frequency')
plt.axvline(sd['Incongruent'].mean() , color = 'g', linestyle = 'dashed', linewidth = 2)
plt.axvline(sd['Incongruent'].median() , color = 'y', linestyle = 'dashed', linewidth = 2)
plt.show()
```
 The Yellow dashed line represent the median of dataset and green dashed line represents mean for each dataset.
It is clear from the plot that their are outliers in both datasets. There are more outliers present in case of Incongruent dataset.
The Higher mean and median 

---
(5)  Now, perform the statistical test and report your results. What is your confidence level or Type I error associated with your test? What is your conclusion regarding the hypotheses you set up? Did the results match up with your expectations? **Hint:**  Think about what is being measured on each individual, and what statistic best captures how an individual reacts in each environment.
--
### Perform the statistical test here
```
stats.ttest_rel(sd['Congruent'], sd['Incongruent'])
```
--
Since the original hypothesis does not state that the difference in population means should be positive or negative, we performed two-tailed test with alpha level of .025 and degree of freedom 23 which results in t-critical value of ±2.069.

Above result shows that the t-statistic is -8.0207, that means we reject the null hypothese(μc = μi) and accept the alternative
hypothesis that the population means for the Congruent Condition and Incongruent condition are not equal(μc != μi)

---
(6) Optional: What do you think is responsible for the effects observed? Can you think of an alternative or similar task that would result in a similar effect? Some research about the problem will be helpful for thinking about these two questions!
---

Parallel distributed processing could be responsible for the observed effects.

This theory suggests that as the brain analyzes information, different and specific pathways are developed for different tasks. Some pathways, such as reading, are stronger than others, therefore, it is the strength of the pathway and not the speed of the pathway that is important. In addition, automaticity is a function of the strength of each pathway, hence, when two pathways are activated simultaneously in the Stroop effect, interference occurs between the stronger (word reading) path and the weaker (color naming) path, more specifically when the pathway that leads to the response is the weaker pathway.

---
Resources referenced for this project:
---
    1.^https://en.wikipedia.org/wiki/Null_hypothesis
    2.^https://statistics.laerd.com/statistical-guides/dependent-t-test-statistical-guide.php
    3.^http://psycnet.apa.org/doiLanding?doi=10.1037%2F0033-295X.97.3.332
    4.^https://s3.amazonaws.com/udacity-hosted-downloads/t-table.jpg
