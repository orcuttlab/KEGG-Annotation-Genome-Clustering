# KEGG-Annotation-Genome-Clustering
Cluster genomes based on KEGG annotation content. 

This program runs KOFAMSCAN (-mapper option) on a set of input protein fasta files. It then clusters the genomes by similarity based on their KEGG annotations. 

Fasta file format requirements:

Please format fasta files with a simple name that is one string with no spaces or special characters besides dashes or underscores. The shorter and simpler the name, the better.

The fasta file name should be formatted so that everything before .faa is what you want your genomes to be called in downstream figures.
Please ensure the fasta headers are formatted in a simple way that is one string of text.  It is best that the individual ORFs are formatted in a way that is easily identifiable for downstream parsing.

Example of an ideal fasta header: 

>GenomeName_Orf1
 
If you are using genomes downloaded from a database like NCBI or IMG it is probably best to use the identifiers used on those databases for future reference:

>ImgGenomeeID_ImgOrfID 


The resulting KOFAMSCAN annotation files are used to build a Genome x KEGG ID count table, with KEGG ID's missing from a given genome counted as 0
The KEGG content table is an output (PREFIX__KO_Table.txt).  Additionally, the genomes are hierarchically clustered based on KEGG content using the euclidean distance of KEGG presence/absence data and the Wards linkage method.

The program will output a Genome X KO# count table and a hierarchically clustered heatmap.  The clustering and heatmap are based on a binary version of the data (the data in the table file converted to 0's for absence and 1's for presence of a given KO).


This program requires that you have KOFAMSCAN installed in your path. This can be set up using Anaconda: https://anaconda.org/bioconda/kofamscan 
Be sure to load the Conda environment that KOFAMSCAN is active prior to running.

The necessary HMM profiles and KO IDs to run KOFAMSCAN can be downloaded from this link: ftp://ftp.genome.jp/pub/db/kofam/
Input arguments allow you to point to where you have stored those files for running KOFAMSCAN
