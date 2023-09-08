# Building an Effective Password Strength Classifier

## Introduction
Machine learning models are integral to bolstering cybersecurity. With the soaring need for robust security measures, models that proficiently classify password strengths are crucial. However, aligning a password strength classifier with real-world standards presents challenges, particularly ensuring that model metrics genuinely reflect its real-world performance.

## Dataset Overview and Insights
The [dataset](https://www.kaggle.com/datasets/bhavikbb/password-strength-classifier-dataset) comprises passwords from the 000webhost leak, categorized for strength using the PARS tool from Georgia Tech University. This tool integrates commercial password strength meters from Twitter, Microsoft, and Battle. Their unique approach, based on machine learning, only included passwords consistently flagged as weak, medium, or strong across all meters. Initially starting with 3 million passwords, the consistent rating criterion narrowed the dataset to 0.7 million.

To visually grasp the distribution and variability of the dataset, we visualized the boxplot with kde and violin plot which are as follows:

![image](https://github.com/DrishtiShrrrma/codebert-base-password-strength-classifier/assets/129742046/7184e96a-81a7-4071-aa16-2e21a0eed865)

Figure 1: i) Histogram with kde ii) Violin Plot for Password length by Strength

![image](https://github.com/DrishtiShrrrma/codebert-base-password-strength-classifier/assets/129742046/10c8beb9-0e87-4824-9823-97675f7c2e21)

Figure 2: Table illustrating maximum, minimum and average password length corresponding to each class


Moreover, the class counts were as follows:
1  ---> 496801
0  ---> 89701
2  ---> 83120

Clearly, a class-imbalance scenario exists. We will be dealing with this with the help of a custom trainer which will be responsible for computing the loss using the normalized weights we will assign and ensuring that the model’s training aligns with our objectives.

## The Model: A Brief Overview
In a quest to develop an effective classifier, I turned to the ccodeBERT architecture, training it to discern password strengths into three categories: weak, medium, and strong. The training metrics were initially promising:

![image](https://github.com/DrishtiShrrrma/codebert-base-password-strength-classifier/assets/129742046/0aa81a48-0c15-4d8b-857b-01ef20e5a057)


Furthermore, metrics like Macro F1, Micro F1, and weighted F1 all revolved around the impressive 99.7% threshold, suggesting both overall and class-specific efficacy.

## Metrics vs. Reality
When testing certain passwords, the model demonstrated the following classifications:

'drishti123' → medium
'Drishti123' → strong
'drishti' → weak
'drishti@123' → strong

**Interestingly, changing the casing in 'drishti123' to 'Drishti123' altered its classification from medium to strong.** **This implies that the model may factor casing into its decision-making process.** However, from an industry standpoint, such a distinction does not necessarily guarantee that the classifier is robust.


## Bridging the Gap/ Future Directions
Achieving practical reliability in a model demands more than just outstanding metrics. To bolster the classifier's accuracy:

1. Iterative Feedback: Introducing the model in a semi-supervised setting can be beneficial. Misclassified predictions can be correctly re-labeled and re-introduced for training.
2. Training Data Refinement: Regularly updating and curating the training dataset, ensuring it aligns with industry best practices for password strength  could help.
3. Model Ensembling: Consider blending multiple models or architectures to enhance prediction robustness.
4. Continuous Feedback Loop: Set up a system where real users rate the password strength, providing continuous feedback to the model.

## Conclusion
While our password strength classifier displayed promising metrics during its initial phases, there might be some limitations when dealing in real-world scenerio. This venture underscores a crucial machine learning tenet: iterative testing, feedback, and refinement are indispensable for achieving excellence. 
