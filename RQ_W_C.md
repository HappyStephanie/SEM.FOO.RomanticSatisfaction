# 1. RQ1 for China
Use Chinese sample as the comparison part to US sample to answer RQ3. To be convenient, I changed the data file (copied from mplus data, created on 7/9) name from C_ssea.data to ssea.data (do not need to change things in the inp files).

Here only include brief steps. Could check the file for us for details.

## 1.1. test the hybrid model with all three predictors and all covariates (class4 p16)
### 1.1.1. Step A: check if the measuement model consistent with the data & Step B: Revise the measurement model
Directly choose the final measurement model that correlate M1-F1, M2-F2, etc. df=536. 

Note, this is with the catigorical command (estimator is WLSMV)

The results looks similar to the US sample.
Chi-Square Test of Model Fit

          Value                            599.264*
          Degrees of Freedom                   536
          P-Value                           0.0300
RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.024
          90 Percent C.I.                    0.008  0.034
          Probability RMSEA <= .05           1.000

CFI/TLI

          CFI                                0.928
          TLI                                0.916

Chi-Square Test of Model Fit for the Baseline Model

          Value                           1511.302
          Degrees of Freedom                   630
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.051

### 1.1.2. StepC: Evaluate deleted paths
Looks similar to US. The chi2 is less (752 vs 1002), but it might due to the sample size difference.

Chi-Square Test of Model Fit

          Value                            752.216
          Degrees of Freedom                   536
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.045
          90 Percent C.I.                    0.037  0.052
          Probability RMSEA <= .05           0.875

CFI/TLI

          CFI                                0.949
          TLI                                0.942

Chi-Square Test of Model Fit for the Baseline Model

          Value                           4843.550
          Degrees of Freedom                   609
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.050

There are 9 significant correlations. Change the int file accordingly.

PCS      WITH
    PSF                0.534      0.076      7.010      0.000
    PSM                0.557      0.077      7.229      0.000
    
 PSF      WITH
    PSM                0.538      0.079      6.795      0.000


 RELA_STA WITH
    DURATION           0.136      0.036      3.752      0.000
    GENDER_3          -0.012      0.006     -1.990      0.047

 AGE      WITH
    DURATION           0.274      0.073      3.752      0.000

 SES      WITH
    GENDER_3           0.031      0.012      2.530      0.011

 DURATION WITH
    GENDER_2           0.098      0.036      2.752      0.006

 GENDER_2 WITH
    GENDER_3          -0.017      0.006     -2.818      0.005

### 1.1.3. StepD:Test of the Specified Paths and Correlations

I add 9 correlations from step c (or maybe 6, because the correlations between PCS, PSF and PSM should not be considered deleted ones, they are in conseptual model). Now the df is 570+11-9=572 (found problems of my writen model based on this caculation).

An interesting thing is that the SES is significantly correlated to PCS, PSF and PSM in US sample, but does not in this sample.

Chi-Square Test of Model Fit

          Value                            776.685
          Degrees of Freedom                   572
          P-Value                           0.0000

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.042
          90 Percent C.I.                    0.034  0.049
          Probability RMSEA <= .05           0.961

CFI/TLI

          CFI                                0.952
          TLI                                0.949

Chi-Square Test of Model Fit for the Baseline Model

          Value                           4843.550
          Degrees of Freedom                   609
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.054

#### 1.1.3.1. Standardized coeeficients
RRS      ON
    PCS                0.254      0.105      2.434      0.015
    PSF               -0.101      0.120     -0.838      0.402
    PSM                0.102      0.133      0.770      0.441
RRS      ON
    RELA_STA           1.327      0.181      7.336      0.000
    AGE                0.013      0.088      0.148      0.882
    SES                0.083      0.086      0.968      0.333
    DURATION           0.163      0.093      1.758      0.079
    COVID             -0.549      0.222     -2.474      0.013
    GENDER_2          -0.150      0.177     -0.844      0.398
    GENDER_3          -0.718      0.516     -1.393      0.164

PCS, RELA_STA and covid could be kept, the other paths should be deleted in the final model.

