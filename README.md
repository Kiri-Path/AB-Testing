# A/B Testing

**Business Perspective Summary of A/B Testing:**
A/B testing, in a business context, is a method used to compare two versions of a product, webpage, or marketing strategy to determine which one performs better in achieving a specific goal, such as increased sales or user engagement. By randomly assigning users to two groups – A (the control group) and B (the experimental group) – businesses can systematically test changes in design, content, or features. This data-driven approach helps companies make informed decisions, reduce guesswork, and optimize their products or services to enhance customer satisfaction and drive growth.

**Statistical Perspective Summary of A/B Testing:**
From a statistical standpoint, A/B testing involves hypothesis testing to evaluate the effectiveness of changes. The process begins by formulating a null hypothesis (H0) that assumes no difference between the two versions. Data collected from both groups are then analyzed to calculate key metrics and test statistics. Statistical significance is determined using p-values and confidence intervals, which help to assess whether observed differences are due to chance or actual effects of the changes implemented. Ensuring a sufficient sample size and controlling for variables are critical to achieving reliable and valid results, ultimately guiding data-driven decision-making.


A/B Testing - Minimum Sample size

A/B testing is the process of creating 2 variations 1 being the control and 1 being the new variation. We then see which one delivers a goal conversion. For example, if your website has always had a red background on the order page you might find that if you change it to green you will get more order conversions. However we need to test this so that we can be statistically sure the result is true and not just luck.




Before going into the code of A/B testing we first need to understand fundamental statistic - Type 1 vs Type 2 Errors.




2 possible outcomes of a hypothesis test
Human decision made
Null Hypothesis (H0) is True
Null Hypothesis (H0) is False
Reject H0
Type 1 Error
Probability = ⍺
Correct decision 
Probability = 1-⍺
Accept H0
Correct Decision
Probability = 1-ꞵ
Type 2 Error
Probability = ꞵ


As an example…

H0: You are not pregnant




2 possible outcomes of a hypothesis test
Pregnancy test decision
H0 is True : You are NOT pregnant
H0 is False: You ARE pregnant
Reject H0: You are Pregnant
Type 1 Error
Probability = ⍺
Correct decision 
Probability = 1-⍺
Accept H0: You are not pregnant
Correct Decision
Probability = 1-ꞵ
Type 2 Error
Probability = ꞵ


Confidence interval
It starts here with us deciding how confident/stringent we want to be when running a test. For example we want to be 95% sure in order to reject the null hypothesis. 

Alpha
This is our significance level 
This is the probability of rejecting null hypothesis when it is actually true
A 5% significance level indicates a 5% risk of concluding that a difference exists when there is actually no difference

P-Value
We compare our p-value (the calculated phi value) against out alpha level. If it is less then we can reject the null hypothesis and conclude it is in deed different.


P-value less that alpha: reject null hypothesis as the result is statistically significant and we can be sure there is something besides chance that gave us our observed sample. 
P-value greater than alpha: fail to reject the null hypothesis as result is NOT statically significant. In other words, we can be reasonably sure the observed data can be explained by chance alone. 
So this is why its important to not choose a too high alpha because then you will just end up concluding the result is stastically significant! And vice versa if your alpha is too small then it is hard to prove your results are stasticially signfifcant.
The pvalue is similr to the alpha signicance level in that both are measured between 0 – 1. 
The number alpha is the threshold that we measure the p-value against. It tells us how extreme observed values must be in order to reject the null hypothesis.
The Alpha is associated with confidence intervals. The alpha value gives the probability of a type 1 error. 

Power = 1- Beta
This is the probability that a test will CORRECTLY support the alternative hypothesis. 
Beta is the probability that we would accept the null hypothesis even if the alternative hypothesis is actually true. In other words this is the probability of type 2 error.




BCR - Base Conversion Rate
this is our current conversion rate we are achieving (so what our control conversion is)
MDE - Minimum Detectable Effect
User input to determine lift. Bear in mind this will have a knock on effect to test duration.

POWER - Statistical power of sensitivity
power of sensitivity  = predicted true events / total events
Power of sensitivity = probability (Rejecting H0 | H0 is false)
Power of sensitivity = probability (not making a type 2 error)
Industry Standard = 0.8

Signficance Level (Alpha)
Our risk of making a type 1 error
Industry Standard = 0.05

Standard_norm, Z -Beta , Z - Alpha:
Z-beta and Z-Alpha returns the standard normal  Z-Values for the probabilities. 
Z- Alpha returns 1.96 , Z -Beta returns 

Pooled Prob = average of BCR and BCR*MDE

Sample size for 2 sample test = 2 * average conversion * (average failure) * (Zbeta+Zalpha)**2  / BCR % difference
