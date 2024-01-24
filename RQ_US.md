RQ1 (Confirmatory): Does parent-child satisfaction and parental support during childhood predict current romantic relationship satisfaction?
RQ2 (Confirmatory): Does adult attachment mediate these associations?
RQ3 (Exploratory): What are the differences between American and Chinese samples in answering the first two research questions? 
RQ4 (Exploratory): How do different adult attachment dimensions play varied mediating roles across different cultural contexts and in comparisons between father-child and mother-child relationships?

# RQ1 for US
Use only US sample for answering RQ1. But I think it’s convenient that I also analyze the chinse sample and put the results in the RQ3.

The mplus files are in Q1_US folder. I rerun some of the models using the new data (after scaling duration etc), found no difference in model fit or standardized coefficient.

The model is 3 predictors (each has it's indicators: 4+10+10), 7 covariates, 1 outcome (5 indicators). 36 obseved variables.

## Check the df of the hybrid model (get familiar with how mplus works, do not need this in regular research step)
I found in the mplus diagram, there are links between the covariates. I want to check the mplus results of the coviarates: make sure if the default setting is to estimate the corelations between the coviarates (there are real correlations) or it's just the problem of the mplus diagram (no correlations, but shows to have).
### Caculate the knowns and unknows based on my model (class 4 ppt)
measurement knowns:36*37/2 = 666

measurement unknowns:25 loadings(29-4) + 11 variances of constructs + 11*10/2 + 29 error variances = 120

measurement df=546

structrual knowns:11*12/2=66

structrual unknowns: 10 paths + 11 variances + 3 covariances between exo =24
structrual df=42

hybrid model df= 546+42=588

### find the real problem and fix it
The df based on the diagram is 567. I think the differences is about the structrual unknows: 10 paths + 11 variances + 24 covariances (in my model, it should be 3) between exo (3+7*6/2) =45. then the structrual df=21, so the hybrid model df= 546+21=567. 

It means that I need to rewrite the syntax so that it reflect my real model.

For the first try, I add commend to make sure the correlations between these covariances are set to 0, such as rela_sta WITH age@0; 
However, I do not know why, but the previous version did not correlate these observed variables to pcs, psf and psm, but now they did. Somehow it happened so I need to make these correlations to 0 as well.

For the second try, the df is 588 now. it works.

## test the hybrid model with all three predictors and all covariates (class4 p16)
### StepA: check if the measuement model consistent with the data & Step B: Revise the measurement model
df=546 chi2=1638
RMSEA=0.075 (0.05-0.10=accecptable fit) v
CFI 0.878 / TLI =0.859 (0.9-0.95=accecptable fit, a little bit low)
SRMR=0.042 (<0.08 =accecptable fit) v

Looks fine. Keep checking the normalized residuls and MI. (before that I have checked the factor loadings, looks fine: not <0.3 or >0.95;correlations between factors is not >0.85)

when I'm checking, I find another proplem: I need to tell mplus some binary variables are catigorical: CATEGORICAL = rela_sta ..After this, the model fits increase. But the method changed to WLSMV. Plus, in the output, there are threshold, gpt said "the thresholds you see are part of this IRT-based approach to handling binary and categorical variables." In fact, I found it might not be neccecery, since these categorical variables are not outcomes.

Check for Heywood cases (standardized loading is larger than 1 and the error variance is negative): looks fine

Check for empirical underidentification (lack of covergence orhuge standard eorrors): the only problem is since I use WLSMV, no standardized and normalized residuals are available. As I have scaled most variables, from checking the raw residual might be fine as well, however, it shows every residual is 0, I think there is problem, but I will leave it as is (might be fine in path model).

Check for MI, could correlate M1-F1 etc. After that, the CFI turns to 0.947. The respecification is pretty sucsess.
df 536 chi2=659
RMSEA 0.025
CFI 0.947
SRMR 0.051
Note, this is with the catigorical command (estimator is WLSMV), the measurement model fit without the command (so it's ML) is the same to the deleted paths model as follows.

### StepC: Evaluate deleted paths

Chi-Square Test of Model Fit

          Value                           1002.498
          Degrees of Freedom                   536
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.049
          90 Percent C.I.                    0.044  0.054
          Probability RMSEA <= .05           0.609

CFI/TLI

          CFI                                0.947
          TLI                                0.940

Chi-Square Test of Model Fit for the Baseline Model

          Value                           9420.729
          Degrees of Freedom                   609
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.038             
There are no deleted path, only deleted correlations. Here are the significant ones.
PCS with SES 
PSF WITH SES 
PSF WITH PCS
PSM WITH SES
PSM WITH PCS
PSM WITH PSF
RELA WITH DURATON
RELA WITH GENDER2
AGE WITH DURATION
SES WITH DURATION
GENDER 2 WITH GENDER3

### StepD:Test of the Specified Paths and Correlations
I add 11 correlations from step c. Now the df is 536+(45-11)=570 (the same to the model fit information)

PCS, RELA_STA and gender_2 could be kept, the other paths should be deleted in the final model.

Chi-Square Test of Model Fit

          Value                           1048.393
          Degrees of Freedom                   570
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.048
          90 Percent C.I.                    0.044  0.053
          Probability RMSEA <= .05           0.727

CFI/TLI

          CFI                                0.946
          TLI                                0.942

Chi-Square Test of Model Fit for the Baseline Model

          Value                           9420.729
          Degrees of Freedom                   609
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.049

#### Standardized coeeficients
RRS      ON
    PCS                0.303      0.107      2.820      0.005
    PSF                0.000      0.062     -0.008      0.994
    PSM               -0.075      0.094     -0.798      0.425

#### R2
0.390

## test the hybrid model with only PCS, RELA_STA and gender_2
### Step A
df=40
model fit is fine.

### Step C
RELA WITH GENDER2 is significant, need to be kept.

### StepD:Test of the Specified Paths and Correlations
No specified path needs to be deleted, so this model is the same to the model in step e.
### StepE: Trimmed Model
It is reported that there is some problem with the parameter for the correlation betwwen rela and gender. Before constrain it to 0, the model fit is:
Chi-Square Test of Model Fit

          Value                            131.086
          Degrees of Freedom                    42
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.077
          90 Percent C.I.                    0.062  0.092
          Probability RMSEA <= .05           0.002

CFI/TLI

          CFI                                0.962
          TLI                                0.951

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2382.205
          Degrees of Freedom                    54
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.050

#### STDYX Standardization
RRS      ON
    PCS                0.249      0.045      5.572      0.000

 RRS      ON
    RELA_STA           0.585      0.037     15.708      0.000
    GENDER_2          -0.104      0.045     -2.322      0.020
#### R-SQUARE
0.392

### final trimmed (constrain the correlation betwwen rela and gender to 0, use this for further analyzing, but I think both are ok)
After constrain it (makes more sense and simpler), the model fit is as follows (although it also shows something's wrong with the parameter related to rela_sta)

Chi-Square Test of Model Fit

          Value                            144.332
          Degrees of Freedom                    43 (I have checked the df, by add measurement df 40 and structrual df 3)
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.081
          90 Percent C.I.                    0.067  0.096
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.956
          TLI                                0.945

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2382.205
          Degrees of Freedom                    54
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.063

#### STDYX Standardization
RRS      ON
    PCS                0.247      0.044      5.577      0.000

 RRS      ON
    RELA_STA           0.578      0.036     16.045      0.000
    GENDER_2          -0.103      0.044     -2.349      0.019


#### R-SQUARE
0.405


## Should I keep both covariates?
I think to answer RQ1, it's better to keep both. For RQ 3, to compare, maybe delete is better.
### model with only rela_sta
Chi-Square Test of Model Fit

          Value                            107.428
          Degrees of Freedom                    34 (checked. 33+1)
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.077
          90 Percent C.I.                    0.061  0.094
          Probability RMSEA <= .05           0.003

CFI/TLI

          CFI                                0.968
          TLI                                0.958

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2353.257
          Degrees of Freedom                    45
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.045
          #### STDYX Standardization
#### STDYX Standardization
RRS      ON
    PCS                0.238      0.045      5.272      0.000

 RRS      ON
    RELA_STA           0.566      0.037     15.258      0.000
#### R-SQUARE
0.377

### model without covariates

Chi-Square Test of Model Fit

          Value                             77.735
          Degrees of Freedom                    26
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.074
          90 Percent C.I.                    0.056  0.094
          Probability RMSEA <= .05           0.018

CFI/TLI

          CFI                                0.976
          TLI                                0.967

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2192.204
          Degrees of Freedom                    36
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.028
#### STDYX Standardization
RRS      ON
    PCS                0.184      0.056      3.314      0.001
#### R-SQUARE
0.034 


## moderation
Out of curiosity, I checked if rela_sta and gender are the moderators. Turns out they are not.
    PCSXRELA_S        -0.117      0.271     -0.431      0.667
    PCSXGENDER        -0.120      0.237     -0.506      0.613
    
## is using means ok compared to latent variables?
### Model with 2 covariates (RRS is latent. I tried RRS as mean, not work)
Model fit is ok for the model with 2 covariates (RRS is latent), and is very good for the one with one covariates (RRS is mean). For the first model, it's model fit is not good (RMSEA is bigger than 0.1). For the second model, the model fit is good, but the df is only 1, with R square only 0.329. Therefore, do not use the means.

Chi-Square Test of Model Fit

          Value                            107.972
          Degrees of Freedom                    20
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.111 (not good, do not choose this one)
          90 Percent C.I.                    0.091  0.131
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.931
          TLI                                0.914

Chi-Square Test of Model Fit for the Baseline Model

          Value                           1304.055
          Degrees of Freedom                    25
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.068
#### STDYX Standardization
 RRS      ON
    PCS                0.235      0.043      5.494      0.000
    RELA_STA           0.577      0.036     15.952      0.000
    GENDER_2          -0.102      0.044     -2.307      0.021
#### R-SQUARE
0.398

### Model with 1 covariate:rela_sta (RRS is also mean in this model. I tried the latent one, RMSEA is bigger than 0.1)

90 percent CI over 0.1.

Chi-Square Test of Model Fit

          Value                              3.092
          Degrees of Freedom                     1
          P-Value                           0.0787

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.076
          90 Percent C.I.                    0.000  0.179 (over 0.1)
          Probability RMSEA <= .05           0.212

CFI/TLI

          CFI                                0.984
          TLI                                0.969

Chi-Square Test of Model Fit for the Baseline Model

          Value                            136.031
          Degrees of Freedom                     2
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.039

#### STDYX Standardization
RRS      ON
    PCS                0.209      0.042      4.935      0.000
    RELA_STA           0.534      0.037     14.601      0.000
#### R-SQUARE 
0.329

# RQ2

Tried to include sec when the model still have PSF and PSM, the results are very messy, especially for the just identified model (even not converge), so I decide to just follow what I planned

## Step A & B measurement model
Chi-Square Test of Model Fit

          Value                            127.113
          Degrees of Freedom                    47 (checked.47=78-31.78=12*13/2;3+4+9++5*4/2=31)
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.069
          90 Percent C.I.                    0.055  0.083
          Probability RMSEA <= .05           0.016

CFI/TLI

          CFI                                0.968
          TLI                                0.955

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2593.039
          Degrees of Freedom                    66
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.030

## Step C deleted paths
The model fit is checked (the same to measurement model).
It seems like the deleted path PCS to RRS is also significant: 0.103 (p=0.017).
RRS      ON
    PCS                0.103      0.043      2.388      0.017

 RRS      ON
    SEC                0.485      0.041     11.742      0.000
    RELA_STA           0.399      0.042      9.420      0.000
    GENDER_2          -0.086      0.040     -2.156      0.031

 SEC      ON
    PCS                0.265      0.051      5.168      0.000

 PCS      WITH
    RELA_STA          -0.102      0.054     -1.872      0.061
    GENDER_2           0.094      0.055      1.731      0.083

 SEC      WITH
    RELA_STA           0.407      0.044      9.213      0.000
    GENDER_2           0.036      0.053      0.674      0.500


RELA_STA WITH
    GENDER_2           0.190      0.051      3.742      0.000



R2=0.553
## Step D specified paths
### Keep the 1 path and 2 correlations from step3 (final one). 

Chi-Square Test of Model Fit

          Value                            135.517
          Degrees of Freedom                    50 (delete 3 correlations)
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.069
          90 Percent C.I.                    0.055  0.083
          Probability RMSEA <= .05           0.013

CFI/TLI

          CFI                                0.966
          TLI                                0.956

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2579.793
          Degrees of Freedom                    65
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.048
#### STDYX Standardization
RRS      ON
    PCS                0.102      0.042      2.402      0.016

 RRS      ON
    SEC                0.484      0.042     11.642      0.000
    RELA_STA           0.391      0.041      9.524      0.000
    GENDER_2          -0.083      0.039     -2.142      0.032

 SEC      ON
    PCS                0.309      0.046      6.777      0.000
#### 
R2 0.568

## what happened if I do not use the final model as suggested by the steps?
### model that did not include the deleted path PCS to RRS (I think the path need to be kept)
Chi-Square Test of Model Fit

          Value                            141.164
          Degrees of Freedom                    51
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.070
          90 Percent C.I.                    0.056  0.084
          Probability RMSEA <= .05           0.009

CFI/TLI

          CFI                                0.964
          TLI                                0.954

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2579.793
          Degrees of Freedom                    65
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.041

#### STDYX Standardization
RRS      ON
    SEC                0.524      0.038     13.858      0.000
    RELA_STA           0.368      0.041      9.031      0.000
    GENDER_2          -0.072      0.039     -1.842      0.066

 SEC      ON
    PCS                0.309      0.046      6.779      0.000

#### 
R2 0.554
### model that did not include the delted path PCS to RRS and did not include the correlation between rela and gender (I think it should be kept)
Chi-Square Test of Model Fit

          Value                            154.862
          Degrees of Freedom                    52
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.074
          90 Percent C.I.                    0.061  0.088
          Probability RMSEA <= .05           0.002

CFI/TLI

          CFI                                0.959
          TLI                                0.949

Chi-Square Test of Model Fit for the Baseline Model

          Value                           2579.793
          Degrees of Freedom                    65
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.050
R2 0.559

## step e trimmed model
I think nothing should be trimed from model in step d

## bootstrap
The model fit keeps the same with the final model (df=50).
                  Lower .5%  Lower 2.5%    Lower 5%    Estimate    Upper 5%  Upper 2.5%   Upper .5%

Effects from PCS to RRS

  Total              0.160       0.208       0.238       0.391       0.538       0.566       0.619
  Total indirect     0.129       0.149       0.162       0.233       0.320       0.337       0.375

  Direct
    RRS
    PCS             -0.043       0.008       0.030       0.158       0.280       0.304       0.367


# RQ3 part 1
## briefly check the differences with the old version Chinese data
Moel fit is fine.
rela_sta can imapct RRS, but the gender2 can not in this situation. COVID can, for Chinese. 
Need to change the covariates for further analysis.

## measurement invariance (MG-CFA. class 10 after p14)
PCS and RRS

Partial measurement invariance: Some factor loadings vary across groups; others do not.

Groups may differ in their variabilities in the common factor or the errors (check these AFTER the loadings), it’s not necessary to have complete equivalence across all parameters to talk about measurement invariance.

I will use reference laten mean = 0 Approach (for the mean structure) and marker factor loading (fixed variance approach is not recommanded in MG method)

### Step 1: Unconstrained Common Model (Configural Model,freely estimate loadings, means/intervept, residual variances)
df=52=9*10/2*2-19*2(19 is the parameter it evaluate that I counted for each group). The df for the mean structure is 0 (for us,9-9, for china,9-9).

Do not need to free RRS with PCS, because it does not constrain them by default.

Chi-Square Test of Model Fit

          Value                            134.926
          Degrees of Freedom                    52
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                77.735
          CHINA                             57.192

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.076
          90 Percent C.I.                    0.060  0.092
          Probability RMSEA <= .05           0.004

CFI/TLI

          CFI                                0.974
          TLI                                0.964

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3274.225
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.037

### Step 2 constrain factor loadings- Metric model
df increase by 7 (constrain the loadings)
Chi-Square Test of Model Fit

          Value                            142.318
          Degrees of Freedom                    59
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                80.222
          CHINA                             62.096

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.072
          90 Percent C.I.                    0.057  0.087
          Probability RMSEA <= .05           0.010

CFI/TLI

          CFI                                0.974
          TLI                                0.968

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3274.225
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.044

### Step 3 constrain intercepts-Scalar model
df increase by 7
Chi-Square Test of Model Fit

          Value                            171.644
          Degrees of Freedom                    66
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                90.378
          CHINA                             81.265

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.076
          90 Percent C.I.                    0.062  0.090
          Probability RMSEA <= .05           0.001

CFI/TLI

          CFI                                0.967
          TLI                                0.964

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3274.225
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.050
### step 3 partial (intercept)
Check if free some of the intercepts would make the model an acctepted one. When deciding which intercepts to free, I check the standardized residuals of the intercepts.

At first , I tried free R2, R4, R5, the chi2 is about 145, df=63.

Then, I tried free R2, R5, the chi2 is about 146.5,df=64.

At last, I tried only free R5, the chi2 is 153,df=65, seems like the chi2 difference test would be significant this time.

Using the rule for chi2 difference test, if two nested model is not significant different from each other, choose the more restrictive one (more df). Therefore, choose to free R2 and R5. Use this model from this step.

Chi-Square Test of Model Fit

          Value                            146.499
          Degrees of Freedom                    64
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                83.619
          CHINA                             62.880

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.068
          90 Percent C.I.                    0.054  0.083
          Probability RMSEA <= .05           0.020

CFI/TLI

          CFI                                0.974
          TLI                                0.971

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3274.225
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.046

#### questions
1. why some standardized residual show 999, when there are respective normalized ones
2. why a standardized residual could be as big as 6, while the respective normalized one is onky about 1, which to follow?


### Step 4: Equality of residual variances (and covariances)
The chi2 turns to 500! Then I check the MI, decide try to free S1 S2. It still suggest to constain S3,S4, R1,R2,R4. I think it's just too much, meaning the residual variances is just different between groups.

#### note
This step is optional.
Not essential for multiple group analysis.
Important if you want to examine whether the reliability of measures is equivalent across groups.

### Step 5:  Equality of Factor (structural) means

Since the model in step 4 is optional and is not a good fit model, I will moderate based on the model in step 3 partial.

Chi-Square Test of Model Fit

          Value                            544.787
          Degrees of Freedom                    66 (constain 2 means to be 0, as the reference group)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                87.396
          CHINA                            457.392

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.162
          90 Percent C.I.                    0.150  0.175
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.850
          TLI                                0.837

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3274.225
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.900

#### questions
1. The ppt does not say much, I guess I could just constrain the factor means in second group to be 0?
Yes. Confirmed by the class syntax.

2. I think the ppt said the means in the second group reflect the difference between these two groups?The results show huge difference, which did not seems right. I want to check.
These estimates are actually the relative differences on the factor means, as compared to the reference sample (in the metric of the marker variable). 

Means
    PCS                4.561      0.145     31.546      0.000
    RRS               -0.695      0.136     -5.105      0.000

Standadized means
Means
    PCS                2.582      0.161     16.046      0.000
    RRS               -0.529      0.107     -4.921      0.000
    
3. Then what is the marker variable (in the sentence "in the metric of the marker variable")? The ones constained to be equal across the groups?
In p 9, it said "Option 1: set the intercept of one of the variables = 0. This variable becomes the marker variable for the mean structure and so the latent mean is scaled in the metric of the marker variable.". BYW, option 1 is Fix the same indicator to be equal to 0 across the two groups.

To be honest, it is very confusing, I am using the option 2 (fix the mean of the latent variable to 0;Must have at least one intercept per factor constrained to be equal across groups), then how could the marker variable be the intercept=0 related variable? 

If so, which marker variable does it mean? The factor loading =1 related variable(indicator)? Is the metrics for factor loading the same to the means?

I asked chatgpt and she said "In SEM, the marker variable is typically the first indicator variable you list in your measurement model or the one for which you fix the factor loading to 1". I will just take this as the answer.

### Step 6:  Invariance of Factor Variances and Covariances (Steps 5 & 6 are interchangeable in terms of order)
Since the model in step 5 does not work, I use the model in step 3 partial 

#### step 6_1 Factor Variances
I tried to only constain the variance, but not works well: turns to be constain the standardised variance to 1 and make the correlation to be equal across two groups. By trying to fix this problem, I found 2 things.
1. Lacking ";" before the new commands, causing this problem.
2. The standardized latent variable variances would always be 1.

The model fit is fine, but the chi2 difference test would be significant (2 df more, but more than 100 chi2 increase).

Chi-Square Test of Model Fit

          Value                            253.025
          Degrees of Freedom                    66
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               138.316
          CHINA                            114.709

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.101
          90 Percent C.I.                    0.088  0.115
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.942
          TLI                                0.936

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3274.225
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.204

#### step 6_2 factor covariances(Given equality of the factor variances, this test evaluates equality of the factor correlations)
It is said that this test is only meaningful if the loadings and the factor variances are invariant (c10 p23). Since Factor Variances are not equal, showed in the previous step 6_1, this step is not nececerry, just try (and write the model to be used in the future). 

Interstingly, constrain this correlation does not worsen the model fit.
Chi-Square Test of Model Fit

          Value                            253.714
          Degrees of Freedom                    67
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               138.812
          CHINA                            114.902

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.101
          90 Percent C.I.                    0.088  0.114
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.942
          TLI                                0.937

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3274.225
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.202
          


# RQ3 part 2 MG-SEM (using multiple groups modeling on hybrid models; class 11 after p11)

MG-SEM involves all the measurement invariance steps used in MG-CFA as a part of evaluating the measurement model.

The only difference is that the measurement model includes the observed structural variables as well (we correlate all of our factors and observed structural variables just like in our normal hybrid model testing steps).

In the previous MG-CFA steps I did not include the observed structual variables. This time I will include sec and rela_sta (do not sure if I should include this)

## test for measurement part

### Step 1: Unconstrained Common Model (Configural Model)

#### With rela_sta (has warning) 

THE STANDARD ERRORS OF THE MODEL PARAMETER ESTIMATES MAY NOT BE
     TRUSTWORTHY FOR SOME PARAMETERS DUE TO A NON-POSITIVE DEFINITE
     FIRST-ORDER DERIVATIVE PRODUCT MATRIX.  THIS MAY BE DUE TO THE STARTING
     VALUES BUT MAY ALSO BE AN INDICATION OF MODEL NONIDENTIFICATION.  THE
     CONDITION NUMBER IS       0.168D-13.  PROBLEM INVOLVING THE FOLLOWING PARAMETER:
     Parameter 62, Group CHINA: [ RRS ]

     THIS IS MOST LIKELY DUE TO VARIABLE RELA_STA BEING DICHOTOMOUS BUT
     DECLARED AS CONTINUOUS. )

Knid of not sure how to caculatethe df here, check class 4, p10 again.

Chi-Square Test of Model Fit

          Value                            190.460
          Degrees of Freedom                    80 (66-4-4*3/2-9-7)*2
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               107.975
          CHINA                             82.485

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.071
          90 Percent C.I.                    0.058  0.084
          Probability RMSEA <= .05           0.005

CFI/TLI

          CFI                                0.970
          TLI                                0.958

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3767.969
          Degrees of Freedom                   110
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)
          Value                              0.037
#### Without relat_sta
Chi-Square Test of Model Fit

          Value                            155.897
          Degrees of Freedom                    66 (55-3-3*2/2-9-7)*2
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                81.604
          CHINA                             74.293

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.070
          90 Percent C.I.                    0.056  0.085
          Probability RMSEA <= .05           0.011

CFI/TLI

          CFI                                0.974
          TLI                                0.964

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.037
          
### Step 2: Invariance of Factor Loadings: Metric Model
Since there are warning that the estimated parameters may not be trusted when include rela_sta, I decide not to include it from this step.

Chi-Square Test of Model Fit

          Value                            162.492
          Degrees of Freedom                    73 (free 7 loadings)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                83.898
          CHINA                             78.593

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.067
          90 Percent C.I.                    0.053  0.081
          Probability RMSEA <= .05           0.024

CFI/TLI

          CFI                                0.974
          TLI                                0.968

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.041
          

###  Step 3: Equality of Indicator Intercepts: Scalar model
Chi-Square Test of Model Fit

          Value                            191.687
          Degrees of Freedom                    80 (free 7 means)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                93.885
          CHINA                             97.802

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.071
          90 Percent C.I.                    0.058  0.084
          Probability RMSEA <= .05           0.004

CFI/TLI

          CFI                                0.968
          TLI                                0.964

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.047
          
### Step 3 partial
In fact, constain all means almost did not worsen the model fit, just a little bit chi square higher. Any way, try to free R5 first (higher standardized residual for china), chi2 173.206. Then try to free R2 (higher raw and normalized residual for china; higher everything for us), chi2 177.161. To be honest, I do not understand why R5 impact more. Free both, leading to 166.697 (comapred to 162.492 in step 2). I would keep the final one (free both).

Chi-Square Test of Model Fit

          Value                            166.697
          Degrees of Freedom                    78
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                87.188
          CHINA                             79.509

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.064
          90 Percent C.I.                    0.051  0.078
          Probability RMSEA <= .05           0.042

CFI/TLI

          CFI                                0.974
          TLI                                0.970

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.043
### Step 5 latent means
Free 2 latent means, chi2 to 562.159. Not good.

## test for MG Hybrid Models
### step 1: Just ID Structural/Hybrid Model: no constraints
Start from the step 3 partial model.
#### without covariates
df=78 (the same)

It seems like do not include rela_sta and gender exclude the significant impact of the direct effect of PCS on RRS.
standardized for us
RRS      ON
    PCS                0.012      0.047      0.254      0.800

 RRS      ON
    SEC                0.650      0.035     18.492      0.000

 SEC      ON
    PCS                0.267      0.051      5.206      0.000

standardized for china
RRS      ON
    PCS                0.130      0.071      1.831      0.067

 RRS      ON
    SEC                0.479      0.061      7.861      0.000

 SEC      ON
    PCS                0.178      0.073      2.439      0.015
#### with covariates
for us
RRS      ON
    PCS                0.103      0.043      2.378      0.017

 RRS      ON
    SEC                0.486      0.041     11.741      0.000
    RELA_STA           0.399      0.042      9.431      0.000
    GENDER_2          -0.085      0.040     -2.137      0.033

 SEC      ON
    PCS                0.266      0.051      5.190      0.000
    
for china
RRS      ON
    PCS                0.179      0.065      2.740      0.006

 RRS      ON
    SEC                0.334      0.065      5.105      0.000
    RELA_STA           0.403      0.063      6.409      0.000
    GENDER_2          -0.041      0.062     -0.654      0.513

 SEC      ON
    PCS                0.180      0.073      2.470      0.014
    
Add covariates would raise warnings,no matter it's adding one, two or three covariates. Also, the catigorical variable command do not fit here, many warnings (said only work when it's dependent variable).