#### 1.1.3.2. R2
0.392

## 1.2. test the hybrid model with only PCS, RELA_STA and covid (need to change the US model)

### 1.2.1. Step A measurement model
The same to the US, model fit is fine. df=40

### 1.2.2. Step C deleted paths
None of the correlations should be kept.

### 1.2.3. Step D (conceptual) & E (trimmed) are the same
Chi-Square Test of Model Fit

          Value                             70.998
          Degrees of Freedom                    43
          P-Value                           0.0046

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.057
          90 Percent C.I.                    0.032  0.080
          Probability RMSEA <= .05           0.296

CFI/TLI

          CFI                                0.976
          TLI                                0.970

Chi-Square Test of Model Fit for the Baseline Model

          Value                           1209.885
          Degrees of Freedom                    54
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.044

#### 1.2.3.1. STDYX Standardization
RRS      ON
    PCS                0.269      0.062      4.334      0.000

 RRS      ON
    RELA_STA           0.523      0.054      9.700      0.000
    COVID             -0.163      0.061     -2.650      0.008

#### 1.2.3.2. R-SQUARE
0.373

## 1.3. Should I keep both covariates?

### 1.3.1. model with only rela_sta
Similar to the US sample.

Chi-Square Test of Model Fit

          Value                             69.479
          Degrees of Freedom                    34
          P-Value                           0.0003

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.072
          90 Percent C.I.                    0.048  0.096
          Probability RMSEA <= .05           0.067

CFI/TLI

          CFI                                0.969
          TLI                                0.959

Chi-Square Test of Model Fit for the Baseline Model

          Value                           1201.610
          Degrees of Freedom                    45
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.046

#### 1.3.1.1. STDYX Standardization
RRS      ON
    PCS                0.262      0.063      4.135      0.000

 RRS      ON
    RELA_STA           0.526      0.054      9.655      0.000
#### 1.3.1.2. R-SQUARE
0.345

### 1.3.2. model without covariates
Chi-Square Test of Model Fit

          Value                             62.076
          Degrees of Freedom                    26
          P-Value                           0.0001

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.083
          90 Percent C.I.                    0.057  0.110
          Probability RMSEA <= .05           0.022

CFI/TLI

          CFI                                0.967
          TLI                                0.955

Chi-Square Test of Model Fit for the Baseline Model

          Value                           1134.797
          Degrees of Freedom                    36
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.044

#### 1.3.2.1. STDYX Standardization

#### 1.3.2.2. R-SQUARE
RRS      ON
    PCS                0.245      0.073      3.328      0.001

#### 1.3.2.3. R-SQUARE
0.060

Model fit are all fine. R2 changed significantly. Coefficient changed. Similar to the US.

## 1.4. moderation
Need to change the model, from gender to covid.

Still, no moderating effect.

    PCSXRELA_S        -0.096      0.213     -0.450      0.652
    PCSXCOVID          0.109      0.253      0.432      0.665

## 1.5. is using means ok compared to latent variables?
### 1.5.1. Model with 2 covariates (RRS is latent)
The model fit is very good.

Chi-Square Test of Model Fit

          Value                             17.874
          Degrees of Freedom                    20
          P-Value                           0.5957

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.000
          90 Percent C.I.                    0.000  0.054
          Probability RMSEA <= .05           0.932

CFI/TLI

          CFI                                1.000
          TLI                                1.006

Chi-Square Test of Model Fit for the Baseline Model

          Value                            491.031
          Degrees of Freedom                    25
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.030

#### 1.5.1.1. STDYX Standardization
RS      ON
    PCS                0.242      0.061      3.974      0.000
    RELA_STA           0.528      0.054      9.808      0.000
    COVID             -0.162      0.062     -2.618      0.009

#### 1.5.1.2. R-SQUARE
0.363 (still ok, compared to the latent one, 0.373)

Although this is a ok model, since the US used the latent one, China should be consistant. May not need to mention this difference, since it's not help much with interpretation.

### 1.5.2. Model with 1 covariate:rela_sta (RRS is also mean in this model.) 

The model fit is not good: 90 percent CI over 0.1.

