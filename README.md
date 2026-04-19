# RNA-Seq-Reference-Based-Analysis-Workflow
### Biological Insights into Splicing Regulation in *Drosophila melanogaster*

## 🧬 Project Background
This project analyzes RNA-Seq data from *Drosophila melanogaster* cells to investigate the impact of the **Pasilla (PS)** gene. Pasilla is the fly homolog of the human splicing factors **NOVA1** and **NOVA2**. By depleting this gene via RNA interference (RNAi), we identified genes and pathways regulated by this specific splicing factor.

The pipeline processes raw sequencing reads (**FASTQ**) through to biological interpretation via **GO/KEGG Enrichment**.

---

## 🛠 The Bioinformatics Pipeline

### 1. Pre-processing & Quality Control
* **Tools:** `Falco` (FastQC replacement) and `MultiQC`.
* **Process:** Checked raw reads for per-base quality, adapter contamination, and GC bias.
* **Result:** Data was aggregated into a MultiQC report to ensure consistency across biological replicates.

> **[ADD SCREENSHOT HERE]**: Upload your `MultiQC_report.png` (showing General Statistics and % GC) to an `images` folder and link it here: 
> `![MultiQC Statistics](images/multiqc_stats.png)`

### 2. Read Mapping (Alignment)
* **Tool:** `RNA STAR` (Spliced Transcripts Alignment to a Reference).
* **Reference:** *D. melanogaster* genome (BDGP6).
* **Method:** Splicing-aware alignment ensured reads spanning exon-exon junctions were correctly mapped.

> **[ADD SCREENSHOT HERE]**: `![STAR Alignment View](images/star_alignment.png)`
> *Tip: Use a pyGenomeTracks or JBrowse view showing read peaks over the Thd1 gene.*

### 3. Quantification
* **Tool:** `featureCounts`.
* **Method:** Counted reads mapping to gene features defined in the GTF.
* **Strandness:** Library was determined to be **unstranded** by comparing coverage of forward/reverse strands.

### 4. Differential Expression Analysis (DGE)
* **Tool:** `DESeq2`.
* **Statistical Logic:** Shrinkage estimator for fold change and Wald test for significance.
* **Filters:** Adjusted p-value (FDR) < 0.05 and $|log_2 \text{Fold Change}| > 1$.

> **[ADD SCREENSHOT HERE]**: `![DESeq2 Volcano Plot](images/volcano_plot.png)`

### 5. Functional Enrichment Analysis
* **Tool:** `goseq`.
* **Correction:** Corrected for gene length bias.
* **Databases:** Gene Ontology (GO) and KEGG Pathways.

> **[ADD SCREENSHOT HERE]**: `![Enrichment Bar Chart](images/enrichment_results.png)`

---

## 📊 Key Results Summary

| Metric | Result |
| :--- | :--- |
| **Total Samples** | 7 (4 Untreated, 3 Treated) |
| **Mapping Rate** | ~90-95% |
| **Significant DEGs** | [Insert Number, e.g. 450] |
| **Top Up-regulated Gene** | [Insert Gene Name] |
| **Primary Pathway Impacted** | RNA Splicing / Metabolism |

### Data Visualization: The Heatmap
The heatmap displays the $Z$-score of the top 30 differentially expressed genes. It demonstrates clear clustering where treated samples (Pasilla-depleted) show a distinct expression profile compared to wild-type controls.

> **[ADD SCREENSHOT HERE]**: `![Expression Heatmap](images/heatmap.png)`

---

## 🚀 How to Run this Project
1.  **Galaxy Workflow:** Import the provided `.ga` file from the `/workflows` folder into your Galaxy instance.
2.  **Input Data:** Data can be retrieved from the [Zenodo Repository](https://zenodo.org/record/6457007).
3.  **Reference Genome:** Use the `dm6` (BDGP6) build for *Drosophila*.

## 📚 References
* **Brooks et al. (2011).** "Conservation of an RNA regulatory network." *Genome Research*.
* **Galaxy Training Network (GTN).** [Reference-based RNA-Seq Tutorial](https://training.galaxyproject.org/training-material/topics/transcriptomics/tutorials/ref-based/tutorial.html).

---
*This project was completed as part of a bioinformatics competency training in transcriptomics.*
