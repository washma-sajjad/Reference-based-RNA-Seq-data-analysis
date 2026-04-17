#  Reference-based RNA-Seq Data Analysis

**Assignment | Bioinformatics | Galaxy Training Network Tutorial**

---

##  Overview

This repository contains the outputs of a complete **Reference-based RNA-Seq data analysis** pipeline performed on *Drosophila melanogaster* using the [Galaxy Training Network (GTN) tutorial](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/ref-based/tutorial.html).

The study is based on [Brooks *et al.* 2011](https://genome.cshlp.org/content/21/2/193), which investigates the role of the *Pasilla* gene — the *Drosophila* homologue of mammalian splicing regulators Nova-1 and Nova-2 — in regulating gene expression. RNA interference (RNAi) was used to deplete the *Pasilla* gene, and RNA-Seq was performed to identify differentially expressed genes between treated (PS-depleted) and untreated samples.

---

##  Dataset

| Sample | Condition | Type |
|--------|-----------|------|
| GSM461176 | Untreated | Single-end |
| GSM461177 | Untreated | Paired-end |
| GSM461178 | Untreated | Paired-end |
| GSM461182 | Untreated | Single-end |
| GSM461179 | Treated (PS depleted) | Paired-end |
| GSM461180 | Treated (PS depleted) | Paired-end |
| GSM461181 | Treated (PS depleted) | Single-end |

- **Organism:** *Drosophila melanogaster*
- **Reference Genome:** dm6
- **Raw data:** [GSE18508 on NCBI GEO](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE18508)
- **Zenodo dataset:** [https://zenodo.org/record/6457007](https://zenodo.org/record/6457007)

---

##  Workflow Summary

```
Raw FASTQ reads
      │
      ▼
Quality Control (Falco + MultiQC)
      │
      ▼
Trimming (Cutadapt + MultiQC)
      │
      ▼
Splice-aware Mapping (STAR + MultiQC)
      │
      ▼
Read Counting (featureCounts)
      │
      ▼
Differential Expression Analysis (DESeq2)
      │
      ▼
Annotation & Visualization (heatmaps, PCA, volcano plots)
      │
      ▼
Functional Enrichment Analysis (goseq + Pathview)
```

---

##  Repository Structure

```
 Reference-based-RNA-Seq-data-analysis/
│
├──  01_quality_control/
│   ├── multiqc_report_falco.html          # QC report before trimming
│   └── multiqc_report_cutadapt.html       # QC report after trimming
│
├──  02_mapping/
│   └── multiqc_report_star.html           # STAR alignment statistics
│
├──  03_read_counting/
│   ├── featureCounts_counts.tabular       # Gene read count matrix
│   └── featureCounts_summary.tabular      # Assignment summary/QC
│
├──  04_differential_expression/
│   ├── DESeq2_results.tabular             # Full DESeq2 results table
│   ├── DESeq2_normalized_counts.tabular   # Normalized count matrix
│   ├── DESeq2_plots.pdf                   # PCA, heatmap, MA, volcano plots
│   ├── annotated_DE_genes.tabular         # Filtered & annotated DE genes
│   └── heatmap_DE_genes.png              # Heatmap of top DE genes
│
├──  05_functional_enrichment/
│   ├── goseq_GO_results.tabular           # GO enrichment table
│   ├── goseq_top10_GO_plot.png           # Top 10 GO terms bar chart
│   └── pathview_KEGG_pathways/           # KEGG pathway images (PNG)
│
└── README.md
```

---

##  Tools Used

| Step | Tool | Version |
|------|------|---------|
| Quality Control | Falco | 1.2.4 |
| QC Aggregation | MultiQC | 1.27 |
| Trimming | Cutadapt | 5.2 |
| Mapping | RNA STAR | 2.7.11b |
| Read Counting | featureCounts | – |
| Differential Expression | DESeq2 | – |
| GO Enrichment | goseq | – |
| KEGG Pathway Analysis | Pathview | – |

All tools were run on **[Galaxy](https://usegalaxy.eu)** — an open-source platform for data-intensive biomedical research.

---

##  Key Results

- Reads were trimmed for quality (Q > 20, min length 20 bp) using **Cutadapt**
- Over **80%** of reads mapped uniquely to the *Drosophila* genome (dm6) using **STAR**
- Differentially expressed genes were identified using **DESeq2** (adjusted p-value < 0.05)
- Gene Ontology (GO) and KEGG pathway enrichment analyses were performed on DE genes to identify impacted biological functions

---

##  Reference

Brooks AN, Yang L, Duff MO, et al. (2011). Conservation of an RNA regulatory map between *Drosophila* and mammals. *Genome Research*, 21(2), 193–202. https://doi.org/10.1101/gr.108662.110

---

##  Author

**Washma Sajjad**  
Special Topics in Bioinformatics Assignment  
Galaxy Training Network Tutorial