Chi-Square Test of Model Fit

          Value                              0.663
          Degrees of Freedom                     1
          P-Value                           0.4156

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.000
          90 Percent C.I.                    0.000  0.173
          Probability RMSEA <= .05           0.522

CFI/TLI

          CFI                                1.000
          TLI                                1.010

Chi-Square Test of Model Fit for the Baseline Model

          Value                             70.332
          Degrees of Freedom                     2
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.024

#### 1.5.2.1. STDYX Standardization
RRS      ON
    PCS                0.236      0.057      4.105      0.000
    RELA_STA           0.499      0.051      9.754      0.000

#### 1.5.2.2. R-SQUARE
0.305

To sum up, the results are pretty similar to the US sample, just the covariate change from gender_2 to covid, to further compare, I think it's better to use the MG-CFA and MG-SEM

# 2. RQ 2 for China
## 2.1. Step A & B measurement model

Chi-Square Test of Model Fit

          Value                             89.116
          Degrees of Freedom                    47
          P-Value                           0.0002

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.067
          90 Percent C.I.                    0.045  0.088
          Probability RMSEA <= .05           0.095

CFI/TLI

          CFI                                0.965
          TLI                                0.951

Chi-Square Test of Model Fit for the Baseline Model

          Value                           1285.363
          Degrees of Freedom                    66
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.042

## 2.2. Step C deleted paths
The df is right.

The deleted path PCS to RRS is also significant. Like the US, there is relationship between sec and rela_sta. Not like US, there is no relationship between rela_sta and the other covariate (which makes sense).

RRS      ON
    PCS                0.206      0.062      3.336      0.001

 RRS      ON
    SEC                0.321      0.062      5.150      0.000
    RELA_STA           0.418      0.059      7.037      0.000
    COVID             -0.168      0.058     -2.875      0.004

 SEC      ON
    PCS                0.188      0.071      2.647      0.008

 PCS      WITH
    RELA_STA          -0.035      0.072     -0.479      0.632
    COVID              0.049      0.072      0.683      0.494

 SEC      WITH
    RELA_STA           0.349      0.062      5.605      0.000
    COVID              0.007      0.071      0.095      0.925

 RELA_STA WITH
    COVID             -0.011      0.071     -0.155      0.877

R2=0.454

## 2.3. Step D specified paths (no need to trim, no step e)
### 2.3.1. Keep the 1 path and 1 correlations from step3 (final one. although did not try the other options, as did the US). 
Chi-Square Test of Model Fit

          Value                             89.851
          Degrees of Freedom                    51
          P-Value                           0.0006

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.062
          90 Percent C.I.                    0.040  0.082
          Probability RMSEA <= .05           0.175

CFI/TLI

          CFI                                0.968
          TLI                                0.959

Chi-Square Test of Model Fit for the Baseline Model

          Value                           1285.339
          Degrees of Freedom                    65
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.046
#### 2.3.1.1. STDYX Standardization
RRS      ON
    PCS                0.205      0.061      3.361      0.001

 RRS      ON
    SEC                0.320      0.062      5.155      0.000
    RELA_STA           0.415      0.059      7.068      0.000
    COVID             -0.166      0.058     -2.873      0.004

 SEC      ON
    PCS                0.198      0.067      2.981      0.003
####
R2=0.461

 Lower .5%  Lower 2.5%    Lower 5%    Estimate    Upper 5%  Upper 2.5%   Upper .5%

Effects from PCS to RRS

## 2.4. bootstrap
The model fit keeps the same with the final model (df=51).



                    Lower .5%  Lower 2.5%    Lower 5%    Estimate    Upper 5%  Upper 2.5%   Upper .5%

Effects from PCS to RRS

  Total              0.125       0.196       0.229       0.387       0.566       0.593       0.638
  Total indirect     0.011       0.029       0.038       0.091       0.173       0.191       0.226

  Specific indirect 1
    RRS
    SEC
    PCS              0.011       0.029       0.038       0.091       0.173       0.191       0.226

  Direct
    RRS
    PCS              0.038       0.109       0.139       0.296       0.467       0.497       0.539

