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

Additionally, folders with all of the graphs that were or weren't used in the paper are available here. The foldernames refer to the C value of the AI that was played against to generate the data, 141 standing for 1.41.

# Analysis in R
Coming soon
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
