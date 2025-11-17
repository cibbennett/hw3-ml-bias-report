## Interpreting Model Parameters
### Polynomial SBP Parameter (curvature term): c1: -0.0020222943722938425

### Polynomial DBP Parameters (curvature term): d1: -0.005561255411254962

##### The fact that both c1 and d1 are negative, means that the parabola opens downward. In order to determine units of the parameter, I tried to figure it out from the output which is in mmHg. 
If the equation is x1 * (a**2) + (x2 * a) + x3, 

mmmHg = x1 * (years**2) + (x2 * years) + x3

x1 = mmHg / (years**2)

x2 = mmHg / years

x3 = mmHg

### Sigmoidal SBP Parameters:
### Smax: 145.25974335449789
##### This means that the max SBP with age is 145 mmHg (which is likely not true, as blood pressures can go up higher)
### k: 0.019839335660418216
### a0: -53.8108700301842
##### The a0 does not make sense, because it is saying that the age at which SBP reaches half-maximum is -53, which is not biologically possible. This is because we are only seeing the top half of the S-curve. This means that this may not be the best physiological model.

### Gaussian DBP Parameters:
### Dmax: 78.50436221654194

##### This refers to the maximum DBP around middle age, which is 78 mmHg.
### a_peak: 52.27779418080324

##### Age at peak DBP is predicted to be 52, which may be correct as afterwards it begins to fall. 
### width: 81.14056751771523

##### The standard deviation of the Gaussian curve is 81, meaning the spread of the data is 81 years, which makes sense in the setting of normal lifespan.


## Discussion and Analysis: Answer the following
### i. Which model captures age trends in SBP and DBP better?

Based on the MSE and R-squared of the different models, for SBP the Sigmoidal model was the best fit while for DBP the Gaussian model was the best fit. They both had the lowest MSE (error or difference between the model's predictions and the actual data) and the highest R-squared (which tells you how much variation in BP can be explained by the model). The difference between MSE and R-squared was highest for DBP (the Gaussian model was much better than the polynomial). BUT, when determining whether the model is physiologically plausible, the polynomial model for SBP makes more physiological sense. Although the Sigmoidal model has a small statistical edge (in terms of MSE and R2), the polynomial model makes more sense.

### ii. How do model parameters reflect physiological blood pressure changes with age?

The models clearly show that as we age, SBP steadily rises as our vessels become more stiff, and DBP initially increases steadily until a certain point around middle age (40-50 years, the Gaussian model predicted a_peak to be 52 years with a value of Dmax = 78 mmHg) before then decreasing with older age. Smax is the plateau of the SBP, which the sigmoidal model predicted at 145 mmHg. The sigmoidal parameter k represents how fast (the steepness of the curve) the SBP reaches its max value.

### iii. Discuss limitations in capturing demographic nuances.

These models did not take all demographic measures into account. The paper where the data came from discussed some variations in blood pressure based on sex and race/ethnicity, however the models above did not take any of these factors into account. They only utilized age demographics. Demographic data is also only as good as what the participants provide, or in the case of chart-review what was documented.



### Analysis:
##### i. Discuss classifier performance changes with different male/female data ratios.
Accuracy of the model as a whole went down for the 80/20 datasets. The 50/50 split showed an accuracy of 58%, with F1 scores for both males and females of 0.58. The balance between precision and recall was fair for both sexes. Once we changed the ratios to be 80/20 for female- or male-predominant datasets, the accuracy decreased to 50%. The recall for the less-predominant sex was always 0, precision higher (given whenever the mdoel guessed, it was because the data was very obvious), but the f1 score for the less-predominant sex was 0 (taking into account both the model's precision and recall).

##### ii. Identify and examine potential biases introduced by varying prevalences.
The female-predominant set showed an F1 score of 0.0 for males, while the male-predominant set showed an F1 score of 0.0 for females. Models are not inherently biased, they try to minimize error and be as accurate as possible. This means that for a dataset that is biased, the less-predominant class/group is a negative predictor and that the cost of being "wrong" about that group is low.

### Discussion
##### i. Reflect on the importance of balanced datasets in healthcare.
Unfortunately, significant biases can come from unbalanced datasets. And real-word data is often unbalanced and skewed, with compiled human biases on top. Whether it is unbalanced in sex, or other factors, it is always important to think about the end-goal of the model when developing and training. The female-predominant set showed an F1 score of 0.0 for males, while the male-predominant set showed an F1 score of 0.0 for females. The mdoel is only as good as the data you feed it. If coming up with synthetic data, this needs to be taken into account whend developing your training data.

##### ii. Discuss implications and challenges with real-world unbalanced datasets (by changing M and F).
By training a model on unbalanced datasets, unfortunately we are creating systematically biased models that will inherently widen the gap in equity for our patients. We cannot overlook these unbalances, but should confront them and work to mitigate bias in model development. As I was researching this topic, I found a video from the Harvard Medical School Center for Bioethics entitled "Data Science Challenges in the Hospital of Today: Ethics, Culture & Governance" (https://www.youtube.com/watch?v=T2vlzRBUFII). One of the presenters showed two questions that data analysts could consider when determining if there is bias in a dataset:
1. Were the various input data collected, measured, or processed differently between groups? (For example, only some groups provided relevant data? Or were some groups treated differently during data collection?)
2. Will the people (who are impacted) likely disagree about whether the impacts were a net positive or net negative? (The same impacts could be good for one groups but bad for another, so we should consider impacted individuals' interests.)
I think these two questions encapsulate the goal of determining risk of bias even prior to model training. And then they can begin to see if they can be corrected for.

##### iii. Suggest and explore strategies to address these challenges in practice, based on the example provided in the class.
When developing real-world models that will be utilized in a healthcare setting, I think it is very important to utilize data that is most representative of your population as your training and testing data. The idea is to try and simulate what the model will see in the real world. Unfortunately, a lot of datasets have inherent bias, so when attempting to clean and prepare data, it should be the developer's responsibility to brainstorm and examine the different ways that the model could develop bias and to mitigate this by including synthetic data. I think synthetic data is the best way to emulate fairness in an unfair world. This is, of course, not the only way, as discrimination and underrepresentation can occur at every step/level of research, healthcare, data accurement, model training, etc. 

Another important factor is ensuring that the healthcare providers that may be utilizing models know what is the intended use of the model. Also, thinking about accessibility to the model so that all populations can benefit (not just the upper class and/or majority).