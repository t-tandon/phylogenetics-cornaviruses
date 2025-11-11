
# **Phylogenomic Analysis of Coronaviridae**

Whole-genome and protein-level phylogenetics using MAFFT, IQ-TREE, TrimAl, and custom Python preprocessing.

## **Overview**

This repository documents a complete exploratory phylogenomic analysis of 70+ coronavirus genomes and key viral proteins (Spike, Nucleocapsid), including:

* Genome preprocessing and header cleanup
* Multiple sequence alignment (MAFFT)
* Model selection and phylogenetic inference (IQ-TREE 2)
* Trimming noisy alignment regions (TrimAl)
* Tree comparison (RF distance, tanglegrams)
* Comparison of conserved vs variable protein trees
---

## **Project Workflow**

### **1. Data collection**

* Downloaded 73 complete coronavirus genomes from NCBI Virus
* Downloaded protein FASTAs for Spike and Nucleocapsid
* Cleaned and standardized headers for downstream visualization and IQ-TREE compatibility

### **2. Whole-genome analyses**

Analyses were performed:

* with the “salmon coronavirus” outlier
* without the salmon sequence
* with multiple trimming thresholds (0.1–0.5)

Tools used:

```bash
mafft --auto <input.fasta> > <aligned.fasta>
iqtree2 -s <aligned.fasta> -m MFP -bb 1000 -nt AUTO
trimal -in <aligned> -out <trimmed> -gt 0.1
```

Key outcomes:

* Best-fit nucleotide model: **GTR+F+I+G4**
* Removing salmon genome changes only ~4% of bipartitions (RF distance ~0.043)
* Trimming thresholds do not materially change topology

---

### **3. Protein-level analyses**

**Proteins studied:**

* Spike (variable)
* Nucleocapsid (moderately conserved)

Headers standardized as:
```
>Organism | Accession | Protein
```

Key results:

* Spike: best model WAG+F+R6
* Nucleocapsid: best model Q.pfam+F+R5
* Nucleocapsid–Spike comparison feasible: 60 shared assemblies

*Note:* initial analysis was carried out with nsp12–spike comparison but failed due to zero shared taxa

---

### **4. Tree comparison**

Comparison methods:

* Robinson–Foulds (RF) distance
* Cophylo tanglegrams
* Bootstrap support assessment
* Split-by-split topology examination

Findings:

* Whole-genome trees are highly stable across trimming thresholds
* Removing salmon genome does not distort overall phylogeny
* Conserved (Nucleocapsid) vs variable (Spike) protein trees show broadly consistent evolutionary signal
* Differences are concentrated in shallow clades and high-variability regions
