# Methods

## Sample

- **Accession:** SRR37543559
- **Library type:** Single-end
- **Read length:** 40bp
- **Total reads (raw):** 25,562,087
- **Reference genome:** hg38 (GRCh38)

## Pipeline Steps

### 1. Data retrieval
Raw reads pulled via `fastq-dump` (single-end mode) on Galaxy Australia.

### 2. Initial quality check — FastQC
Raw reads assessed for quality before any trimming.

- Total sequences: 25,562,087
- Total bases: 1 Gbp
- Sequence length: 40bp
- Encoding: Sanger / Illumina 1.9
- %GC: 41%
- Sequences flagged as poor quality: 0

**Module results:**

| Module | Result |
|---|---|
| Basic Statistics | Pass |
| Per base sequence quality | Pass |
| Per tile sequence quality | Pass |
| Per sequence quality scores | Pass |
| Per base sequence content | **Fail** |
| Per sequence GC content | Warning |
| Per base N content | Pass |
| Sequence Length Distribution | Pass |
| Sequence Duplication Levels | Pass |
| Overrepresented sequences | Pass (none found) |
| Adapter Content | Pass |

The "Per base sequence content" failure is common due to early-cycle positional bias and is not unusual in WGS libraries — it doesn't necessarily indicate a problem, but is one reason a trimming step (fastp) follows regardless.

Full report: [`results/fastqc/fastqc_report.html`](../results/fastqc/fastqc_report.html)

### 3. Quality control & trimming — fastp v1.3.3
Read quality assessed and low-quality reads/bases trimmed.

- Reads before filtering: 25,562,087
- Reads after filtering: 25,493,268
- Reads passing filters: 99.73%
- Reads removed for low quality: 0.27%
- Reads removed for excess N content: 0.003%
- Q30 bases: 94.4% (before) → 94.5% (after)

Full report: [`results/fastp/fastp_report.html`](../results/fastp/fastp_report.html)

### 4. Alignment — BWA
Trimmed reads aligned against the hg38 reference genome, producing coordinate-unsorted BAM output.

### 5. Sort — SortSam
Alignments sorted into coordinate order for downstream variant calling.

### 6. Variant calling — FreeBayes v1.3.10
Variants called from the sorted BAM against hg38.

- Total variant records: 105,517
- SNPs: 101,792
- Indels: 3,725
- Multi-allelic sites: 153

### 7. Filtering — VCFfilter
Raw FreeBayes output filtered to remove low-confidence calls before annotation.

### 8. Annotation — SnpEff v5.4c
Filtered VCF annotated against the hg38 gene model.

- Input variant records: 146,436
- Variants processed: 146,421
- Total annotations produced: 283,576
- Genome effective length: 3,139,120,403 bp
- Variant rate: 1 variant per 21,439 bases

Full report: [`results/snpeff/snpeff_report.html`](../results/snpeff/snpeff_report.html)
Per-gene impact table: [`results/snpeff/snpeff_stats_genes.txt`](../results/snpeff/snpeff_stats_genes.txt)

## Command line (SnpEff, from report metadata)

\`\`\`
SnpEff -i vcf -o vcf -csvStats snpeff_stats.csv -s snpeff_stats.html hg38 <input.vcf>
\`\`\`

## Platform

All steps executed on [Galaxy Australia](https://usegalaxy.org.au/) using its hosted tool versions and hg38 reference build.