To sum up, there are minor differences in the model, but still very similar. However the indirect effec caculated by bootstrap is much less (0.091 vs 0.233).

# 3. RQ3 part 1 (RQ1 related)
I decide to rewrite the RQ3 part.

## 3.1. measurement invariance
Only indicators of PCS & RRS, no covariate
### 3.1.1. Step 1: Unconstrained Common Model (Configural Model)

Chi-Square Test of Model Fit

          Value                            139.811 (the same to RRS scaled)
          Degrees of Freedom                    52 (remember, knowns or unknowns need to *2)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                77.735
          CHINA                             62.076

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.078
          90 Percent C.I.                    0.062  0.093
          Probability RMSEA <= .05           0.002

CFI/TLI

          CFI                                0.973
          TLI                                0.963

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.034

### 3.1.2. Step 2 constrain factor loadings- Metric model
Compared to model of step 1, not significant. (the critical value for df=7 is 14.07, greater than the difference 8.69)

Chi-Square Test of Model Fit

          Value                            148.486 (the RRS scaled one is 148.707; the unscaled one is 152.292)
          Degrees of Freedom                    59
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                80.480
          CHINA                             68.006

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.074
          90 Percent C.I.                    0.059  0.088
          Probability RMSEA <= .05           0.005

CFI/TLI

          CFI                                0.973
          TLI                                0.966

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.042

### 3.1.3. Step 3 constrain intercepts-Scalar model
Compared to model of step 2, significant. (the critical value for df=7 is 14.07, less than the difference 25)

Chi-Square Test of Model Fit

          Value                            173.509 (the RRS scaled one is 148.732)
          Degrees of Freedom                    66
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                88.230
          CHINA                             85.279

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.076
          90 Percent C.I.                    0.062  0.090
          Probability RMSEA <= .05           0.001

CFI/TLI

          CFI                                0.967
          TLI                                0.964

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.049

### 3.1.4. step 3 partial (intercept)
Compared to model of step 2, not significant. (the critical value for df=6 is 12.59, greater than the difference 11.47).

Although it might be even better if I also free R4 and R5. But since the model fit is fine and only free one is easier to interpret, I would keep it this way.

Chi-Square Test of Model Fit

          Value                            159.951
          Degrees of Freedom                    65
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                84.399
          CHINA                             75.552

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.072
          90 Percent C.I.                    0.058  0.086
          Probability RMSEA <= .05           0.006

CFI/TLI

          CFI                                0.971
          TLI                                0.968

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.045

### 3.1.5. Step 4: Equality of residual variances (and covariances)
Free 7 df (after free S1 S2), with 89 chi2 increase, way more than 14. I checked the M.I. residual variances, it suggests to free R1,R2,R4,S3 (I tried, still significant). I think it might be too much, we could just say they do not have the same residual variances, and so the reliability.


Chi-Square Test of Model Fit

          Value                            239.168
          Degrees of Freedom                    72
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               119.111
          CHINA                            120.057

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.091
          90 Percent C.I.                    0.078  0.104
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.949
          TLI                                0.949

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.077

### 3.1.6. Step 5:  Equality of Factor (structural) means
Compared to step 3 partial: 160, df65. The first model has 2 df more, but 21 chi2 more. 

Then, I tried to free RRS (based on MI), the chi2 keeps the same (increase 0.001) to step 3 partial,and has one more df. Meaning, PCS can be considered to be equal, while RRS is not.

#### 3.1.6.1. constrain two means
Chi-Square Test of Model Fit

          Value                            181.766 (the scaled one is 148.733)
          Degrees of Freedom                    67
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                91.413
          CHINA                             90.353

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.078
          90 Percent C.I.                    0.065  0.092
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.965
          TLI                                0.962

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.065

#### 3.1.6.2. only constrain PCS
Chi-Square Test of Model Fit

          Value                            159.952
          Degrees of Freedom                    66
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                84.400
          CHINA                             75.552

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.071
          90 Percent C.I.                    0.057  0.085
          Probability RMSEA <= .05           0.007

