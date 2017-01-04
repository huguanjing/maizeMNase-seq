# Data analysis of maize MNase-seq datasets
---
Re-analyze data from [Rodgers-Melnick et al. PNAS 2016](http://www.pnas.org/content/113/22/E3177.full)

## Download and prepare datasets

### MNase-seq datasets
Short-read data are deposited in the NCBI short read archive ([SRP064243](http://trace.ddbj.nig.ac.jp/DRASearch/study?acc=SRP064243)), also as Biobroject [PRJNA297204](https://www.ncbi.nlm.nih.gov/bioproject/PRJNA297204). By selecting all 9 SRA Experiments (including 16 illumina runs) to Run Selector, all sample information can be collected and downloaded to [SraRunTable.txt](maizeMNase-seq/SraRunTable.txt).

#### Download fastq files using SRA tool kits
    cd jfw-lab/Projects/MNase-seq/maizePNAS2016
    module load sratoolkit/2.8.0
    fastq-dump -I --split-files SRR2531556

#### Checking read quality with FastQC
    mv *fastq fastq/
    module load fastqc/0.11.3
    fastqc fastq/*fastq
    
#### trim fastq files
module load sickle/1.33
sickle pe -t sanger -f SRR1695160_1.fastq -r SRR1695160_2.fastq -o SRR1695160_1.trimmed.fastq -p SRR1695160_2.trimmed.fastq -s SRR1695160_S.trimmed.fastq

### Maize B73 AGPv3 reference genome


## Read mapping and calling of hypersensive sites
(Rodgers-Melnick et al. PNAS 2016): "After the computational trimming of adaptor sequences using CutAdapt (40), paired-end reads were mapped to the maize B73 AGPv3 reference genome, using Bowtie2 with options “no-mixed,” “no-discordant,” “no-unal,” and “dovetail” (41) for each replicate digest and for the genomic DNA. BED files were made from the resulting BAM files, using bedtools bamtobed, filtered for minimal alignment quality (≥10), and read coverage in 10-bp intervals was calculated using coverageBed (42). The DNS values were obtained by subtracting the mean normalized depth (in reads per million) of the heavy digest replicates from those of the light digest replicates. In this way, positive DNS values correspond to MNase hypersensitive footprints (as defined by ref. 8; and referred to here as MNase HS regions), whereas negative DNS values correspond to nuclease hyper-resistant footprints (MRF, as per ref. 8). A Bayes factor criterion was used to classify as significantly hypersensitive."
