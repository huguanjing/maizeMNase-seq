Data analysis of maize MNase-seq datasets
---

Re-analyze data from Rodgers-Melnick et al. PNAS 2016

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
    
# trim fastq files
module load sickle/1.33
sickle pe -t sanger -f SRR1695160_1.fastq -r SRR1695160_2.fastq -o SRR1695160_1.trimmed.fastq -p SRR1695160_2.trimmed.fastq -s SRR1695160_S.trimmed.fastq
