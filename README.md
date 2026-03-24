# k-mer-based-genome-sequence-clustering-
The aim of this analysis is to explore how using various metrics genome data analysis metrics affects ouptut clustering. 

While doing kmer based sequence clustering, it is important to account for various biases in genome sequences taht can vastly manipukate clustering ouptut. While doing k-mer based clustering, we convert the entire sequence into kmers, and based on the counts, or occcurences of the kmer, the output dendrogram will be genrated. The dendrogram shows which sequence is more close to a given sequence compared to others. For doing clustering, we have 3 various types of linkages and 3 variosu distance metrics whcih we can calculate between a set of points from two different clusters.

If we carry out kmer based similarity sequencing using simply raw counts of k-mer appearance, and then we compare it with the output dendrogram under the same conditions(same linkage, same distance metric, same value of k), the difference caused due to biases in length will be evident. A sequence having a larger length will have more "occurences" of a given k-mer than a sequence with a smaller length. Therefore, raw counts has a built in genome "length bias" where the clustering tends to cluster more towards larger genome sequences, even though the shorter sequence(s) may be simialar in composition.

In this project, using quantitative metrics like ARI (adjusted rank index), i try to analyse the changes in output clustering when using raw counts and frequency counts (occurences of a k-mer relative to the length of the sequence).

ARI or adjusted rank index gives a quantitative metric that helps us undertsand how well two dendrograms agree with each other. ARI ranges from 1 to -1. If ARI is 1.0, it meand that the two dendrograms "agree" with each other, and there is no "random" clustering.  ARI values below 0 are worse than "random" clustering and both the dendrograms are "opposite". In python using libraries it can be calculated using libraries like sklearn. 
The three various distance metrics that are calculated duirng clustering are cosine, euclidean and manhattan. 
The three various linkages that are used in k-mer based similairty clustering are average (UPGMA) linkage, single linkage and complete linkage.
Euclidean distance is the square root of the square of the difference between the positions between two points in space. 
Manhattan distance is the sum of absolute value of the raw difference between the two positions of the points.
Cosine distance is 1 - cosine similairity where cosine similarity = (x.y)/(|x||y|).
Single linkage takes the smallest possible value of the distance between a point in a cluster and its counterpart in another cluster/group.
Complete linkage takes the largest possible value of the distance between a point in a cluster and its counterpart in another cluster/group.
Average linkage (UPGMA) takes the average of all distances calculated between each point and its counterpart in the other batch.

In this project, I try to find differecnes between the dendrograms generated using various combinations (3 linkages x 3 distance metrics = 9 dendrograms) for raw counts and frequency counts, using different values for k (k = 4, 5, 10) to generate the k-mers.




