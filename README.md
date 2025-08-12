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
│   ├── NCBI_genome_annotations/          # Annotated genome and plasmid protein text files
│   ├── domain_search_files/              # InterProScan domain search results, reference domains and metadata
│   └── pXO1_plasmid_protein_sequences.fasta  # Complete set of pXO1 protein sequences used in analysis
│
├── jupyter_notebooks/
│   ├── pxo1_plasmid_affinity_analysis.ipynb   # Affinity analysis, computation of decision tree
│   ├── pxo1_plasmid_domain_search.ipynb       # Searching domains in pXO1 plasmids from reference NERD-domain network
│   ├── pxo1_plasmid_tsne_projection.ipynb     # t-SNE plot for plasmid protein composition
│    
└── README.md
```

---

## Citation

If you use this code or data, please cite:

> Harrigan W., La T.H.A., Dahal P., Belcaid M., Norris M.H.  
> *Machine-learning-based characterization of Bacillus anthracis phenotypes from pXO1 plasmid proteins*  
