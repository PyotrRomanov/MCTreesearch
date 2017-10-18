# MCTreesearch
Thus far, three Random Number Generators have been tested. The tools with which this has been done and the results can be found in the files of this repo. These three generators are: The generic C# Random class, the C# System.Security.Cryptography.RandomNumberGenerator class and the "true random number service" random.org. 

Especially relevant are the results of the Kolmogorov-Smirnov tests done on all three datasets to compute their similarity to uniform distributions. Considering we are looking for random sets of a uniform distribution, a p value approaching 1 would indicate a higher chance of actually being random. The results are as follows:

C# Random: p = 0.2336

C# Cryptographically Secure: p = 0.4002

Random.org: p = 0.665
