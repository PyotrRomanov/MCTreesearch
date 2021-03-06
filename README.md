# Random Generation
Thus far, three Random Number Generators have been tested. The tools with which this has been done and the results can be found in the files of this repo. These three generators are: The generic C# Random class, the C# System.Security.Cryptography.RandomNumberGenerator class and the "true random number service" random.org. 

Especially relevant are the results of the Kolmogorov-Smirnov tests done on all three datasets to compute their similarity to uniform distributions. Considering we are looking for random sets of a uniform distribution, a p value approaching 1 would indicate a higher chance of actually being random. The results are as follows:

C# Random: p = 0.2336

C# Cryptographically Secure: p = 0.4002

Random.org: p = 0.665

In addition, 2D plots of the random values within a dataset were made to visualize possible patterns that would otherwise not be intuitive. Luckily, none of the three seemed to have particularly clear patterns when ordered this way.
Auto-correlation graphs were also generated using R for all three datasets. All these plots are named after their origin sets, Random, Secure and True.
![plot](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/RandomPlot2dc.png)
Illustrated is the 2D plot of the generic C# random generator's generated values.

All these factors lead to the conclusion of Random.org being the best source of random numbers out of the ones tested. However, due to accessing these numbers being slow compared to generating them using the secure generator, the secure generator was chosen to be used in the actual MCTS implementation. Two different remapping functions were used to get the random numbers in the ranges required by the program.

# Analysis in R
Rough approximation in range 0 <= C < 50 with step size of 1:
![141ro](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/141/141rough.png)
Note that the peak and most contrast are found in the [0,2] range, so this was picked as the focus for the rest of the research.

Fitting of a third degree polynomial onto the data generated by playing games with 0 <= C < 2 with step size is 0.05.
```R
>lm(formula = X30ms141final$rate ~ X30ms141final$c + X30ms141final$c2 + X30ms141final$c3)

Residuals:
   Min     1Q Median     3Q    Max 
-5.444 -1.772  0.221  1.561  4.985 

Coefficients:
                Estimate Std. Error t value Pr(>|t|)    
(Intercept)       32.306      1.404   23.01  < 2e-16 ***
X30ms141final$c   92.347      6.314   14.62  < 2e-16 ***
c2               -96.609      7.580  -12.75 6.56e-15 ***
c3                27.658      2.553   10.83 7.04e-13 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 2.431 on 36 degrees of freedom
Multiple R-squared:  0.8808,	Adjusted R-squared:  0.8709 
F-statistic: 88.71 on 3 and 36 DF,  p-value: < 2.2e-16
```
![141fine](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/141/141.png)

Confidence bounds of the fit on this same data:
```R
      fit             lwr             upr       
 Min.   :32.31   Min.   :29.46   Min.   :35.15  
 1st Qu.:46.82   1st Qu.:45.35   1st Qu.:48.42  
 Median :50.46   Median :48.99   Median :52.55  
 Mean   :50.91   Mean   :49.40   Mean   :52.41  
 3rd Qu.:56.62   3rd Qu.:55.40   3rd Qu.:57.85  
 Max.   :59.11   Max.   :57.77   Max.   :60.47  
 ```
 ![141conf](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/141/141conf.png)
 Prediction bounds:
 ```R
       fit             lwr             upr       
 Min.   :32.31   Min.   :26.61   Min.   :38.00  
 1st Qu.:46.82   1st Qu.:41.67   1st Qu.:52.00  
 Median :50.46   Median :45.22   Median :55.86  
 Mean   :50.91   Mean   :45.74   Mean   :56.08  
 3rd Qu.:56.62   3rd Qu.:51.54   3rd Qu.:61.70  
 Max.   :59.11   Max.   :54.00   Max.   :64.22  
 ```
 ![141pred](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/141/141pred.png)
 
 Fit of a parabola on the rough data in range 2 < c < 50:
 ```R
 
lm(formula = X141roughAdj$rate ~ X141roughAdj$c + X141roughAdj$c2)

Residuals:
    Min      1Q  Median      3Q     Max 
-9.3673 -2.1299 -0.9171  2.2671  8.4555 

Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
(Intercept)     42.434568   2.131335  19.910  < 2e-16 ***
X141roughAdj$c  -1.931816   0.187474 -10.304 2.63e-13 ***
X141roughAdj$c2  0.026303   0.003511   7.491 2.19e-09 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 3.959 on 44 degrees of freedom
Multiple R-squared:  0.8404,	Adjusted R-squared:  0.8331 
F-statistic: 115.8 on 2 and 44 DF,  p-value: < 2.2e-16
```
![141r](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/141/141roughadjline.png)

Confidence bounds:
```R
      fit              lwr              upr        
 Min.   : 6.966   Min.   : 5.403   Min.   : 8.529  
 1st Qu.: 7.913   1st Qu.: 6.072   1st Qu.: 9.709  
 Median :10.579   Median : 8.242   Median :12.955  
 Mean   :14.828   Mean   :12.877   Mean   :16.779  
 3rd Qu.:19.960   3rd Qu.:18.389   3rd Qu.:21.531  
 Max.   :36.876   Max.   :33.528   Max.   :40.224  
 ```
 ![141rconf](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/141/141roughadjconf.png)
 Prediction bounds:
 ```R
 
      fit              lwr               upr       
 Min.   : 6.966   Min.   :-1.1638   Min.   :15.10  
 1st Qu.: 7.913   1st Qu.:-0.2766   1st Qu.:16.10  
 Median :10.579   Median : 2.2769   Median :18.86  
 Mean   :14.828   Mean   : 6.6002   Mean   :23.06  
 3rd Qu.:19.960   3rd Qu.:11.8284   3rd Qu.:28.09  
 ```
 ![141rpred](https://raw.githubusercontent.com/PyotrRomanov/MCTreesearch/master/141/141roughadjpred.png)
 

That's all for the games played against the opponent with C = 1.41. Data for the other opponents can be found in their respective folders on this repository. These folders are simply named after their C values, 0 and 3.
