# KEGG-Annotation-Genome-Clustering

This program runs KOFAMSCAN (-mapper option) on a set of input protein fasta files. It then clusters the genomes by similarity based on their KEGG annotations. 

Please format fasta files with a simple name that is one string with no spaces or special characters besides dashes or underscores. The shorter and simpler the name, the better. The fasta file name should be formatted so that everything before .faa is what you want your genomes to be called in downstream figures.
It is best of the fasta headers are formatted in a way that is easily identifiable for downstream parsing. Example

">GenomeName_Orf1"
 
If you are using genomes downloaded from a database like NCBI or IMG it is probably best to use the identifiers used on those databases for future reference:

">ImgGenomeeID_ImgOrfID" 

The resulting KOFAMSCAN annotation files are used to build a Genome x KEGG ID count table, with KEGG ID's missing from a given genome counted as 0
The KEGG content table is an output (PREFIX__KO_Table.txt).  Additionally, the genomes are hierarchically clustered based on KEGG content using the euclidean distance of KEGG presence/absence data and the Wards linkage method.

The program will output a Genome X KO# count table and a hierarchically clustered heatmap.  The clustering and heatmap are based on a binary version of the data (the data in the table file converted to 0's for absence and 1's for presence of a given KO).


This program requires that you have KOFAMSCAN installed in your path. This can be set up using Anaconda: https://anaconda.org/bioconda/kofamscan 
Be sure to load the Conda environment that KOFAMSCAN is active prior to running.

The necessary HMM profiles and KO IDs to run KOFAMSCAN can be downloaded from this link: ftp://ftp.genome.jp/pub/db/kofam/
Input arguments allow you to point to where you have stored those files for running KOFAMSCAN

# Comparison to Annotation-independent workflows
This workflow was tested against an annotation-independent workflow that clusters genomes based on protein families (links below). The sequence similarity calculation followed by MCL clustering used is similar to the pangenome workflow in the Anvio program.   

https://github.com/raphael-upmc/proteinClusteringPipeline and in this publication: https://www.nature.com/articles/s41467-019-12171-z

The Mantel test in the R library Vegan was used to compare the data resulting from this KEGG annotation based genome-clustering, and annotation-independent protein-family based genome-clustering mentioned above. The comparison shows that the resulting data from both workflows is highly correlated (R2 = 0.9332 for Euclidean distance and 0.8625 for the Jaccard distance), and thus the intepretations will be similar. 

