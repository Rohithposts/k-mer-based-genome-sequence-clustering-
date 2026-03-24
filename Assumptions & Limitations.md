Assumptions and Limitations:

1) This analysis cannot give any biological or evolutionary interpretation that is statistically significant. A significantly larger number of genomes would be required for that. The aim of this particular analysis is to try and understand how genome data comparison metrics and data preprocessing largely affect outputs.	

2) All the sequences used in this analysis were downloaded from NCBI. Therefore, an assumption that there will be no form of “batch effects” was taken given that all the genome sequences are from one source. However, there is a possibility of such “batch effects” occurring.

3) As GC content is a very important biological metric for a sequence, in this analysis “GC Bias” was not accounted for.

4) Some of the sequences are outputs of genome assembly (computational algorithm that joins the k-mers of a sequence by checking similarity of k-1 positions at the start and end of the k-mers). Given the nature of this method of assembly, some ambiguities and variations might exist in these sequences, which may affect clustering.

5) Choosing larger values of k (k = 20+) is computationally expensive and extremely time consuming. Moreover, it becomes difficult to find matches for a k-mer with large lengths

6) To calculate ARI (Adjusted rank index), the dendrogram must be “cutted”. The python function fclutster() carries out this. While fcluster() has many criterion that can be chosen to “cut” the dendrogram, the most common criterion is “maxclust”. Adding other such methods would add many more dimensions to this analysis, which have been skipped. However, the criterion used in fcluster() has a strong influence on the output ARI.

7) Even though this is a comparative methods/metrics analysis, the outputs can change significantly if we use another set of sequences. Therefore, the sequences we consider while doing such analysis also plays an important role in analysis outputs.
