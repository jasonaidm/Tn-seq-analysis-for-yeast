# Tn-seq-analysis-for-yeast
The Tn-seq Analysis of Yeast Package
Features
The package implements a pipeline consisting of a read preprocessing module followed by an off-target identification module. The preprocessing module takes raw reads (FASTQ) from a pooled multi-sample sequencing run as input. Reads are demultiplexed into sample-specific FASTQs and PCR duplicates are removed using unique molecular index (UMI) barcode information.
 
The individual pipeline steps are:
1.	Sample demultiplexing: A pooled multi-sample sequencing run is demultiplexed into sample-specific read files based on sample-specific dual-indexed barcodes
2.	PCR Duplicate Consolidation:Reads that share the same UMI and the same first six bases of genomic sequence are presumed to originate from the same pre-PCR molecule and are thus consolidated into a single consensus read to improve quantitative interpretation of GUIDE-Seq read counts.
3.	Read Alignment: The demultiplexed, consolidated paired end reads are aligned to a reference genome using the BWA-MEM algorithm with default parameters (Li. H, 2009).
4.	Candidate Site Identification: The start mapping positions of the read amplified with the tag-specific primer (second of pair) are tabulated on a genome-wide basis. Start mapping positions are consolidated using a 10-bp sliding window. Windows with reads mapping to both + and - strands, or to the same strand but amplified with both forward and reverse tag-specific primers, are flagged as sites of potential DSBs. 25 bp of reference sequence is retrieved on either side of the most frequently occuring start-mapping position in each flagged window. The retrieved sequence is aligned to the intended target sequence using a Smith-Waterman local-alignment algorithm.
5.	False positive filtering: Off-target cleavage sites with more than six mismatches to the intended target sequence, or that are present in background controls, are filtered out.
6.	Reporting: Identified off-targets, sorted by GUIDE-Seq read count are annotated in a final output table. The GUIDE-Seq read count is expected to scale approximately linearly with cleavage rates (Tsai et al., Nat Biotechnol. 2015).
7.	Visualization: Alignment of detected off-target sites is visualized via a color-coded sequence grid, as seen below:

Dependencies
•	Python 2.7: If a version does not come bundled with your operating system, we recommend the Anaconda scientific Python package.
•	R version 3.1.1 or later version: A free software environment for statistical computing and graphics. ggplot2 (a plotting system for R) is also required. 
•	Bowtie: An ultrafast memory-efficient short read aligner. You can either install bowtie with a package manager (e.g. brew on OSX or apt-get on Ubuntu/Debian), or you can download it from the project page and compile it from source.
•	Skewer: An adapter Sequences trimming soft. You can download it from the project page and compile it from source.
Getting Set Up
Install Dependencies
Tnseqy requires this software to be installed::
•	Python 2.7: If a version does not come bundled with your operating system, we recommend the Anaconda scientific Python package.
•	R version 3.1.1 or later version: A free software environment for statistical computing and graphics. ggplot2 (a plotting system for R) is also required. 
•	Bowtie: An ultrafast memory-efficient short read aligner. You can either install bowtie with a package manager (e.g. brew on OSX or apt-get on Ubuntu/Debian), or you can download it from the project page and compile it from source.
•	Skewer: An adapter Sequences trimming soft. You can download it from the project page and compile it from source.
For both bwa and bedtools, make sure you know the path to the respective executables, as they need to be specified in the pipeline manifest file.
