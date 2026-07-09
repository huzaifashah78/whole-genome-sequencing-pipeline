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
