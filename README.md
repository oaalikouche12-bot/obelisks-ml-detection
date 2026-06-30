# Detection and classification of obelisks using machine learning

> **Master's Thesis · UPF Barcelona School of Management · June 2026**
> Master's Degree in Data Analytics for Business — *Health Data Analytics track*

End-to-end system for detection, classification, and discovery of **obelisks** — a recently described class of circular RNA elements (Zheludev *et al.*, Cell 2024) — applied to genomic data from the human microbiome. The project combines classical machine learning, deep learning, and bioinformatics to audit the public catalog, reconstruct the S. sanguinis obelisk genome, propose 14 previously undescribed families, and characterize the functional domain of the Oblin protein.

---

## Authors

- **Omar Aalikouche Alichane**
- **Catalina Catà Socias**
- **Adrià Hernández Seguí**

Supervisor: **Ana Freire** (UPF-BSM).

---

## Key contributions

1. **Empirical audit** of POS/NEG/FECAL sequencing data, confirming the all-or-nothing pattern (0.31% / 0% / ~0% obelisk reads).
2. **14 previously undescribed candidate families** (ObnewA–ObnewN) proposed via Ward hierarchical clustering over the 6,356 unclassified entries of the public catalog.
3. **Hardened universal detector (V2)** with 100% sensitivity and 0% false positives against three negative controls, including a GC-matched synthetic control.
4. **Characterization of the canonical Oblin domain** G-Y-X-D-H-G with three sub-classes (X = R, T, K) and statistically significant association with the host phylum (Fisher's exact test p = 0.0455).
5. **PSSM of the Oblin domain** rescuing the chi and beta families from 0% (regex) to 100% (PSSM) — evidence of remote homology.
6. **Four Class II motifs at 100%** family-specificity: pi → ISEADL, sigma → EEVRFL, upsilon → MMNLGL, psi → MKETEK.
7. **New canonical variant G-Y-Q-D-H-G** (residue Q = glutamine) found in candidate family ObnewJ.
8. **Bacterial host prediction** based on codon usage, validated against the S. sanguinis obelisk (Firmicutes, known host).
9. **De novo reconstruction of the S. sanguinis obelisk** from raw reads via differential k-mer analysis, achieving 100% identity to the reference.

---

## Repository structure

```
.
├── README.md                          ← this file
├── LICENSE                            ← MIT
├── notebook/
│   └── TFM_Obeliscos.ipynb            ← main notebook (all sections)
├── thesis/
│   └── Memoria_TFM_Obeliscos.docx     ← full academic memoir
├── defense/
│   └── Defensa_TFM_Obeliscos.pptx     ← defense slides
├── results/
│   ├── TFM_Resultados_Obeliscos.xlsx  ← 8 sheets with all numerical data
│   ├── Explicacion_Completa_TFM.pdf   ← cell-by-cell explanatory analysis
│   └── Resumen_TFM_Obeliscos.pdf      ← executive summary
├── scripts/
│   └── ESMFold_Colab_Oblin.py         ← pipeline for 3D structure prediction (GPU)
└── data/
    └── README.md                       ← how to download the data (not included)
```

---

## Data

Heavy sequencing files (FASTQ, ~1.4 million reads each) and the obelisk catalog **are not included in this repository** due to size constraints and out of respect for the original sources. To reproduce the results:

1. **Obelisk catalog** (Zheludev *et al.* 2024):
 Download supplementary file `mmc2.xlsx` from:
 https://doi.org/10.1016/j.cell.2024.09.033

2. **Sequencing reads** (POS / NEG / FECAL):
 - POS (*Streptococcus sanguinis* SK36 ObP1): SRA SRR####
 - NEG (control): SRA SRR####
 - FECAL (human microbiome): SRA SRR5949245

3. Place the files under `/data/` with the following layout:
 ```
 data/
 ├── mmc2.xlsx
 ├── POS.fastq.gz
 ├── NEG.fastq.gz
 └── FECAL.fastq.gz
 ```

---

## How to run

### Option A — Google Colab (recommended, no local install)

1. Upload `TFM_Obeliscos.ipynb` to Colab.
2. Mount Google Drive and place the data files under `/content/drive/MyDrive/TFM_Obeliscos/`.
3. Run the cells sequentially. A few sections require GPU (Runtime → Change runtime type → T4 GPU): §16 (ESM-2 embeddings), §23 (ESMFold).

### Option B — local with Python 3.10+

```bash
git clone https://github.com/<owner>/tfm-obeliscos.git
cd tfm-obeliscos
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebook/TFM_Obeliscos.ipynb
```

---

## Main dependencies

- Python 3.10+
- `pandas`, `numpy`, `scikit-learn`, `scipy`, `matplotlib`, `seaborn`
- `biopython` (Smith-Waterman, BLOSUM62)
- `ViennaRNA` (RNA secondary structure)
- `pyhmmer` (HMM / PSSM of the Oblin domain)
- `networkx`, `python-louvain` (graph analysis)
- `torch`, `transformers` (ESM-2 / ESMFold, optional)

---

## Key references

- Zheludev, I. N. *et al.* (2024). Viroid-like colonists of human microbiomes. ***Cell*** 187:6521-6536.
- Lin, Z. *et al.* (2023). Evolutionary-scale prediction of atomic-level protein structure with a language model. ***Science*** 379:1123-1130.
- Eddy, S. R. (2011). Accelerated profile HMM searches. ***PLoS Comp. Biol.*** 7:e1002195.
- Carbone, A., Zinovyev, A., & Képès, F. (2003). Codon adaptation index as a measure of dominating codon bias. ***Bioinformatics*** 19:2005-2015.
- Lloyd-Price, J. *et al.* (2019). Multi-omics of the gut microbial ecosystem in inflammatory bowel diseases. ***Nature*** 569:655-662.

---

## License

This work is released under the [MIT License](LICENSE) to encourage academic reuse with appropriate attribution. The original datasets belong to their respective sources (Zheludev et al. 2024, NCBI SRA) and are governed by their own terms.

---

## Suggested citation

> Aalikouche Alichane, O., Catà Socias, C., & Hernández Seguí, A. (2026).
> *Detection and classification of obelisks using machine learning and deep learning applied to genomic data from the human microbiome*.
> Master's Thesis, UPF Barcelona School of Management.
