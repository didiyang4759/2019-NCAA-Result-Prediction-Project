#  Data Modeling Project
 ##  2019 NCAA  Division I Men’s Basketball Tournament Result Prediction
 - [Code_Checking_ipnyb](https://github.com/didiyang4759/Data_Modeling_2019-NCAA-Result-Prediction-Project/blob/main/Modeling/FinalProject_Team14_asfor1202_2137.ipynb)
 - [Backgroud](#backgroud)
- [INTRODUCTION AND BUSINESS PROBLEM](#introduction-and-business-problem)
  * [a.Introduction](#aintroduction)
  * [b.Business Problem](#bbusiness-problem)
  * [c.Data Used](#cdata-used)
- [Methodology and Approach](#methodology-and-approach)
  * [a.Methodology](#amethodology)
  * [b.Approach](#bapproach)
  * [Decision Tree Classifier](#decision-tree-classifier)
  * [Random Forest Classifier](#random-forest-classifier)
  * [Logistic Regression](#logistic-regression)
  * [K-Nearest Neighbors Classifier](#k-nearest-neighbors-classifier)
  * [Naïve Bayes](#na-ve-bayes)
  * [Neural Network (MLP: Multilayer Perceptron)](#neural-network--mlp--multilayer-perceptron-)
  * [Support Vector Machine](#support-vector-machine)
  * [Neural Network (MLP: Multilayer Perceptron)](#neural-network--mlp--multilayer-perceptron--1)
  * [Support Vector Machine](#support-vector-machine-1)
- [Results and Model Performance](#results-and-model-performance)
- [Logistic regression](#logistic-regression)
- [K Nearest Neighbors](#k-nearest-neighbors)
- [Appendix](#appendix)


![Related image](https://lh6.googleusercontent.com/6BHC9kuuNq_OLxYqAA9Kq_NmX_Yl2T3TsJrK06yUS1cvvJfwxC0HLVuBFpz7h6c88Eni8EOAXE5g2BWUnRIItD0FSX3W8weRMr2NPJoAMi6mQ4vPbUrnIUa3uYiqoUci4_RC_T2fXVDtB41DsQ)

### **1.  EXEVUTIVE SUMMARY**
    

  

The analysis focuses on predicting the probability that a team will win. Using data from kaggle, we preprocessed it, using a total of 21 variables. Since the probability of the team winning depends not only on the number of wins, but also on coaching experience and the probability of three-pointers, we have added three of our own variables after the 18 variables, namely delta_coachexp, delta_coachexpteam, deltaFGA3Prct.

  

Second, we sampled and ran 7 independent models and compared them. By studying the accuracy, sensitive, precision, and F1Score of each model, we conclude that the decision tree is the best model. Other well-performing models such as random forest classifier and K-Nearest Neighbors Classifier.

  

The best value of F1 is 0.686 of decision tree, similarly, potentially ensemble multiple modes of different types, such as the Logistic Regression, Naïve Bayes, Neural Network, Support Vector Machine, KNN could help improve predictions without increasing bias.

  

![](https://lh5.googleusercontent.com/gmgoE7oP93nulqt6frsqdKiluoZER89CVb6EFF_qQKmx-BbkRIyTL0jsDebVfaQDQ0E-BlvFnner4YFXrWZcK6wdzNGwOFKmHK4nJ8cRa91JtlXC0hWEESJUAaSoJ4DCDztV6Vgn5QfRVSh67g)

  

### **2.  BACKGROUND**
    

  

This background of this study and literature involved from Kaggle (provided on canvas). These variables cover history, season performance, rankings and team composition statistics. Historical variables include data describing the team's performance in previous seasons. Ranking statistics, including seeds, are statistics that are published to compare teams. Season performance statistics describe different aspects of team performance throughout the season. Finally, team composition statistics represent seasonal statistics by class and residence, as well as coaching variables. We used 18 existing variables and added 3 variables of our own as predictors.  We have access to data dating back to 1984-1985 season, but we only used data from 2002-2003 season.  

deltaSeed: difference in team's seeds

deltaMO: difference in team's Massey Ordinals on day 128

deltaWinPct: difference in the team's winning percentage

deltaPointsFor: difference in the average points scored per game

deltaPointsAgainst: difference in the average points scored agains the teams

deltaFGM: difference in the field goals made per game

deltaFGA: difference in the field goals attempted per game

deltaFGM3: difference in 3 point fields goals made per game

deltaFTM: difference in free throws made per game

deltaFTA: difference in free. throws attempted per game

deltaOR: difference in offensive rebounds per game

deltaDR: difference in defensive rebounds per game

deltaAst: difference in assists per game

deltaTO: difference in turnovers per game

deltaStl: difference in steals per game

deltaBlk: difference in blocks per game

deltaPF: difference in personal fouls per game

  
  
  

**Our Added Variables**

***-   delta_coachexp:*** the difference in number of seasons the coach of opposing teams served as HC since 1985.
    
***-   delta_coachexpteam***: the number of seasons the coach served as HC with current team since 1985.
    

We used these two variables because we believe coach plays a very important role on the basketball team, and the coach’s experience is a very good indicator of the coach’s ability, since coaching College Sports in the U.S is very competitive and only good coaches get multi year contracts. And a coach who stay with the same team usually means the trust from the school and his players. For example, Coach K with Duke, Coach Boeheim with Syracuse all stayed with the same school for a very long career, and their programs are always considered one of the top programs in the country.

  

***-   deltaFGA3Prct:***The difference in the percentage of 3-PT field goal attempt in total field goal attempt.
    

We added this because in professional basketball, there is a noticeable trend in recent years that winning teams are usually the ones that shoots more 3s, we’re curious to see if that trend also holds true in the collegiate level.

  
  

### **3.  INTRODUCTION AND BUSINESS PROBLEM**
    

  

**3.1.  Introduction**
    

Since 1940 the National Collegiate Athletic Association (NCAA) has held an annual competition pitting the best college basketball teams against each other. This single-elimination tournament has grown to include sixty-eight teams vying to be crowned national champion. Every year, 68 of the best college basketball teams in the country are selected for the tournament and play through a single-elimination bracket until one team is crowned the national champion.

  

**3.2.  Business problem**
    

  

This analysis uses the strength of the seeds to predict the strength of the team. In the ncaa competition, the seed strength data and winning score data from 2003 are used. Because the strength of the seeds is a manifestation of the strength of the team Form, so you can better predict the probability of the team winning.

  

Because there are many reasons that affect the strength of the team, different coaches coach in different teams, and the coaching experience is also different. We have used teamcoaches data to analyze the most experienced coaches and the teams they have taken. Comparing different teams brought by different experience coaches, we will also analyze and compare the three-point shooting percentage of the winning team. This also concerns the strength of the team members and makes the assumption of the winning team.

  

As a result, the teams brought by more experienced coaches may not be successful. We compared the coaches of Auburn and Kentucky. The two coaches have a long time in coaching and leading the team. Time difference, but the result is not as expected. The more experienced the coaching team, the greater the probability of winning.

  

**3.3. Data Used**

  

Team coaching data is downloaded from Kaggle and includes 5 columns. Since the data is too extensive since 1985, we have selected the time after 2003 as a sample.

  

Since the data only gives the coaching start time and end time, first of all, we need to know the coaching time, so we use "Coachexp" for analysis. In the analysis, we found a key problem. In the coaching career, he has coached different teams, so we readjusted the sample and added a new time for coaching in different teams during the coaching career called "Coachexpteam" to analyze the impact of coaching experience on the team.

  

In this analysis, the "Coachexp" and "Coachexpteam" we use are both coach related. We also use the proportion of three-pointers as a variable called "FGA3Prct". They are both x variables. Model prediction, analyzing the winning probability as a variable of y.

  

### 4. METHODOLOGY AND APPROACH

**4.1.  Methodology**
    

We used almost all the models that are covered in the Predictive Modeling II class for the following reasons :

First, the nature of our analysis is a binary classification problem, the outcome of our prediction is a simple W(win) or L(lose). which means that all these classification models are suitable for our analysis.

Second, we included almost all the models that are covered in this semester’s class because we simply have the extra time to run all of them. The March Madness prediction contest has been on Kaggle for many years, the data that are provided hardly need any data cleansing, also the fact that we’re building on someone’s existing notebook saved us a lot of time. With all the extra time in our hands, we’re interested to see what’s the outcome for different models and it’s a great chance to put our coding and modeling skills to test.

  

***4.2.  Approach***
    

After entering the necessary packages, we imported the TeamCoaches dataset and excluded records before the year 2003. Because the original data does not have the coaching experience and coaching team timeline, we use Excel to calculate the data and to read the new dataset. We made sure the two new columns are added by using coaches.head() function to check.

  

![](https://lh5.googleusercontent.com/CoK3UiuyphQ1bDPNdaqAwZlIAnmqrLRbibh3s1CgG1w23rNZ_pol0lXPyMLk3VUbDTMbKTrz1CMdojENWTRVhvnGgkeiKjKdaNDOOudjLw97L8ShRH0VukHXIcUo44dnqsjzqT9rHI08uBlCGA)

We measured each model in several ways, including the accuracy score, AUC score, precision, recall, and F1 score. Since the prediction is a binary classification problem, accuracy score was informative and the primary evaluation metric. This is because accuracy score is a ratio defined by how many correct predictions were made from all predictions.

To be more specific, we used 7 different models in our analysis, including: Decision tree classifier, Random forest classifier, Logistic Regression, K-Nearest Neighbors Classifier, Naive Bayes, Neural Network (in this case, we used multilayer Perceptron, also as known as MLP) and Support Vector Machine.

  

#### ***•Decision Tree Classifier***

We built a decision tree model using the codes below, and the tree image shows that the most important variables are deltaseed and deltaMO, which is consistent with all our other models suggest.

![](https://lh5.googleusercontent.com/9YGZEHD2XK_VEbtFkIgzxVjpkODU0-XNpXpD8CnUjO7rA8N9xKikDzRPElVgX_jfCuDGSr0q9wOBq1TUoa2FL95rrqixDw8fBglufESJEjWqttk8c5i7iYgE1O8b_69iWQbQcm8a)

![](https://lh5.googleusercontent.com/zwTNvQcFeV2EAvYMNXjFxDm4rFUtLQj0H9NhIiKBbhJ-QyQwQA9-14ofESkztbx1b1ndwhjC7mlN1iPUZPt71ZFNuv6ed1C3iDGIB6IQ9smPFapWaCcHZd5-Ypa12Xw1Cvhv8FSn)

***•Random Forest Classifier****

We built the Random Forest Model by using the following code. We printed the accuracy for every possible number of number of features(1 to 21), and we found that 3 features returns the highest accuracy. So we used max feature of 3 to fit the model.

![](https://lh6.googleusercontent.com/YfFj4wyuO6EHovop1SS5oeWrHpTELoS-U7WahT31tOc2AtHQL6lecIAm8RW0NOsEth2v3fC_9G9iDxjSvRmGMJrrxRCoRxX7hMtHrso3NWySHS05u-iReg6-6AIGkfMbgQO1q5It)

![](https://lh5.googleusercontent.com/pZUxNTgTMmmSjzzPxCzNw0cpQThNFxTbzfv5lvEtgoC37pLEqKXW4rfYG4uk3agexwABBWip8hWtqdrnhYQwkSdlYsRKXj19T0l_3kilkfMNAiGEUgryJ7KbuO1feeM0dEGXPz2j)

![](https://lh3.googleusercontent.com/UxkLFgMe82nwOP1A-4Eupn1maRFexfVjiW4dlCgFPlTTrgYq2ZncHuuYPjl0E3AAe3fmELRQWM9DO_DA361lAg5qvqxyR3SqWITOs9ZXKCCOqBuiNVxrahk9sLUvDKZY4NzfNEZT)![](https://lh3.googleusercontent.com/Z3OUq1piWPPWNBL45lYdVq0SmPtjGUusLKb1glxJLugXPwiv_mR2NiNU9NzAPGbMNaE74W-KhCoDK7gPoYsQM33vhs9ryAJAKUnzKnBS4bIqMjSzG7B0q6QAREL7p82FyHfvvRHM)![](https://lh4.googleusercontent.com/1lxJHDuuyVHYw8pFaVDZwrW2XfGKSNZIWRBST9fxhEit7RM0lSD3clr9xXphl3_SXOls-qCYqTnbnXB3Tpb0Jc06tVELDaCjeMprbSWFcwoXDDa69U0RRtaH3SgJX1m-xOHfnaaY)![](https://lh3.googleusercontent.com/xNYfve2JtGh2vlCz2c-ACukWLS6IX67Lu3VK4FsSi3Ug7zGk71yvzp2CrO40S8nuek4u7A4_Tab61w-YoEeETMsY9Wr5UMd0yUSgulenkVuFN6ABvIA0BWJFoVSXY6M2LSLmIgDZ)

  

***•Logistic Regression***

The logistic regression model creates classification predictions by using the logit function, which creates an odds-value for how likely each observation is to be classified as a certain class.

For our logistic regression model, we found 4 variables to be significant:deltaSeed, deltaFGM3, deltaAst and deltaFTA. deltaMO is surprisingly not significant in this model.

![](https://lh6.googleusercontent.com/YZ2pIJgiuEzEmEk2SvUg9NVR6KyRfwBdAF5Ag7bbi5qxDc55TrsORNVjfAVPIK_tiJMJJcqU7gWp7DAIkTpzpSn_oGzzoVGBCltJYGfeDf0c98EVgHD1ilkvIbZqY9vu5m6fcTi5)

![](https://lh6.googleusercontent.com/RJzuCAsJkEDdujrCUL97zu83hXY23WiVNbW2Qe-OjkK0gN8FFkEfZJBnI54nGHWjAF2pnyA7_M_GNwEfI0mB9gflfKMH4FU7lN-9Gmexfwd2uS9hTkM5J-WJxqhZw4yF14lSoaa9)

***•K-Nearest Neighbors Classifier***

The k-nearest neighbors (KNN) algorithm is a simple, easy-to-implement supervised machine learning algorithm that can be used to solve both classification and regression problems.The KNN algorithm assumes that similar things exist in close proximity. In other words, similar things are near to each other. In our analysis, we set the k-nearest neighbors to 5, it uses the 5 most proximate observations to categorize the test data. Overall KNN has a mediocre performance compared to our other models.

![](https://lh4.googleusercontent.com/9VmpeE08vhrcx_HnaLbQS5eR2Cb6yzN71CsRUo0frPt0D-aXF6pxulxLyboG8Oc1AylJ13mpu97ZksBfdlfQBr7EazO1V3PPspzPaAVGEQJ8YMhW8hSiwDinoPqc-8mFKJMTqKmI)

  
  
  

***•Naïve Bayes***

  

Naive Bayes classification is a probabilistic method that assumes that attributes are independent. At the same time, when using Python to calculate the probability, we can take the logarithm and perform the corresponding calculation.

  


**![](https://lh3.googleusercontent.com/8Szdb_Zqi9f5wEWborZWO_lseEHBS-1LakNntX57bqdP1VA2U8JakZKLGOFU23RLQE21jqH9Mzg6AmDQTqw4X74zzQ-FDRcgLYW4Jc92Xa6q9GSWMOyqwXFLD_Xb78JuhkGV41nyS43GYj5yyQ)**

  

![](https://lh6.googleusercontent.com/ewRJiSCDkKkT5O5L_B5Kr7z7lONMU_fvjEPpDdxhXhrvYXOUQqKF6OABTAnszjvVzfXAYPvh7dZEtgChW-fBfKAkndXGoJtUOZb6KJ1igP3ZDQ6_S73mk1aNeHjzku8p98ia39wgeIWicA8JPg)![](https://lh6.googleusercontent.com/OLg9jgUUklR4kGhINhZZHVt3oeSJyw6e7sLPCBG0keX1DfGeDwEDg7F2fusKmee6T327gu1BiXfRQ4soEibo42ftY1gWmvcc1RNNC_5F7Y_ItjHGBUwXJYQa1pXjNAN2vSp_QurG26ga0bQ1yA)

  

Naive Bayes classification is a probabilistic method that assumes that attributes are independent. At the same time, when using Python to calculate the probability, we can take the logarithm and perform the corresponding calculation. Because Naive Bayesian theory uses conditional probability, some probabilities are predicted to be zero. Although we try to avoid variables and inexact numbers in the data, there is a correlation between attributes, and biases still occur, leading to precision and specificity values are not good.

  

***•Neural Network (MLP: Multilayer Perceptron)***

  

Neural networks are dedicated to building complex functions through neurons that are interconnected with neural networks. Neural networks make predictions through forward propagation. MLP or multilayer perceptrons are a form of using hidden layers to create these functions and therefore use these neural network functions and relationships to predict value.

  

![](https://lh3.googleusercontent.com/u9Pyy9DQqi_VPP_3MczebhsZaQPeZlORaBgIavfByVRt5aAk3hDNt-OUQxTy_MRSMY4TKYucRrTr3k-nyXy8QSZZtuwRRskYNEczOQJogjxVMePXKJZj9kz7SwlycXC_pPhz088wX8fKqSKmzw)

![](https://lh3.googleusercontent.com/l7TWZGrfLp9TTqmM_HvQ00pZnUQBfx6KT-pZk6W6L_fZsoC_d7t6T4hLc7pv1E_lnXQCFWxj7WpeJIn7awAsxY0KVEhaZD9slekhW0Os8PSO9Zin_kK1ey01nLINadyUY_Kg95jxyIB5itCQmA)![](https://lh6.googleusercontent.com/k-WD8ueOb7vIsVZUfNpE55MVQP5cAVtGc2r-Y7ZGgFIq77a-yuYYfxYtt1BWmB1b0fISprqpi5OYzVbqfLPr9AEmVdHpXA2G4agM88dP9_azL2MUd2tcUk9s-UkelTnYG22-cPWnnS1upppiDA)

  

The accuracy of the output results reached 0.903. For our MLP classifier, we created three hidden layers with 5 neurons, which resulted in an accuracy score of 0.60. But unexpectedly, specificty, precision, F1 -score is much lower than we thought, only 0.308, 0.556 and 0.44 respectively. We analyzed the general reasons. Because the recall value is low and only 0.30, the model has a weak ability to recognize positive samples. Because precision reflects the model against negative samples. The discriminating ability of precision is low, and the model is weak in discriminating negative samples. F1-score reflects the lack of stability of our model. We consider this model to be invalid.

  
***•Support Vector Machine***

  

After analyzing the naive Bayesian model, we started to try Support Vector Machine. SVM is to create a new instance assigned to two categories. When the data is not labeled, supervised learning cannot be performed, and unsupervised learning is required. , It will try to find natural clusters of data to clusters and map new data to these already formed clusters.

![](https://lh6.googleusercontent.com/isL1Uu25ZNAOpDYvhuMyeu48SUKCh1QIBVTNP15N7hwUdmTFr2S7BfbNIObvblk6xLlvkhHP_cibsykk_3DvloHbotM89YjxEgM8m8Fqr61NrHHD15j4wcgAnisInSZGVzXY_DVu)![](https://lh3.googleusercontent.com/epfUru9gdbTnmS6eYi6qVOD2pa-7hP_l7qNv82s1tOxOutJbQTSxNG7AMypjRGMiKOwTWzhI0j7VmLlmsTYYneWJvGk-EVr32TBdIwTi2yFDJ_ESZ1H6zWzqBRlmzoKh22DxDFVo)

  
  

![](https://lh5.googleusercontent.com/Lyzu9aoLGCXNWkM1dUXJCo03mMhBoCXjJDPsd67IVUeiLX9XB2vK4n5zh0fwSutx_QLU-1yPErlP9Jr0YqY9JfVKIvVqh-6OzEMfauvtRLNf1z4klVwrVmJ1DtdMdQedt_XSpZy3)

  

From the output results, the AUC value is 0.61, which has a fairly good model performance. Sensitivity and specificity have higher values of 0.573 and 0.749, especially the specificity, which is higher than any previous model. The recall also has a high value. The value reached 0.75, indicating that the model is stable.

  

***5. Results and Model Performance***

  

Since this prediction is a classification problem, we try to use accuracy, sensitivity, specificity, precision, and F1Score as the reference index of the evaluation model. Each method will be applied to an important evaluation method. We calculated the model with the best comprehensive result. In order to gain a better understanding of the evaluation of the model, I will introduce these matrices truly mean.

Accuracy refers to the ratio of the number of correctly predicted samples to the total number of predicted samples, regardless of whether the predicted samples are positive or negative.TP/(ITP=FP)

Precision refers to the ratio of the number of correctly predicted positive samples to the number of all predicted positive samples, which how many of all predicted positive samples are real positive samples. (TP/TP=FP)

Specificity refers to the ratio of the number of correctly predicted negative samples to the total number of valid negative samples, that is, how many negative samples can I correctly find out from these samples. (TN/TN+FP)

F-score is equivalent to the harmonic average of precision and recall, which is designed to refer to two indicators. [2*(Precision*Recall/Precision + Re-call)]

Decision tree is our first analysis model, it using “DecisionTreeClassifier” via “sklearn.tree”, the winning probability as a variable of y. Decision tree is a very common classification method, which can specify a set of attributes and a category for the sample in the entire database. At the same time, each node represents a classification rule, and each branch represents the classification of the attributes of this type of object. This process can be used to split the tree recursively. When the segmentation can no longer be performed or a single class is defined, the recursive process is completed. This is a model that is easier to analyze and understand. Through interpretation, you can clearly understand the meaning of the decision tree expression. And it can analyze large data in a relatively short time. At the same time, we choose to use it with random forest to improve the classification accuracy of the decision tree.

![](https://lh3.googleusercontent.com/BtHi5IjM7KXau1PZMJnlTnwIoS84ITFqet4VgTvE0GvlCP7eDqodCIxlJDN_yPSxjrr2aC2dRVuM7uLDCSYVnYdhNGlcIC4JvgKTI09ZNzLae_vuWw20Yk17n4_kTZCBPgWwpe1B)

![](https://lh4.googleusercontent.com/6xEGnAf51TycEjGsZfB3uzpptNNQ766WDdxHge2WHHg1xkSSpVz9075ceOjRe29Mfz7TTIpYSuOtrOlH-QfZpv7tic1sucWe16Q1lrTzvHq_SyKg_bJOcOMKeqjfgqcbAoEcdPug)![](https://lh4.googleusercontent.com/IJEarkZbXVlDGH2B_RNamA8t9BH8Go_WqAiuCq1zl_Ylq7ouicZWpwDHb2zlUBmVAaMYEUuhuPBXahl_vau8-d64P4r5whntlwYdCB6ytst3kVFjX1A54xvMx8EMGZnLbD5ZWNKL)

  

The data of the decision tree needs to be processed in advance. The first is the creation of node N. We need to establish standards to limit their nodes and branches. In general, the first tree will have two "features". Such a high probability will avoid overfitting and it is easier to set up. The second tree will undergo the pruning process. As can be seen from the figure below, it cannot exceed three layers (max_depth = 3). Considering how well the model fits the training data, we did not choose complex pruning. This implies that some of the smallest function subtrees are lost.

in order to evaluate the performance of decision model, we create 4 evaluation models, from the figure we can get that the accuracy of the decision tree is 68.57%, the sensitivity score of 67.96%, the specificity score of 69.16%, and the precision score of 65.96%. Also, we build another model in order to the value of precision, recall and F1_score for decision model. We can see the result from above table. Whatever for 1 (win) or 0 (not win) their score doesn't have too much different and very stable.

![](https://lh5.googleusercontent.com/QeK8PSg4Q3V3Mef2E3pXzOGeUl3UMYaGKah44VZlc_EuQXvZ4IXQghonDV1uAzbAw_XRQ5DMSKEiMyJLGKirYnx0qLOgjAbMNqRszW4QTarQ4TMOwJe0o0wV71ZFgzPPOt3b8kF8)![](https://lh6.googleusercontent.com/EhVm4XUnwXNquUtCZ2i1DG3m_zKw0uZXTJVmblBTwOQ_ggYLshin3aDeCQ-q59WrFTb0CJv6B2gy3piHkHtl90lvNcWzFtqIUT1crSXWrMa953GdogEqNuwaPVSTi_MSNchXjNDK)![](https://lh5.googleusercontent.com/FhN8bWAqT6UZaAS3CsHXsOUgKDS8nwLjkc7X1VHO3zB1-xaq3w8C5AVU_pjghUxR0BWbL3pzAmQrhw50iJH8ojEaM7OYwb4WVOsCzVoRWDUX6yv0Mam-QJOILuqELI8DbFubuoya)

The AUC score for this model was 0.724. When we set the threshold to 1 and 0, we can get two points (0,0) and (1,1) on the ROC curve. From the figure, we can see that the roc curve is smoother, which means that the TPR and FPR values tend to balance. So, accuracy is a meaningful reference for the model. From the results, the model can effectively perform classification analysis.

  

***Random Forest***

random forest model is our second analysis model, it using “BaggingClassifier” via “sklearn.ensemble”. Random forest mainly refers to integrating multiple decision trees into one algorithm, and the basic unit is still the decision tree, so it tends to over fit. Intuitively, every single decision tree has a classifier, and the output content is based on all the categories that voted the most in random forest integration as the final output. This means that the most suitable feature can be found by continuous replacement and Optimization in the operation. It has a good accuracy in the current algorithm. we tried a Random Forest to use our 21feature. The results are as follows. The best is feature3，accuracy score of 67.62%。We also found the features that have the greatest impact on the model. It can be seen from Figure 2 that deltaSeed is the most important feature affecting y.

![](https://lh4.googleusercontent.com/NgoHCEOAu5djxu3WY6nRhnEAQT1yYu-aeqpW4wu_fakrvUpYyNCLlLeS0CRf20KlWfXvbB-7wOpDQ8qmN2jCrSCWzW3mEFgCi3w433LLraY5z3lccC8GsYJYWQjUj1XcmSPOzuvJ)

![](https://lh3.googleusercontent.com/59KwkkjvbffKSrdR4RZbw0-Pnty20kxyJAr8zv436Fyskbq7UEs-3R5a5yYxPP6_9vKlF8vg3nsnt97P8DyivUXXLsOBJP8d8sJ8eiK4LT9d78rQIpQ1OBLQNgjVmINz-4T9GFLz)

![](https://lh3.googleusercontent.com/aMnbYCuVTzAyyhA6XnXEyVNa_67TtwTp9ecWhf18nnlrGW3b1mvBSTpnPAVgRbU2cbM_7X7JaRad66qFG0XLxwjjJXj4QhnpDq2FZBtz1s7EoPuw31py44d0Hon1Or7jWtQ46BbL)

The results of our evaluation model for random forest creation are as above. Accuracy score of 67.62%, sensitivity score of 60.19%, specificity score of 74.77%, and the precision score of 68.66%. These are not low numbers. This shows that random forest can analyze and predict the model. The AUC score for this model was 0.745. The maximum specificity value has reference value to the model. Compared with the previous decision tree, there is no big difference between the two results. The difference is that the random forest finds a more accurate feature.

  

***Logistic regression***

  

Logistic regression, also known as logistic regression analysis, is a generalized linear regression analysis model, which is essentially a binary classification problem. The binary classification problem is that the predicted y value has only two values (0 or 1). We also made logistic regression models to analyze and predict. The logistic regression model uses a logit function. The output is classified into unexplained values.

![](https://lh3.googleusercontent.com/qivB6aKJpZj9MqEMGjMd4qyak3K0NSsngly41o4yPKEQuIKBMLDKNPnnkygq8Yih3nbE5AGAmZeMl21SU1iHVkYQGS0i7bOXg_cTdL7lKhjZyYSEaWURpzVu2MNWDjcEXvbxvirc)

![](https://lh3.googleusercontent.com/NCr3XfMiW44gFg4ppgaIRaegiB1aoGYcfy3uCJVxSYFNJSnqYI4VqrCzkpa5diUtayCLWHF_zpy_0iunQtZIylMLJTxPfHr5-5kw00Z_spRmGWVvNxzXbA9y1E_uYQtcLikAdSYD)

  

The model has an accuracy score of 67.62 %%, a sensitivity score of 63.1 %%, a specificity score of 72 %%, and the precision score of 68.42%. The AUC score for this model was 0.745. The overall score is slightly higher than the decision tree and random forest Model results.

  

***K Nearest Neighbors***

  

The k-NearestNeighbor classification algorithm is one of the simplest methods in classification technology. K nearest neighbor is that each sample can be represented by its nearest k neighbors. KNN does not have an explicit learning process. The data set already has classification and eigenvalues in advance, and it will be processed directly after receiving new samples. The value of k is very important in the knn model. Because increasing the value of k will make the whole model simple. If the value of k is too small, overfitting is likely to occur. Here we set k=5 , which defined that 5 closest observation. And we got a good accuracy score of 65.71%.

![](https://lh4.googleusercontent.com/jiy9wcayivcwhGCknULO5nfTl4J5sXZ6krlp_UYbPpRkheYvjtO_itBfW4NLDasg0wyywN7B5nbG0zs9lQI8PwfOiyoX_y2yTreKywy2xwFUzpiLvah7IpSX2qQoJIFr3v9tIz8l)

![](https://lh3.googleusercontent.com/O0b_2pF39yWL6mCkZ7Ff798Su_jNXZJ82cP7XJwz9CxJMLf9kj8afsKj19xO9XN0dLNMpI5RVTmqHhi1UkMc0ELLfsLBN-YYN3OCEHndVS0Ai6QTTFZvK51iB8PNRRa17Jmf9ki9)

  

### 6. Conclusions

  

In summary, we built eight models with different levels of accuracy. Among them, the decision tree has the highest accuracy in a set and the highest average score of the model performance indicators.

  

![](https://lh5.googleusercontent.com/gmgoE7oP93nulqt6frsqdKiluoZER89CVb6EFF_qQKmx-BbkRIyTL0jsDebVfaQDQ0E-BlvFnner4YFXrWZcK6wdzNGwOFKmHK4nJ8cRa91JtlXC0hWEESJUAaSoJ4DCDztV6Vgn5QfRVSh67g)

  

By comparing the accuracy, sensitivity, specificity, precision and F1 score of different models, the decision tree is the top performer in these metrics, therefore, decision tree is the best model in here. Similarly, better models also have logistic regression.

  

It is important to observe whether the equations change as the team advances in the tournament on this data set and research question. We assume that the statistics of the team composition, especially the coaching variables, are more predictable in future rounds, and such as Rankings like seeds are less predictive.

  

One of all the remaining models is constructed from a training subset, of which Neural Network and Vector Support Machine are two very complicated models. In order to verify its accuracy, we tried a variety of neurons in the neural network. In the future, in order to further improve the accuracy of various models, I think we can try other methods, such as using integrated methods or cross-validation.

  
  

### 7. Appendix

Codes uses in dataset

deltaSeed: difference in team's seeds

deltaMO: difference in team's Massey Ordinals on day 128

deltaWinPct: difference in the team's winning percentage

deltaPointsFor: difference in the average points scored per game

deltaPointsAgainst: difference in the average points scored agains the teams

deltaFGM: difference in the field goals made per game

deltaFGA: difference in the field goals attempted per game

deltaFGM3: difference in 3 point fields goals made per game

deltaFTM: difference in free throws made per game

deltaFTA: difference in free. throws attempted per game

deltaOR: difference in offensive rebounds per game

deltaDR: difference in defensive rebounds per game

deltaAst: difference in assists per game

deltaTO: difference in turnovers per game

deltaStl: difference in steals per game

deltaBlk: difference in blocks per game

deltaPF: difference in personal fouls per game

codes used in own model analysis

delta_coachexp: the number of seasons the coach served as HC since 1985

delta_coachexpteam: the number of seasons, the coach served as HC with current team since 1985.

deltaFGA3Prct: Three-pointers as a percentage of overall

Resources used in addition to lecture and slides

We did not use other resources.