### step 2:Just ID Structural/Hybrid Model: constrain deleted paths to be equal in each group
df=79. 1 df more, less tahn 3.84 chi2 increase.

Chi-Square Test of Model Fit

          Value                            167.510
          Degrees of Freedom                    79
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                87.688
          CHINA                             79.822

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.064
          90 Percent C.I.                    0.050  0.077
          Probability RMSEA <= .05           0.046

CFI/TLI

          CFI                                0.974
          TLI                                0.971

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.045
          
### step 3:Trim constrained non-significant deleted paths from BOTH groups
1 df more, less than 3.84 chi2 increase.

Chi-Square Test of Model Fit

          Value                            170.041
          Degrees of Freedom                    80
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                87.233
          CHINA                             82.808

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.064
          90 Percent C.I.                    0.051  0.077
          Probability RMSEA <= .05           0.044

CFI/TLI

          CFI                                0.974
          TLI                                0.971

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.049
### step 4:Unconstrained Conceptual Model (with any additional paths after steps 1-3): no constraints on conceptual paths
The same as step 3.

### step 5:Constrained Conceptual Model (with any additional paths after steps 1-3): constrain conceptual paths to be equal in each group.
2 df more, with more than 40 chi2 increase.
Chi-Square Test of Model Fit

          Value                            213.325
          Degrees of Freedom                    82
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               111.024
          CHINA                            102.301

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.076
          90 Percent C.I.                    0.064  0.089
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.962
          TLI                                0.958

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.120


