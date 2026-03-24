# k-mer-based-genome-sequence-clustering-
The aim of this analysis is to explore how using various metrics genome data analysis metrics affects ouptut clustering. 

#human_mitochondria = seq1
#e_coli_strain_k-12 = seq2
#mycoplasma_pnuemoniae_M129 = seq3
#saccromyceies serevaisea CEN.PK113-7D = seq4
#e coli 0157:H7 = seq5
#propionibacterium freudenreichii CIRM-BIA1 = seq6
#Nostoc sp. PCC 7120 = seq7
#azatobacter vinelandii CA = seq8

#read and parse the .fasta/.fna file

def read_file(file_path):
    seq = []
    with open(file_path) as f:
        for line in f:
            line = line.strip()
            if not line.startswith('>'):
                seq.append(line)
    return "".join(seq)

seq1 = read_file("D:/project/human_mitochondria_ncbi_NC_012920.1.fasta")
seq2 = read_file("D:/project/E coli str. K-12 substr. MG1655 U00096.2.fasta")
seq3 = read_file("D:/project/mycoplasma_pnuemoniae_M129_U00089.2_NCBI.fasta")
seq4 = read_file("D:/project/sacchromyces cerevasiea CEN.PK113-7D.fna")
seq5 = read_file("D:/project/ecoliO157H7 .fna")
seq6 = read_file("D:/project/propinoiibacterium freudenreichii CIRM-BA1.fna")
seq7 = read_file("D:/project/nostoc_sp_PCC 7120.fna")
seq8 = read_file("D:/project/azatobacter_vinelandii_CA.fna")

sequences = [seq1, seq2, seq3, seq4, seq5, seq6, seq7, seq8]

def kmer_rawcount(seq, k):
    from collections import Counter                          #fucntion for raw counts of a k-mer occurence in a sequence
    kmers = [seq[i:i+k] for i in range(len(seq) - k + 1)]
    counts = Counter(kmers)
    return counts

def kmer_frequency(seq, k):             #function for frequency of occorence of a k-mer in a sequence
    frequency = {}
    counts = kmer_rawcount(seq, k)
    total = sum(counts.values())
    for kmer in counts:
        frequency[kmer] = counts[kmer]/total
    return frequency

#(changed the value of k for the repsective analysis)
raw_counts = [kmer_rawcount(seq, 4) for seq in sequences]           
frequency = [kmer_frequency(seq, 4) for seq in sequences]    #.................................first change

#generating dendrogram
from scipy.spatial.distance import pdist
from scipy.cluster.hierarchy import linkage, dendrogram, fcluster
import matplotlib.pyplot as plt

#pdlist and clustering functions need a matrix data set
import pandas as pd
raw_counts_df = pd.DataFrame(raw_counts).fillna(0)
frequency_counts_df = pd.DataFrame(frequency).fillna(0)

#clustering from raw counts for k = 4, 5       (changed the value of k for the repsective analysis)
#we have 3 distances: euclidean, cosine, manhattan
#we have 3 linkages: average, single, complete
#thus, we have 3x3 = 9 dendrograms
labels = ["mtchn", "ecoli k12", "mycoplasma", "sacchromyces", "ecoli0157H7", "propionibacterium", "nostoc", "azatobacter"] 
from sklearn.metrics import adjusted_rand_score
def dendrogram_generator(counts, distance, linkage_method, counts_type):
    dist = pdist(counts, metric = distance)
    Z = linkage(dist, method = linkage_method)
    dendrogram(Z, labels = labels)
    plt.title(f"{distance} distance , {linkage_method} linkage, {counts_type} counts, k = 4")  #..................second change
    plt.show()
    return Z
def cutted_dendro_ari(Z, t = 2):
    return fcluster(Z, t = 2, criterion = "maxclust")
def ari(Z1, Z2):
    dendro1 = cutted_dendro_ari(Z1)
    dendro2 = cutted_dendro_ari(Z2)
    ari = adjusted_rand_score(dendro1, dendro2)
    return ari
#ari values for k=4, 5  (change the value of k in appending_the_sequences.py to 4 or 5 as and when needed)   #............third change
print("distance: linkage: k: ARI:") 
Z1 = dendrogram_generator(raw_counts_df, "euclidean", "average", "raw counts")
Z2 = dendrogram_generator(frequency_counts_df, "euclidean", "average", "frequency counts")
print("euclidean average k=4", round(ari(Z1, Z2), 2))
Z3 = dendrogram_generator(raw_counts_df, "euclidean", "complete", "raw counts")
Z4 = dendrogram_generator(frequency_counts_df, "euclidean", "complete", "frequency counts")
print("euclidean complete k=4", round(ari(Z3, Z4), 2))
Z5 = dendrogram_generator(raw_counts_df, "euclidean", "single", "raw counts")
Z6 = dendrogram_generator(frequency_counts_df, "euclidean", "single", "frequency counts")
print("euclidean single k=4", round(ari(Z5, Z6), 2))
Z7 = dendrogram_generator(raw_counts_df, "cityblock", "average", "raw counts")
Z8 = dendrogram_generator(frequency_counts_df, "cityblock", "average", "frequency counts")
print("cityblock average k=4", round(ari(Z7, Z8), 2))
Z9 = dendrogram_generator(raw_counts_df, "cityblock", "complete", "raw counts")
Z10 = dendrogram_generator(frequency_counts_df, "cityblock", "complete", "frequency counts")
print("cityblock complete k=4", round(ari(Z9, Z10), 2))
Z11 = dendrogram_generator(raw_counts_df, "cityblock", "single", "raw counts")
Z12 = dendrogram_generator(frequency_counts_df, "cityblock", "single", "frequency counts")
print("cityblock single k=4", round(ari(Z11, Z12), 2))
Z13 = dendrogram_generator(raw_counts_df, "cosine", "average", "raw counts")
Z14 = dendrogram_generator(frequency_counts_df, "cosine", "average", "frequency counts")
print("cosine average k=4", round(ari(Z13, Z14), 2))
Z15 = dendrogram_generator(raw_counts_df, "cosine", "complete", "raw counts")
Z16 = dendrogram_generator(frequency_counts_df, "cosine", "complete", "frequency counts")
print("cosine complete k=4", round(ari(Z15, Z16), 2))
Z17 = dendrogram_generator(raw_counts_df, "cosine", "single", "raw counts")
Z18 = dendrogram_generator(frequency_counts_df, "cosine", "single", "frequency counts")
print("cosine single k=4", round(ari(Z17, Z18), 2))