CFI/TLI

          CFI                                0.971
          TLI                                0.969

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.045

### 3.1.7. Step 6:  Invariance of Factor Variances and Covariances (Steps 5 & 6 are interchangeable in terms of order)
Since it's said that step 5 and 6 can change order, I will just use the model of step 3 partial 

It seems like they have same variances and same covariances. TOO GOOD. NEED TO CHECK LATER.

Checking: df is right;variances are different in step 1, but similar, so it's fine (not like they are somehow both be fixed to 1).


#### 3.1.7.1. step 6_1 Factor Variances
Chi-Square Test of Model Fit

          Value                            160.239
          Degrees of Freedom                    67 (65+2,65 is from step 3 p, not step 5)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                84.565
          CHINA                             75.674

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.070
          90 Percent C.I.                    0.057  0.084
          Probability RMSEA <= .05           0.009

CFI/TLI

          CFI                                0.971
          TLI                                0.969

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.046


#### 3.1.7.2. step 6_2 factor covariances(Given equality of the factor variances, this test evaluates equality of the factor correlations)
Chi-Square Test of Model Fit

          Value                            160.664
          Degrees of Freedom                    68
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                84.694
          CHINA                             75.971

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.070
          90 Percent C.I.                    0.056  0.084
          Probability RMSEA <= .05           0.011

CFI/TLI

          CFI                                0.972
          TLI                                0.970

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.047

## 3.2. MG-SEM for RQ1, no covariates
### 3.2.1. step 1: Just ID Structural/Hybrid Model: no constraints (for paths. here there is only one path, so it equals to step 4)
I could use the the model that step 3 partial + step 5 and step 6. The df of step 3 p is 65, constarin one mean +1. constrain 2 variance +2, since there is no covariance, df=68 is right. chi2 is 160.393 (change to 150.601 when RRS is scaled, change to 150.603 when R2 and RRS are constrained).

Check: all loadings are constrained, factor PCS and RRS (in the residual variances) variances are constrained, the only path is free, intercept R2 is free, mean PCS is constrained, mean RRS is free.

Since there is only one path, no deleted path (therefore do not need step 2), no need to trim (therefore no step 3).

### 3.2.2. step 5:Constrained Conceptual Model: constrain conceptual paths to be equal in each group.
chi2 did not increase much (change to 150.740 when RRS is scaled and R2 and RRS are constrained). Meaning the path is equal across two groups.

Chi-Square Test of Model Fit

          Value                            160.665
          Degrees of Freedom                    69
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                84.693
          CHINA                             75.972

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.069
          90 Percent C.I.                    0.055  0.083
          Probability RMSEA <= .05           0.014

CFI/TLI

          CFI                                0.972
          TLI                                0.971

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3327.000
          Degrees of Freedom                    72
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.047

Still, only one path, no need to explore partial invariance (no step 6 needed).

### 3.2.3. step 7: constrains means and intercepts to be equal across groups (NOTE: must constrain to latent variable means/intercepts to 0; constrain observed variable means to be equal)

I am not quite understand here: I have constrain factor means in measurement model, how could I do it again here? The new added observed variables could be constrained here. In this step, there is no new added observed variable. 

## 3.3. MG-SEM for RQ1, with covariates, all three
Based on step 3 partial model in the MG CFA section.

### 3.3.1. step 1: Just ID Structural/Hybrid Model: no constraints
Has warnings.

Since it has warnings, I decide directly go to the step 5: it still has warnings. Therefore, give up comparing with covariates (the same when the RRS is scaled).


# 4. RQ3 part 2 (RQ2 related)
## 4.1. measurement model
The same to RQ3 part 1.

## 4.2. MG-SEM without covariates

### 4.2.1. step 1: Just ID Structural/Hybrid Model: no constraints (there is no deleted path, so it equals to step 4)
Since include covariates would raise warning message, I would just test the mediation model without covariates.

Chi-Square Test of Model Fit

          Value                            183.583
          Degrees of Freedom                    82(CHECKED:55*2+mean structure knowns-count estimated parameters, remember to note the factor mean when count)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                88.355
          CHINA                             95.227

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.066
          90 Percent C.I.                    0.054  0.079
          Probability RMSEA <= .05           0.019

