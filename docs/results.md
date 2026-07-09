# Results

## Initial Read Quality (FastQC — pre-trimming)

| Measure | Value |
|---|---|
| Total sequences | 25,562,087 |
| Total bases | 1 Gbp |
| Sequence length | 40bp |
| %GC | 41% |
| Sequences flagged as poor quality | 0 |

**Module results:** 10 of 11 modules passed. "Per base sequence content" failed and "Per sequence GC content" showed a warning — both common in WGS libraries due to early-cycle positional bias, and not indicative of a data quality problem on their own.

Full report: [`results/fastqc/fastqc_report.html`](../results/fastqc/fastqc_report.html)

## Read Quality (fastp — post-trimming)

| | Before filtering | After filtering |
|---|---|---|
| Total reads | 25.56 M | 25.49 M |
| Total bases | 1.022 G | 1.020 G |
| Q20 bases | 96.11% | 96.22% |
| Q30 bases | 94.39% | 94.51% |
| GC content | 41.68% | 41.67% |

**Filtering outcome:** 99.73% of reads passed filters. Only 0.27% were removed for low quality, and adapter contamination was negligible (0.00% adapter dimer reads) — indicating clean input data with minimal trimming required.

## Variant Calling (FreeBayes)

| Metric | Count |
|---|---|
| Total variant records | 105,517 |
| SNPs | 101,792 (96.5%) |
| Indels | 3,725 (3.5%) |
| Multi-allelic sites | 153 |

## Annotation (SnpEff)

### Summary

| Metric | Value |
|---|---|
| Variants processed | 146,421 |
| Multi-allelic VCF entries | 516 |
| Total annotations generated | 283,576 |
| Variant rate | 1 per 21,439 bp |

### Effects by impact

| Impact | Count | Percent |
|---|---|---|
| HIGH | 64 | 0.023% |
| MODERATE | 1,437 | 0.507% |
| LOW | 1,737 | 0.613% |
| MODIFIER | 280,338 | 98.858% |

As expected for a WGS sample, the overwhelming majority of annotated effects are MODIFIER-class (intronic, intergenic, UTR) — the small HIGH and MODERATE fractions are where functionally consequential mutations (frameshift, stop-gained, missense) are concentrated, and are the effects worth following up biologically.

### Effects by functional class

| Class | Count | Percent |
|---|---|---|
| MISSENSE | 1,325 | 49.85% |
| SILENT | 1,313 | 49.40% |
| NONSENSE | 20 | 0.75% |

Missense and silent mutations occur at roughly equal rates, which is consistent with expected background mutation patterns; nonsense (stop-gained) mutations are rare, as they tend to be more deleterious and are selected against.

## Interpretation

The read QC results indicate high-quality sequencing input, meaning downstream variant calls are less likely to be artifacts of poor base calling. The variant load and impact distribution are consistent with typical human WGS output — the vast majority of variants are non-coding or synonymous, with a small, biologically meaningful subset in the MODERATE/HIGH impact categories. That subset is the basis for the targeted breast-cancer gene analysis in [breast_cancer_gene_analysis.md](breast_cancer_gene_analysis.md).
