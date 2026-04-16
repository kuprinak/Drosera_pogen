# Drosera_popgen
## Population genomics of _Drosera rotundifolia_ in Europe (ddRAD)

Full details of the data analysis will be posted soon.

> [!TIP]
> To view any HTML file, please, download it

### Used programs: bcl2fastq v2.20

* [bcl2fastq](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html) v2.20 - demultiplexing and adaptor removal (done by LGC Genomics, Berlin, Germany)
* [trimmomatic](https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software.html) v0.39 - trimming low quality reads and additional adapter removal
* [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) v0.12.1, [MultiQC](https://seqera.io/multiqc/) v1.32
* [rnaSPAdes](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-020-03614-2) v3.15.4  - transcriptome assembling

### Workflow:
```mermaid
flowchart TB
    A@{shape: procs, label: "Illumina raw reads (ddRAD)"} --> B([SortMeRNA]);
 B --> C([bcl2fastq + Trimmomatic]);


AA@{shape: procs, label: "Nanopore raw reads"} --> K([rnaSPAdes]);

AAA@{shape: procs, label: "Illumina raw reads (RNA-seq)"} --> K([rnaSPAdes]);
    C --> K([])