### step 6:Explore partial invariance, if necessary.
By checking the MI in step 5 model, I found the RRS ON sec has a high MI. Then I free it.
Compared to step 4 model, this model is 1 df more, less than 3.84 chi2 increase. Meaning, the path from PCS to sec can be constrained to equal, the path from sec to RRS can not.
Chi-Square Test of Model Fit

          Value                            171.506
          Degrees of Freedom                    81
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                87.804
          CHINA                             83.702

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.064
          90 Percent C.I.                    0.050  0.077
          Probability RMSEA <= .05           0.045

CFI/TLI

          CFI                                0.974
          TLI                                0.971

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.049
### step 7: constrains means and intercepts to be equal across groups (NOTE: must constrain to latent variable means/intercepts to 0; constrain observed variable means to be equal)
### all:PCS, RRS, sec
Chi-Square Test of Model Fit

          Value                            807.283
          Degrees of Freedom                    84
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               161.045
          CHINA                            646.238

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.177
          90 Percent C.I.                    0.166  0.188
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.790
          TLI                                0.775

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3534.042
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.951
       

### keep free PCS (only constrain sec)
chi2: 353.59

### only constrain PCS
chi 543.968 df=82

### only constrain RRS
chi 243

Meaning, no one can be constained to be euqal.

## sum up
Only one path can be constrained to be equal.
