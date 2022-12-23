# Finding Similar Items: Textually Similar Documents

Check all information in the Jupyter Notebook.

## Background

To find textually similar documents among a large dataset, by defining the similarity as the Jaccard similarity, one should compare documents pair-wise. In fact, that similarity is represented by the ratio between the intersection of two sets with their union. As the magnitude of comparisons for N documents grows with the square of N, a more efficient method consists in comparing only those documents that are likely to be similar. This is a three-stage process consisting of shingling, min-hashing and locality-sensitive hashing.

During the shingling phase, a text document is tokenized into k-shingles, e.g. D={abcde}, S(D)={ab, bc, cd, de} for k=2. Having each document represented as a large set of shingles, these can be further reduced into smaller integer vectors called signatures. 

In the min-hashing phase, each shingle in a document is hashed with n different functions and only the minimum value is kept. The result of this second phase is a signature matrix having as rows n hash functions, and as columns a series of vectors each representing a document. Each cell fo the vector contains with the minimal value among all hashed shingles for a specific function. 

Assuming that signatures still represent the document and preserve similarities, in the third phase locality-sensitive hashing can be applied to generate candidate pair. The idea is to divide the matrix into b bands of r rows each and hash these bands to different buckets. Assuming that two bands are identical if they end up in the same bucket, the candidate pairs will be those documents that share at least one bucket in common for at least one band. Finally, only those candidate pairs can be checked for similarity using Jaccard Similarity.
