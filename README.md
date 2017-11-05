# MCTreesearch
Thus far, three Random Number Generators have been tested. The tools with which this has been done and the results can be found in the files of this repo. These three generators are: The generic C# Random class, the C# System.Security.Cryptography.RandomNumberGenerator class and the "true random number service" random.org. 

Especially relevant are the results of the Kolmogorov-Smirnov tests done on all three datasets to compute their similarity to uniform distributions. Considering we are looking for random sets of a uniform distribution, a p value approaching 1 would indicate a higher chance of actually being random. The results are as follows:

C# Random: p = 0.2336

C# Cryptographically Secure: p = 0.4002

Random.org: p = 0.665

In addition, 2D plots of the random values within a dataset were made to visualize possible patterns that would otherwise not be intuitive. Luckily, none of the three seemed to have particularly clear patterns when ordered this way.
Auto-correlation graphs were also generated using R for all three datasets. All these plots are named after their origin sets, Random, Secure and True.

All these factors lead to the conclusion of Random.org being the best source of random numbers out of the ones tested. However, due to accessing these numbers being slow compared to generating them using the secure generator, the secure generator was chosen to be used in the actual MCTS implementation. Two different remapping functions were used to get the random numbers in the ranges required by the program.

Additionally, folders with all of the graphs that were or weren't used in the paper are available here. The foldernames refer to the C value of the AI that was played against to generate the data, 141 standing for 1.41.
