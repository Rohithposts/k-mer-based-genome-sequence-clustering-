While is it expected that the output dendrogram will change when we take frequency counts instead of raw counts, many other points and interpretations can also be made based on the output dendrograms and ARI. 

1) Across three different values of k (4, 5, 10), the ARI output for cosine distance in the analysis is equal to 1.0 irrespective of the linkage considered (average/single/complete linkage).

Cosine distance is equal to 1 – cosine similarity, Where cosine similarity = (x.y)/(|x||y|) where x and y are two points in space/x-y graph. Cosine distance is largely independent of magnitude but is highly affected by direction. When changing from the raw counts of the k-mer to frequency of k-mer appearance, the largest bias that is addressed is genome length bias (Magnitude). A longer sequence will have a higher occurrence of a given k-mer when compared to a sequence with a smaller length. However, direction changes when the sequences a largely different, that is, when the relative position b/w two points in space/x –y graph change. And that change can happen only when there is a very large and noticeable difference between k-mer composition in the sequences.  



2)  One of the many examples of removing genoem sequence length bias

Across variosu combinations of k, distance metric, linkage and count type e coli str. K-12 and e coli O157:H7 are always clustered together. When converting from raw counts to frequency counts the biggest and main bias that we are removing is length bias. When it comes to these two organisms, the length difference isnt very large. e coli str. K-12 has a length of 46,39,675 nucleotides and e coli O157:H7 has a length of 55,94,605 nucleotides. So, ther isn't much relative difference and both being variants of e coli are expected to cluster togehter frequently. However on the contrary, the human mitochondrion genome, has drastic change in its positioning. In raw counts based dendrogram(euclidean distance, average linkage), mitochondria and mycoplasma pnuemoniae M129 are the first two sequences to be clustered together. Human mitochondria is 16,569 nucleotides long whereas mycoplasma is 8,16,394 nucleotides long. Under same conditions using frequency counts, human mitochondria is grouped farthest away from all the other genomes and mycoplasam pnumoniae M129 is clustered between other genome sequences and far off from human mitochondria. This is one example among many that illustrates removing of length bias.  




3) In every single distance metric and linkage combination, irrespective of k value, among all linkages , the ARIs generated with dendrograms made by single linkage tend to have the closest neagtive value to zero.

Single linkage takes the smallesgt distance among all the distances calculated between each point and its counterpart in the other group. Thus single linkage creates the "chaining effect", where groups of points are closer than they actually are. There could be a possibility where the smallest distance is just a one off case and does not truly reflect the entire group of points. So, by chaining these groups, single linkage tends to remove, atleast upto an extent, the differences casued by taking raw counts and frequency reads to perform dendrograms. By effectively reducing the differences, it generates an ouptut ARI that suggests that the pair of dendrograms agree relatively better when compared to ARIs of other linkages.
