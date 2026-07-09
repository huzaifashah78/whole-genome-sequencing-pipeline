# Whole Genome Sequencing Analysis — Variant Calling & Annotation

A complete WGS variant-calling pipeline run on Galaxy Australia, from raw sequencing reads to annotated, gene-level variant reports. Includes a targeted analysis identifying mutations in breast-cancer-associated genes beyond BRCA1/BRCA2.

**Sample:** SRR37543559 (single-end, 40bp reads, ~25.6M reads)
**Reference genome:** hg38
**Platform:** Galaxy Australia

## Pipeline Overview
Raw reads (fastq-dump)
│
▼
FastQC (initial QC check)
│
▼
fastp (QC + trimming)
│
▼
BWA (alignment to hg38)
│
▼
SortSam (coordinate sort)
│
▼
FreeBayes (variant calling)
│
▼
VCFfilter
│
▼
SnpEff (annotation)

See [docs/methods.md](docs/methods.md) for tool versions and exact parameters.

## Key Results

| Metric | Value |
|---|---|
| Reads before filtering | 25.56 M |
| Reads passing QC filters | 99.73% |
| Q30 bases | 94.4% |
| Total variants called | 105,517 |
| SNPs | 101,792 |
| Indels | 3,725 |
| Variants annotated (SnpEff) | 146,421 |
| HIGH-impact effects | 64 |
| MODERATE-impact effects | 1,437 |

Full breakdown in [docs/results.md](docs/results.md).

## Breast Cancer Gene Analysis

A targeted look at non-BRCA1/BRCA2 genes with known breast cancer associations, using the SnpEff gene-level impact table. Four genes showed confirmed mutations: **ATM, CDH1, BARD1, RAD51D**.

Full writeup: [docs/breast_cancer_gene_analysis.md](docs/breast_cancer_gene_analysis.md)

## Repository Structure

​```
├── README.md
├── docs/
│   ├── methods.md
│   ├── results.md
│   └── breast_cancer_gene_analysis.md
└── results/
    ├── fastqc/
    │   └── fastqc_report.html
    ├── fastp/
    │   └── fastp_report.html
    ├── snpeff/
    │   ├── snpeff_report.html
    │   └── snpeff_stats_genes.txt
    └── vcf/
        └── SRR37543559.vcf.gz
​```
## Tools Used

- [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/) — raw read quality control
- [fastp](https://github.com/OpenGene/fastp) v1.3.3 — read QC and trimming
- [BWA](http://bio-bwa.sourceforge.net/) — alignment to hg38
- [FreeBayes](https://github.com/freebayes/freebayes) v1.3.10 — variant calling
- [SnpEff](http://pcingola.github.io/SnpEff/) v5.4c — variant annotation

## Notes

This was completed as part of a bioinformatics WGS data analysis coursework module. All processing was performed on [Galaxy Australia](https://usegalaxy.org.au/).

## Author

**Muhammad Huzaifa Hussain Shah**
Email: huzaifa260106@gmail.com
GitHub: [github.com/huzaifashah78](https://github.com/huzaifashah78)
