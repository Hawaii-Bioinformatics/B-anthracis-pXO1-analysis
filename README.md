# Machine-learning-based Characterization of *Bacillus anthracis* Phenotypes from pXO1 Plasmid Proteins

This repository contains the **code and data** used in the manuscript:

> **Machine-learning-based characterization of *Bacillus anthracis* phenotypes from pXO1 plasmid proteins**  
> William Harrigan¹, Thi Hai Au La², Prashant Dahal², **Mahdi Belcaid¹***, **Michael H. Norris²***  

¹ University of Hawai‘i at Mānoa  
² U.S. Army Medical Research Institute of Infectious Diseases (USAMRIID)  

---

## Abstract

The *Bacillus anthracis* pXO1 plasmid, encoding ~143 proteins, presents a compact model for exploring protein function and evolutionary patterns using protein language models. Due to the organism’s slow evolutionary rate, its limited amino acid variation enhances detection of physiologically relevant protein-protein interactions.  

In this study, we applied embedding-based analyses and bioinformatics methods to characterize pXO1 proteins across diverse *B. anthracis* lineages. We generated sequence embeddings, constructed phylogenies, and compared plasmid content with whole genome variation. While whole-genome and plasmid-based phylogenies diverge, pXO1 protein composition revealed lineage-specific structure.  

Association rule mining generated a decision tree classifier informative of sublineages, while functionally redundant protein modules reflected geographic and phylogenetic patterns. A conserved DNA replication module exhibited both shared and *B. anthracis*-specific features.  

These results show that the pXO1 plasmid contains biologically and evolutionarily informative signatures, highlighting the co-adaptive evolution of virulence-related protein modules. Though plasmid data alone lacks the resolution of whole-genome approaches, it provides valuable insights into the ecology and evolution of *B. anthracis*. This framework can be extended to study additional virulence plasmids across *Bacillus* and other environmental pathogens using scalable protein language model tools.

**Keywords:** machine learning, *Bacillus anthracis*, anthrax, AI, phylogeny, affinity analysis, genotype-to-phenotype

---

## Repository Structure

```
B-anthracis-pXO1-analysis/
│
├── files/
│   ├── NCBI_genome_annotations/          # Annotated genome and plasmid protein tables
│   ├── domain_search_files/              # Pfam domain search results and metadata
│   └── other_input_files/                 # Additional metadata for analysis
│
├── notebooks/
│   ├── data_processing.ipynb             # Data loading, processing, and feature encoding
│   ├── mutual_information.ipynb          # MI computation and feature selection
│   ├── decision_tree_analysis.ipynb      # Decision tree training and visualization
│   └── tsne_visualization.ipynb          # t-SNE plotting for plasmid protein content
│
├── scripts/
│   ├── load_annotations.py
│   ├── compute_mutual_information.py
│   ├── plot_decision_tree.py
│   └── plot_tsne.py
│
└── README.md
```

---

## Analysis Workflow

The repository is organized into **four main steps**:

### **1. Load and Encode pXO1 Protein Composition**
- Parse NCBI genome annotation files to extract protein presence/absence for each plasmid.
- One-hot encode plasmid protein profiles for downstream analysis.

### **2. Identify Lineage-informative Proteins**
- Apply **Mutual Information (MI)** scoring to quantify the discriminative power of each protein for sublineage classification.
- Filter for MI > 0.1.

### **3. Build and Interpret Decision Tree**
- Train a **Decision Tree Classifier** using informative proteins.
- Visualize decision rules that separate *B. anthracis* sublineages.

### **4. Visualize Protein Composition via t-SNE**
- Perform t-SNE dimensionality reduction on binary protein profiles.
- Color-code points by sublineage or ancestral lineage for visual cluster assessment.

---

## Methods & Tools

- **Python Libraries**
  - `pandas`, `numpy` — data handling
  - `mlxtend` — association rule mining
  - `scikit-learn` — mutual information, decision tree classifier, t-SNE
  - `matplotlib`, `seaborn` — plotting
- **Bioinformatics**
  - Pfam domain search results integrated with pXO1 protein annotations
  - Association rules refined with mutual information analysis

---

## Example: Loading and Encoding Proteins

```python
# Load plasmid annotations
annotation_files = glob.glob(f"{home_dir}/files/NCBI_genome_annotations/*")
plasmids = {}

for file_path in annotation_files:
    plasmid_id = "_".join(os.path.basename(file_path).split("_")[-3:-1])
    with open(file_path, "r") as f:
        proteins = [
            line.split("\t")[0]
            for line in f
            if not line.startswith("RefSeq/Protein ID")
        ]
    plasmids[plasmid_id] = proteins

# Build DataFrame and one-hot encode
plasmid_df = pd.DataFrame(
    [(pid, prot) for pid, prots in plasmids.items() for prot in prots if prot],
    columns=["plasmid_id", "protein_sequence_id"]
)

plasmid_sequences_encode = (
    plasmid_df.groupby(["plasmid_id", "protein_sequence_id"])["protein_sequence_id"]
    .count()
    .unstack(fill_value=0)
    .map(lambda x: 1 if x != 0 else 0)
)
```

---

## Output Examples

- **Decision Tree (Informative Proteins Only)**  
  Shows how specific protein modules predict sublineage membership.

- **t-SNE plots**  
  Two-dimensional projection of plasmid protein profiles revealing clustering patterns by lineage.

---

## Citation

If you use this code or data, please cite:

> Harrigan W., La T.H.A., Dahal P., Belcaid M., Norris M.H.  
> *Machine-learning-based characterization of Bacillus anthracis phenotypes from pXO1 plasmid proteins*  
> *[Journal Name, Year]*