CFI/TLI

          CFI                                0.971
          TLI                                0.968

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3589.856
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.047

### 4.2.2. step 5:Constrained Conceptual Model: constrain conceptual paths to be equal in each group.

It increase 3 df, with 8.296 more chi2. The critical value for df=3 is 7.815. Therefore it's significant. So go to step 6. 

Chi-Square Test of Model Fit

          Value                            191.879
          Degrees of Freedom                    85
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                91.566
          CHINA                            100.313

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.067
          90 Percent C.I.                    0.054  0.080
          Probability RMSEA <= .05           0.015

CFI/TLI

          CFI                                0.969
          TLI                                0.968

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3589.856
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.048

### 4.2.3. step 6:Explore partial invariance, if necessary.
Check the MI in step 5, decide to free RRS on sec.

2 df increase than step 1, with 3.924 more chi2,. The critical value is 5.991, so this model is fine. Meaning, only the path from sec to RRS is different between these two groups.

Chi-Square Test of Model Fit

          Value                            187.507
          Degrees of Freedom                    84
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                89.818
          CHINA                             97.689

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.066
          90 Percent C.I.                    0.054  0.079
          Probability RMSEA <= .05           0.019

CFI/TLI

          CFI                                0.970
          TLI                                0.968

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3589.856
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.051


### 4.2.4. step 7: constrains means and intercepts to be equal across groups
I just need to constrain sec in this step.

It's ok to constain sec.

For testing, I constain RRS, chi2 become 218.241, not ok.

Also, I test if adding covariates are fine, strangely, it works this time. Therefore, I decide to do MG-SEM with covariates.

Chi-Square Test of Model Fit

          Value                            187.508
          Degrees of Freedom                    85
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                                89.819
          CHINA                             97.689

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.066
          90 Percent C.I.                    0.053  0.078
          Probability RMSEA <= .05           0.023

CFI/TLI

          CFI                                0.971
          TLI                                0.969

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3589.856
          Degrees of Freedom                    90
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.051


## 4.3. MG-SEM with all covariates
From this section, all paths except the covid to RRS path, are equal. the mean of sec is equal.

### 4.3.1. step 1: Just ID Structural/Hybrid Model: no constraints
Chi-Square Test of Model Fit

          Value                            268.881
          Degrees of Freedom                   124 (checked. took a long time: caculate as 124, but the model shows 128, turns out that I forgot to free the observed structuarl variable means. Interstingly, it does not require this when sec is the only ovserved structuarl variable. )
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               156.111
          CHINA                            112.770

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.065
          90 Percent C.I.                    0.054  0.075
          Probability RMSEA <= .05           0.013

CFI/TLI

          CFI                                0.961
          TLI                                0.953

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.041


### 4.3.2. step 2:Just ID Structural/Hybrid Model: constrain deleted paths to be equal in each group
I constrain 8 correlations. The chi2 increase 5.626, must not significant.

Chi-Square Test of Model Fit

          Value                            274.507
          Degrees of Freedom                   132
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               157.383
          CHINA                            117.124

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.062
          90 Percent C.I.                    0.052  0.072
          Probability RMSEA <= .05           0.029

CFI/TLI

          CFI                                0.962
          TLI                                0.957

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.043


### 4.3.3. step 3:Trim constrained non-significant deleted paths from BOTH groups
In the 8 constained correlations, only 1 is significant: rela with gender. Trim the rest.

7 more df, 9.765 more chi2,<14.067, not significant.

Chi-Square Test of Model Fit

          Value                            284.272
          Degrees of Freedom                   139
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               166.308
          CHINA                            117.964

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.061
          90 Percent C.I.                    0.051  0.071
          Probability RMSEA <= .05           0.038

CFI/TLI

          CFI                                0.961
          TLI                                0.958

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.054

### 4.3.4. step 4:Unconstrained Conceptual Model (with any additional paths after steps 1-3): no constraints on conceptual paths
#### 4.3.4.1. question
Emmm, the model is the same as step 3. In any situation will it be different? if so, why need this step. Maybe there are some deleted paths that could not be constained? Even so, they would be kept and step 3 is still the same to step 4.

