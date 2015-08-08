# Practical-Machine-Learning
Folder to submit the project for practical machine learning course
Practical Machine Learning

Project Write-up

Submitted by GRAMS

Summary:  The purpose of this project is to use a machine learning algorithm to predict exercise mode.   Various sensors on the body of the person provide readings and these readings have to be used to predict the exercise mode.  In the dataset there are 5 exercise modes in the variable classe, titled A, B, C, D and E.   I spent MOST of the time cleaning up and understanding the data.  The raw data set had 160 variables, but many of the columns contained no information at all.  Also, some of the variables were numeric, but many variables were qualitative (e.g., name of individual).  I took a two phase approach to the project (to be described below).  The best algorithm (for me) was a Random Forest algorithm, which provided a classification accuracy of 94% for a TEST data set.  I also tried a simple decision tree algorithm that did not do as well as the Random Forest algorithm.

 

Description of Two Phase Approach:

PHASE 1: EXPLORATORY DATA ANALYSIS

This phase of the project took the most time.    Upon exploratory analysis, it was apparent that there were many columns of data that were empty, or had many missing values.  There were also some Nan variables (e.g., division by 0).  If an entire column was empty, the variable was dropped from the analysis.  I also tried using only quantitative variables in the prediction model.  A very preliminary random forest run with all variables took an inordinately long period of time to train the model.  Hence, it was clear that the features had to be pruned in some manner.  I created a quantitative variable to mimic the 5 classed (A = 1, B = 2 and so on).  I performed a correlation analysis of the dependent variable against all of the features to see if any key predictors could be found.  This exercise led to about 10 predictors that seemed important as listed below.

Sample Feature correlations with dependent variable (only some variables are included here for illustration):

"magnet_belt_x"

[1] 0.030325

[1] "magnet_belt_y"

[1] -0.314773

[1] "magnet_belt_z"

[1] -0.154828

[1] "roll_arm"

[1] 0.04246

[1] "pitch_arm"

[1] -0.200614

[1] "yaw_arm"

[1] 0.011793

The final features selected from the exploratory analyses in PHASE 1 were: 

pitch_forearm + pitch_arm + magnet_belt_y + magnet_belt_z + accel_arm_x +  accel_forearm_x +  magnet_arm_x + magnet_arm_y +  magnet_dumbbell_z +  magnet_forearm_x

 

PHASE 2:

MODEL BUILDING:

Various machine learning algorithms were attempted in Phase 2.  The strategy can be summarized as:

-        Create two feature sets, one SIMPLE (with 4 features) and one EXTENDED (with all the features identified at the end of Phase I).  The 4 features included in the simple model were pitch_forearm + magnet_belt_y + magnet_belt_z + magnet_dumbbell_z.  These 4 features were selected based upon their correlations with the classe variable.

Try various machine learning algorithms in combination with these feature sets.  
I’ll report on two algorithms:
a) decision tree (the rpart method) and b) random forests (RandomForest method).

 

SAMPLE OUTPUTS FROM A) DECISION TREE

1) root 983 704 A (0.28 0.19 0.17 0.16 0.18)  

2) pitch_forearm < -31.7 90   1 A (0.99 0.011 0 0 0) *

3) pitch_forearm >= -31.7 893 703 A (0.21 0.21 0.19 0.18 0.2)  

6) magnet_belt_y >= 555 812 622 A (0.23 0.23 0.21 0.18 0.14)  

12) magnet_dumbbell_z <  -18.5 300 181 A (0.4 0.27 0.097 0.17 0.06) *

13) magnet_dumbbell_z >= -18.5 512 369 C (0.14 0.21 0.28 0.19 0.19)  

26) magnet_belt_y >= 592.5 376 257 C (0.1 0.21 0.32 0.24 0.12) *

27) magnet_belt_y <  592.5 136  87 E (0.24 0.19 0.18 0.037 0.36)*

7) magnet_belt_y <  555 81  14 E (0 0.012 0 0.16 0.83) *

The decision tree algorithm provided a classification accuracy of only about 48%.

Here is a cross-tabulation to illustrate (predicted vs. actual values for the 5 classes):

predtree                             A            B             C             D            E

       A                                    3309      650        278        207        256

       B                                    431        582        23        45         60

       C                                    709        1091      1554       624        473

       D                                   548        705        720        1567      657

       E                                    304        579        675        612       1980

 

B) PERFORMANCE OF RANDOM FORESTS

The random forest algorithm did much better and provided a classification accuracy (for a test data set held out from the training sample) of about 68%.

Here is some sample output from the random forest procedure (predicted vs. actual values for the 5 classes). The column headers are interpreted as A = 1, B = 2 and so on. yhat.rf is the predicted value (by Random Forest)

yhat.rf                                               1             2             3             4             5

      A                                                    4217      483        230              243        163

      B                                                    494        1986      367              347        319

      C                                                    142        617        2127            371        353

      D                                                   270        367        397              1941      153

      E                                                    178        154        129             153        2438

 

PREDICTION FOR 20 TEST CASES:

This final discussion pertains to the prediction for the 20 test cases provided in the project.  The best random forest algorithm was applied to these twenty cases.  Based upon the grade provided by COursera for the twenty test cases, this extended Random Forest algorithm, with all variables from the end of Phase I, provided 100% accuracy for the 20 test cases.



 

 
