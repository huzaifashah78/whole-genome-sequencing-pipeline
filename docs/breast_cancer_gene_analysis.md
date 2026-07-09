# Breast Cancer Gene Mutation Analysis

## Objective

Using the SnpEff per-gene annotation table (`snpeff_stats_genes.txt`), identify mutations in genes other than BRCA1/BRCA2 that are known to be associated with breast cancer risk, and describe their biological role.

## Method

The gene stats file reports variant counts across four impact categories per gene/transcript:

- `variants_impact_HIGH`
- `variants_impact_MODERATE`
- `variants_impact_LOW`
- `variants_impact_MODIFIER`

Together, these four columns account for all annotated mutations for a given gene. A gene was flagged as mutated if any of these columns had a non-zero value. Using this rule, a set of known breast-cancer-associated genes (excluding BRCA1/BRCA2) was checked against the file, and genes with confirmed non-zero impact values were selected for further review.

## Findings

| Gene | Impact | Count | Region | 
|---|---|---|---|
| ATM | MODIFIER | 5 | Intronic |
| CDH1 | MODIFIER | 2 | Intronic |
| BARD1 | MODIFIER | 4 | Intronic |
| RAD51D | MODERATE | 1 | Missense (coding) |

### ATM
5 MODIFIER-impact mutations found, located in intronic regions. ATM plays a central role in the DNA damage response — it helps detect and signal double-strand breaks for repair. Loss-of-function mutations in ATM are associated with elevated breast cancer risk, though intronic MODIFIER variants alone are not typically sufficient evidence of functional impact without further splicing analysis.

### CDH1
2 MODIFIER-impact mutations found, in intronic regions. CDH1 encodes E-cadherin, a protein responsible for cell-cell adhesion. Germline CDH1 mutations are strongly associated with hereditary diffuse gastric cancer and lobular breast cancer specifically.

### BARD1
4 MODIFIER-impact mutations found, in intronic regions. BARD1 forms a heterodimer with BRCA1 and is essential for BRCA1's role in homologous recombination DNA repair. Mutations affecting BARD1 can impair this repair pathway even when BRCA1 itself is unaffected, and BARD1 mutations are independently linked to breast and ovarian cancer risk.

### RAD51D
1 MODERATE-impact mutation — a missense variant, meaning it directly alters the encoded protein rather than being confined to a non-coding region. This is the most functionally notable finding in this analysis, since MODERATE-impact coding changes are more likely to affect protein function than MODIFIER-class intronic variants. RAD51D is part of the RAD51 paralog family involved in homologous recombination repair, the same pathway used by BRCA1/BRCA2, and RAD51D mutations are established breast and ovarian cancer risk factors.

## Interpretation

Three of the four genes (ATM, CDH1, BARD1) show only MODIFIER-class intronic variants — these are the most common and generally least functionally disruptive variant class, and would need additional analysis (e.g. splice-site prediction) to assess real impact. The RAD51D finding is the standout result: a MODERATE-impact missense mutation directly changes the protein sequence and is a more biologically actionable finding, particularly given RAD51D's established role in the same DNA repair pathway as BRCA1/BRCA2.

This analysis is exploratory and screening-level — confirming pathogenicity of any of these variants would require cross-referencing against clinical variant databases (e.g. ClinVar) and, for RAD51D specifically, structural or functional prediction of the missense change.

## Data Source

Full per-gene impact table: [`results/snpeff/snpeff_stats_genes.txt`](../results/snpeff/snpeff_stats_genes.txt)
