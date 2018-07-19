# RNAseq-workflow-using-bowtie2-and-deseq2
A RNA-seq workflow using bowtie2 for alignment and deseq2 for differential expression.

The workflow including the following major steps:
* Align all the R1 reads to the genome with bowtie2 in local mode
* Count the aligned reads to annotated genes with featureCounts
* Performed differential gene expression with DESeq2

# Installation
Requirements: This workflow have been tested on linux environment, it will probably also work on Mac OS and Windows 10 (via the integrated linux subsystem).

* Download and extract this package to a folder {installDir}. 
* Install anaconda3
* From {installDir}, install other external tools using anaconda
```conda env create -f environment.yml```

* Prepare a genome data folder {genomeDir}, with
  * genome.fasta: could be downloaded using `___`
  * genes.gtf: cound be downloaded from GENCODE using `___`
  * Bowtie2Index/: optional, can be automatically generated (if necessary) while running the workflow.

# Usage
## Prepare a work folder {workDir} with
  * input/: with row sequence files, each sample as a folder of fastq(.gz) files.
  * sampleInfo.csv: a comma seperated file with the following columns
    * sample: the sample folder name
    * group: the smaple group name, used to make your contrasts for differential expression
    * batch: optional, use batch mode (or pairwise) if defined.
    
    An example file can be found in {installDir}
    
  * config.yaml: the major file for configuration of
    * genomeDir
    * contrasts
    * Other parameters
    
    An example file can be found in {installDir}
     
## from the {installDir},
  * test by `snakeMake -d {workDir} -n`
  * run the pipeline by `snakeMake -d {workDir}`
  * or run the pipeline parallelly on a cluster by `snakeSlurm -d {workDir}`

# Output
The output files are generated in your {workDir}:
* {genome}.bowtie2/: the alignment files (.bam), the coverage files (.bw), ...
* {genome}.gene_count/: the gene count matrix (gene x sample), the mapping and count summary (...)
* {genome}.deseq2/: the differential expression for each contrast.

  