### 4.3.5. step 5:Constrained Conceptual Model
6 more df, 13.366 more chi2, the critical value is 12.592, significant.
Chi-Square Test of Model Fit

          Value                            297.638
          Degrees of Freedom                   145
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               173.280
          CHINA                            124.358

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.061
          90 Percent C.I.                    0.051  0.071
          Probability RMSEA <= .05           0.032

CFI/TLI

          CFI                                0.959
          TLI                                0.958

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.055


### 4.3.6. step 6:Explore partial invariance, if necessary.
Free RRS ON covid.

1 less df than step 5. 5 more df than step 3, 9.131 more chi2, critical value is 11.07, not significant.

Chi-Square Test of Model Fit

          Value                            293.403
          Degrees of Freedom                   144
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               169.683
          CHINA                            123.720

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.061
          90 Percent C.I.                    0.051  0.071
          Probability RMSEA <= .05           0.038

CFI/TLI

          CFI                                0.960
          TLI                                0.959

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.055


### 4.3.7. step 7: constrains means and intercepts to be equal across groups
I've tried factor means in the MG CFA steps. Now I would just try the observed ones.

Chi-Square Test of Model Fit

          Value                            348.549
          Degrees of Freedom                   148
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               177.468
          CHINA                            171.080

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.070
          90 Percent C.I.                    0.060  0.079
          Probability RMSEA <= .05           0.000

CFI/TLI

          CFI                                0.947
          TLI                                0.946

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.063

### 4.3.8. step 8 explore partial invariance in the mean structrue
#### 4.3.8.1. free covid and gender
Chi-Square Test of Model Fit

          Value                            302.257
          Degrees of Freedom                   146
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               172.291
          CHINA                            129.966

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.062
          90 Percent C.I.                    0.052  0.072
          Probability RMSEA <= .05           0.026

CFI/TLI

          CFI                                0.958
          TLI                                0.957

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.055

#### 4.3.8.2. keep on free rela_sta
1 more df, similar chi2.

Chi-Square Test of Model Fit

          Value                            293.404
          Degrees of Freedom                   145
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               169.684
          CHINA                            123.720

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.060
          90 Percent C.I.                    0.050  0.070
          Probability RMSEA <= .05           0.044

CFI/TLI

          CFI                                0.960
          TLI                                0.959

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3902.125
          Degrees of Freedom                   150
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.055


## 4.4. Problems
1. I found only the MG CFA do not include the observed variables, the measurement steps in MG SEM do. I did not do it this way I think, but it does not matter too much, since the model fit in MG-SEM step 1 is fine.
   
   In class 11, p11, said "The only difference is that the measurement model includes the observed structural variables as well (we correlate all of our factors and observed structural variables just like in our normal hybrid model testing steps).'

2. Can I check the mean differences between these two groups? How? Cohen’s d?

# 5. RQ3 part 3
PSF/PSM--sec/pre/dis--RRS

I plan to only include rela_sta as the covariate.

## 5.1. MG CFA
I plan to include PSM ,PSF, and RRS. The model fit is not good.

Then I try to include PSM and PSF seperately with RRS.

### 5.1.1. PSF & RRS

#### 5.1.1.1. Step 1: Unconstrained Common Model
Chi-Square Test of Model Fit

          Value                            373.854
          Degrees of Freedom                   178 (model fit is fine)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               251.967
          CHINA                            121.887

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.063
          90 Percent C.I.                    0.054  0.072
          Probability RMSEA <= .05           0.011

CFI/TLI

          CFI                                0.962
          TLI                                0.956

Chi-Square Test of Model Fit for the Baseline Model

          Value                           5420.699
          Degrees of Freedom                   210
          P-Value                           0.0000


### 5.1.2. Step 2 constrain factor loadings- Metric model
13 df more,  < 22.362, not sig.

Chi-Square Test of Model Fit

          Value                            388.691
          Degrees of Freedom                   191
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               255.594
          CHINA                            133.097

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.061
          90 Percent C.I.                    0.052  0.069
          Probability RMSEA <= .05           0.022

