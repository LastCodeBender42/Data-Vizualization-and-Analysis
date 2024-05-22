# Drug Screening Project: Summary and Results

## 01. Background:

LRH-1 (Liver Receptor Homolog-1), also known as NR5A2 (Nuclear Receptor Subfamily 5 Group A Member 2), plays important roles in glucose metabolism and insulin sensitivity, making it relevant to the understanding of diabetes. Studies have suggested that LRH-1 may be implicated in the pathogenesis of type 2 diabetes mellitus (T2DM). Altered expression or activity of LRH-1 has been observed in animal models of diabetes and in individuals with T2DM. LRH-1 dysregulation may contribute to insulin resistance, impaired glucose tolerance, and other metabolic abnormalities associated with diabetes.

[Dr. Ray Blind](https://www.vanderbilt.edu/csb/faculty-core/ray-blind/) is a professor with Vanderbilt University Medical Center and School of Medicine. Part of the focus of Dr. Blind's research is identifying compounds that target nuclear signaling enzymes implicated in cancer and diabetes. LRH-1 protein is of interest to many researchers due to its association with antidiabetic effects.

![image](https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/eebf192c-ca97-43b3-8251-7c0f8034fa3a)

**Figure 1.** A cartoon representation of the human liver receptor homologue-1 (LRH-1) protein.

---

## 02. Screening and Prioritizing Drug Candidates:

To identify potential activators of LRH-1 The Blind Lab performed wet lab experiments which scanned a library of 2322 compounds. During this process, Dr. Blind identified a set of 58 compounds that positively regulated LRH-1 in cells. Through further computational investigation, ***a novel method*** for ranking drug candidates as potential regulators for LRH-1 was developed. Denoted by &Delta;&Delta;G this method is given as 

<h3 align="center">
  &Delta;&Delta;G = |&Delta;G<sub>FL</sub>| - |&Delta;G<sub>LBD</sub>|
</h3>

where

<ol>
&Delta;G<sub>FL</sub> is the binding score of a docked molecule to the full-length LRH-1 structure and
</ol>

<ol>
&Delta;G<sub>LBD</sub> is the binding score of each of a docked molecule to the isolated LRH-1 ligand binding domain.
</ol>

<h3>The significance:</h3> Given the positive association between higher &Delta;&Delta;G values and LRH-1 regulation, then it would make sense that future investigations would prioritize candidates ranked by higher &Delta;&Delta;G.

## 03. Network Analysis of LRH-1 Crystal Structures:

Physical mechanisms driving the &Delta;&Delta;G were investigated by docking each of the 58 compounds to the 18 crystal structures. Of the 18, 9 were co-crystalized with small molecules and 9 with phospholipids. Then the &Delta;&Delta;G for each of the 58 compounds were averaged for each crystal structure so that a new metric denoted by &Delta;&Delta;G<sub>XSTAL</sub> was created for each structure. (Fig 2). regardless of LRH-1 regulation the phospholipid structures possessed a &Delta;&Delta;G<sub>XSTAL</sub> $\leq$ 1.0 and small molecule structures a &Delta;&Delta;G<sub>XSTAL</sub> $\geq$ 2.0.

It is noteworthy that the characteristic low vs. high &Delta;&Delta;G<sub>XSTAL</sub> values for phospholipid and small molecule structures is independent of a docked compound's LRH-1 regulation. This implies that the resulting low vs. high &Delta;&Delta;G<sub>XSTAL</sub> values must be driven by structural changes due to small molecule and phospholipid co-crystalization.

---
![image](https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/b06091e1-eaab-4426-8efa-ae64b996c13a)

**Figure 2.** Crystal structures and their averaged &Delta;&Delta;G<sub>XSTAL</sub> values.

---

## 04. Collaboration:

Previously, I had published a [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8246261/pdf/main.pdf) using network analysis to characterize conformational changes in protein structure networks for two other protein systems, constitutive androstane receptor (CAR) and ribonucleotide reductase (RNR). In this work I compared four measures of network centrality to quantify changes in residue-residue contacts from molecular dynamics (MD) simulations. Based on our discussions Dr. Blind was intrigued by the possibility of using network analysis to understand what structural changes were driving the consistency in low vs high &Delta;&Delta;G<sub>XSTAL</sub> values.

## 05. The Results:

To begin, I averaged eigenvector centrality values across all amino acids in each secondary structural element of LRH-1. Then I applied principal component analysis to analyze this multi-dimensional data. I found that the variance in PC1 formed two distinct clusters: 1) low &Delta;&Delta;G<sub>XSTAL</sub> structures bound by phospholipids and 2)  high &Delta;&Delta;G<sub>XSTAL</sub> structures bound by synthetic small molecules. (Fig 3A). This result demonstrates that the topology, or architecture, of the PSNs reflects the unique underlying structure of the two groups of crystal structures, small molecule vs. phospholipid.

Next, I examined the network edges that are unique to each of the two groups of crystal structures. These edges were then mapped onto visualizations of the 3D protein structure so that the network's relationship to the physical structure of the protein is evident. On visual inspection, clear differences exist between the low vs. high &Delta;&Delta;G<sub>XSTAL</sub>, or small molecule vs. phospholipid groups. (Fig 3B). Specifically, the nine structures with the highest &Delta;&Delta;G<sub>XSTAL</sub> values, the small-molecule group, favor Helix 6 having a position that constricts the entrance to the ligand binding pocket. Whereas the nine structures with lowest &Delta;&Delta;G<sub>XSTAL</sub> values, the phospholipid group, showed the opposite positioning which opens up the entrance to the ligand binding pocket. This would has a direct effect on the physical ability of the 58 test compounds to bind in the ligand binding pocket and would, therefore, effect their binding energy differentially. 

---
<img width="1126" alt="image" src="https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/cf8cf236-20e4-4f43-92ba-1b936495d3fe">

**Figure 3.** Eigenvector centraility clusters small molecule and phospholipid PSNs and identifies physical mechanisms associated with low vs. high &Delta;&Delta;G<sub>XSTAL</sub> values.

---

## 06. Significance of This Project to My Background:

I am not a structural biologist. I do not have a background in structural biology. However, I have demonstrated the ability to apply my analytical skill set to highly specialized fields to generate results that give explanation to complex phenomena. 
