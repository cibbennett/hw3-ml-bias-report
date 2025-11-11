# Model-based Bias Removal in Machine Learning
Question Selected: Question 3

This assignment explores model-based bias in machine learning using synthetic blood pressure data.

Part A focuses on modeling real-world, age-dependent blood pressure trends by fitting Polynomial, Sigmoidal, and Gaussian models to data from a medical preprint.

Part B explores how dataset imbalance creates discriminatory models. We generate synthetic blood pressure data for males and females, then train classifiers on balanced and imbalanced datasets (50/50, 80/20) to observe the impact on performance (Accuracy, F1-Score) and fairness. Finally, we implement a model-level mitigation strategy to correct for the bias.

## Summary of Findings & Key Insights:
Balanced data creates fair models: The 50/50 split showed an accuracy of 58%, with balanced F1 scores for both males and females of 0.58. The balance between precision and recall was fair for both sexes.

Imbalanced data destroys performance: When we changed the ratios to 80/20, the accuracy on a balanced test set decreased to 50% (no better than a random guess).

Bias results in a 0.0 F1-Score: The female-predominant set showed an F1 score of 0.0 for males, and the male-predominant set showed an F1 score of 0.0 for females.

How bias works (Recall vs. Precision): The recall for the less-predominant sex was always 0. The precision was higher only because the model would guess the minority class when the data was very obvious, but it missed all other cases.

Models are not inherently biased, they minimize error: A model's goal is to be accurate. In a biased dataset, the minority class becomes a negative predictor because the cost of being wrong about that group is low.

"Garbage in, garbage out": A model is only as good as the data you feed it. This was proven, as real-world data is often unbalanced and skewed, with compiled human biases on top.

## Comparative Model Performance:
## Part A: Age-Based BP Models
   Model Type --- Data --- MSE --- R-Squared
   
   Polynomial --- SBP --- 0.272 --- 0.9948
   
   Sigmoidal --- SBP ---- 0.233 --- 0.9956
   
   Polynomial -- DBP ---- 1.030 --- 0.9152
   
   Gaussian ---- DBP ---- 0.938 --- 0.9228

## Part B: Bias Classification Models
All models evaluated on a balanced test set of 40,000 samples (20k Female, 20k Male).

Training Data ----------- Acc ------ F1 (Fem) -- F1 (Male)

50/50 Balanced ---------- 58.21% --- 0.58 ------ 0.58

80/20 Female ------------ 50.03% --- 0.67 ------ 0.00

20/80 Male -------------- 50.02% --- 0.00 ------ 0.67

20/80 Male+
class_weight='balanced' - 58% ------ 0.58 ------ 0.58


## Relevance to Model-Based Machine Learning:

This assignment demonstrates that "model-based" ML is not just about the final classification algorithm. The "model" applies to the entire pipeline:
1. Modeling the Data: In Part A, we created a mathematical model of the physiological process itself. This is a prerequisite for understanding the features.
2. Modeling the Bias: In Part B, we modeled a biased dataset to understand its effect on a classifier. The imbalanced 80/20 set is a "model" of a biased real-world dataset.
3. Modeling the Algorithm: In Part B.iv, we modified the model's loss function (via class_weight) to account for the deficiencies in the data. This shows how the model itself can be adjusted to be more robust.

By training a model on unbalanced datasets, we risk creating systematically biased models that will inherently widen the gap in equity for our patients. We cannot overlook these unbalances and must work to mitigate bias in model development. Proactive analysis is critical. As noted in research from the Harvard Medical School Center for Bioethics, we should ask questions before training to identify bias risk: "Were the various input data collected, measured, or processed differently between groups?" and
"Will the people (who are impacted) likely disagree about whether the impacts were a net positive or net negative?" When developing real-world models, it is vital to use data that is representative of the target population. Since many datasets have inherent bias, synthetic data may be the best way to emulate fairness in an unfair world and build a balanced, representative training set. Mitigation is not just about data. We must also ensure that healthcare providers utilizing these models know the intended use and that the model is accessible to all populations, not just the upper class and/or majority.

## Suggestions for Future Modeling Improvements:

Improve ROC Curves: The current ROC curves use predict(), which only provides a few points. Future work should use predict_proba() to generate probabilities, which will create a smooth, multi-threshold ROC curve and provide a more accurate Area Under the Curve (AUC) metric.

Explore Other Models: This analysis was limited to Logistic Regression. It would be valuable to test other models (like the RandomForestClassifier I started) to see if they are more or less susceptible to imbalance bias.

Explore Other Mitigation: We only used class_weight (re-weighting). Future work could compare this to data-level mitigation, such as oversampling the minority class (e.g., SMOTE) or undersampling the majority class.

## AI Tool Disclosure:
Disclaimer: Gemini was used as a collaborative coding and debugging partner for this assignment. Gemini's contributions included:

#### Conceptual Understanding: 
Assisted in explaining the assignment's core concepts, such as model fitting, the differences between model types (Polynomial vs. Sigmoidal/Gaussian), and the principles of algorithmic bias.

#### Code Implementation: 
Provided syntax for Python libraries, including scipy.optimize for model fitting, numpy for covariance matrix generation, pandas for data manipulation, and sklearn for the machine learning workflow.

#### Troubleshooting and Debugging: 
Helped to identify and resolve various errors throughout the project, including ValueErrors, SyntaxWarnings, OptimizeWarnings, and AttributeErrors, and assisted with debugging data loading and feature engineering logic (like converting age ranges to numbers).

#### Analysis and Refinement: 
Guided the analysis of model outputs, such as interpreting statistical metrics (MSE, R²) and non-physiological parameters (the a0 value). Also helped analyze the F1-score paradox in the biased models and provided feedback on refining the final written discussion.

### Beyond the AI's contributions, I wrote the initial script, connected all the code pieces, ran all the executions, and provided the errors and outputs for Gemini to analyze. A full transcript of the conversation with Gemini is included in the file Gemini Prompts and Responses.pdf.