CFI/TLI

          CFI                                0.962
          TLI                                0.958

Chi-Square Test of Model Fit for the Baseline Model

          Value                           5420.699
          Degrees of Freedom                   210
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.044

### 5.1.3. Step 3 constrain intercepts-Scalar model
13 df more, 25.25 chi2 more > 22.362, sig.

Chi-Square Test of Model Fit

          Value                            413.941
          Degrees of Freedom                   204
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               263.354
          CHINA                            150.587

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.061
          90 Percent C.I.                    0.052  0.069
          Probability RMSEA <= .05           0.020

CFI/TLI

          CFI                                0.960
          TLI                                0.959

Chi-Square Test of Model Fit for the Baseline Model

          Value                           5420.699
          Degrees of Freedom                   210
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.046

### 5.1.4. step 3 partial (intercept)
1 less df than step 3, 12 df moe than step 2, chi2 is 11.725 more <22.362, not sig.

Chi-Square Test of Model Fit

          Value                            400.416
          Degrees of Freedom                   203
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               259.588
          CHINA                            140.828

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.059
          90 Percent C.I.                    0.050  0.067
          Probability RMSEA <= .05           0.044

CFI/TLI

          CFI                                0.962
          TLI                                0.961

Chi-Square Test of Model Fit for the Baseline Model

          Value                           5420.699
          Degrees of Freedom                   210
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.045

### 5.1.5. Step 4: Equality of residual variances (and covariances)
15 df more, chi2 is 159.159 more, 24.996 is the critical value, it is hard to make it non significant by free only a few variances.

### 5.1.6. Step 5:  Equality of Factor (structural) means
2 df more, 21 chi2 more, sig.

#### 5.1.6.1. try to free RRS
1 df more, a little chi2 higher. works

# 6. An important update
**I just curious if scaled RRS would change the results. It did!**

I decide to go back to check. Just in case it cause some differences. 

## 6.1. RQ1 is the same.

## 6.2. RQ2 
The regular part is the same. But for the bootstrap part, the results change, but it is because the previous indirect effect is not a standardized one. After putting the STANDARDIZED commond for the first data (RRS not scaled), the standardardized results are the same to the results of the second data (RRS scaled).

STDYX Standardization

                  Lower .5%  Lower 2.5%    Lower 5%    Estimate   
                   Upper 5%  Upper 2.5%   Upper .5%

Effects from PCS to RRS

  Total              0.097       0.130       0.153       0.251     
                     0.340       0.354       0.391
  
  Total indirect     0.083       0.098       0.105       0.149      
                     0.201       0.210       0.229

  
  Direct
    RRS
    PCS             -0.029       0.004       0.018       0.102    
                   0.179       0.194       0.232

Use Chinese sample to answer Q1, Q2, the results are the same, just the bootstrap need to be changed.



## 6.3. RQ3

### 6.3.1. part 1
The measurement part: all show invariance except for the residual variances

The path part: still equal.

### 6.3.2. part 2
I newly make the measurement part.
#### 6.3.2.1. step 1

It has warning this time!!!

Chi-Square Test of Model Fit

          Value                            249.301
          Degrees of Freedom                   108 (checked)
          P-Value                           0.0000

Chi-Square Contribution From Each Group

          US                               149.724
          CHINA                             99.576

RMSEA (Root Mean Square Error Of Approximation)

          Estimate                           0.068
          90 Percent C.I.                    0.057  0.079
          Probability RMSEA <= .05           0.004

CFI/TLI

          CFI                                0.962
          TLI                                0.946

Chi-Square Test of Model Fit for the Baseline Model

          Value                           3915.930
          Degrees of Freedom                   156
          P-Value                           0.0000

SRMR (Standardized Root Mean Square Residual)

          Value                              0.035

Changes a lot. With the RRS scaled, the mean is not different now. It makes me think through the whole process, I think I should not standardized the variables.In this situation, it is hard to compare the means. I will try the raw data ,and then the min max scale in the new file.

