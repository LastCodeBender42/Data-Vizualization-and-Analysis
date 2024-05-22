# Drug Screening Project: Summary and Results

Drug screening methods are crucial in the process of discovering and developing new medications. These methods involve testing a large number of compounds to identify potential drugs that can interact with specific biological targets. Traditional drug screening techniques include high-throughput screening (HTS), where thousands of compounds are tested in parallel, and in vitro assays, which evaluate the biological activity of compounds in cell cultures or biochemical assays. Recently, network analysis has emerged as a powerful tool in drug discovery. By leveraging computational and mathematical models, network analysis can map and analyze the complex interactions within biological systems. This approach helps identify key nodes and pathways that are critical in disease processes, thereby highlighting potential targets for drug intervention. Additionally, network analysis can predict off-target effects and drug repurposing opportunities by examining the connectivity and relationships between different biological entities. Combining traditional drug screening methods with network analysis enhances the efficiency and effectiveness of the drug discovery process, ultimately leading to the development of more targeted and safer therapeutic options.

## Contents:
- # [LRH-1: A Target for Diabetes Treatment](#lrh-1-a-target-for-diabetes-treatment)
- Screening and Prioritizing Drug Candidates
- &Delta;&Delta;G<sub>XSTAL</sub> for Small Molecules vs. Phospholipids
- Network Analysis of LRH-1 Protein Structure Networks
- Network Analysis Identifies Mechanisms Driving &Delta;&Delta;G<sub>XSTAL</sub>
- Relevance to My Professional Experience
# [link](#what-the-hell)

## LRH-1: A Target for Diabetes Treatment

Liver receptor homolog-1 (LRH-1) is a nuclear receptor that plays a significant role in regulating various metabolic processes, including glucose homeostasis, making it a promising target for diabetes treatment. Studies have suggested that LRH-1 may be implicated in the pathogenesis of type 2 diabetes mellitus (T2DM). Altered expression or activity of LRH-1 has been observed in animal models of diabetes and in individuals with T2DM. LRH-1 dysregulation may contribute to insulin resistance, impaired glucose tolerance, and other metabolic abnormalities associated with diabetes.

Research into LRH-1-targeted drugs involves sophisticated drug screening methods to identify compounds that can modulate this receptor's activity. HTS techniques are employed to test vast libraries of chemical compounds for their ability to regulate LRH-1 activity. Additionally, network analysis is utilized to understand the intricate biological pathways associated with LRH-1, helping to pinpoint its influence on glucose metabolism and identify potential side effects. By focusing on LRH-1, researchers aim to develop novel therapeutics that can enhance insulin sensitivity and glucose uptake, thereby alleviating symptoms of diabetes. The integration of these advanced screening methods and computational analyses accelerates the discovery of effective LRH-1 modulators, offering new hope for diabetes management and treatment.

[Dr. Ray Blind](https://www.vanderbilt.edu/csb/faculty-core/ray-blind/) is a professor with Vanderbilt University Medical Center and School of Medicine. Part of the focus of Dr. Blind's research is identifying compounds that target nuclear signaling enzymes implicated in cancer and diabetes. LRH-1 protein is of interest to many researchers due to its association with antidiabetic effects.

![image](https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/eebf192c-ca97-43b3-8251-7c0f8034fa3a)

**Figure 1.** A cartoon representation of the human liver receptor homologue-1 (LRH-1) protein.

---

## Screening and Prioritizing Drug Candidates

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

## &Delta;&Delta;G<sub>XSTAL</sub> for Small Molecules vs. Phospholipids

Physical mechanisms driving the &Delta;&Delta;G were investigated by docking each of the 58 compounds to the 18 crystal structures. Of the 18, 9 were co-crystalized with small molecules and 9 with phospholipids. Then the &Delta;&Delta;G for each of the 58 compounds were averaged for each crystal structure so that a new metric denoted by &Delta;&Delta;G<sub>XSTAL</sub> was created for each structure. (Fig 2). regardless of LRH-1 regulation the phospholipid structures possessed a &Delta;&Delta;G<sub>XSTAL</sub> $\leq$ 1.0 and small molecule structures a &Delta;&Delta;G<sub>XSTAL</sub> $\geq$ 2.0.

It is noteworthy that the characteristic low vs. high &Delta;&Delta;G<sub>XSTAL</sub> values for phospholipid and small molecule structures is independent of a docked compound's LRH-1 regulation. This implies that the resulting low vs. high &Delta;&Delta;G<sub>XSTAL</sub> values must be driven by structural changes due to small molecule and phospholipid co-crystalization.

---
![image](https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/b06091e1-eaab-4426-8efa-ae64b996c13a)

**Figure 2.** Crystal structures and their averaged &Delta;&Delta;G<sub>XSTAL</sub> values.

---

## Network Analysis of LRH-1 Protein Structure Networks

Previously, I had published a [paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8246261/pdf/main.pdf) using network analysis to characterize conformational changes in protein structure networks for two other protein systems, constitutive androstane receptor (CAR) and ribonucleotide reductase (RNR). In this work I compared four measures of network centrality to quantify changes in residue-residue contacts from molecular dynamics (MD) simulations. Based on our discussions Dr. Blind was intrigued by the possibility of using network analysis to understand what structural changes were driving the consistency in low vs high &Delta;&Delta;G<sub>XSTAL</sub> values.

## Network Analysis Identifies Mechanisms Driving &Delta;&Delta;G<sub>XSTAL</sub> 

To begin, I averaged eigenvector centrality values across all amino acids in each secondary structural element of LRH-1. Then I applied principal component analysis to analyze this multi-dimensional data. I found that the variance in PC1 formed two distinct clusters: 1) low &Delta;&Delta;G<sub>XSTAL</sub> structures bound by phospholipids and 2)  high &Delta;&Delta;G<sub>XSTAL</sub> structures bound by synthetic small molecules. (Fig 3A). This result demonstrates that the topology, or architecture, of the PSNs reflects the unique underlying structure of the two groups of crystal structures, small molecule vs. phospholipid.

Next, I examined the network edges that are unique to each of the two groups of crystal structures. These edges were then mapped onto visualizations of the 3D protein structure so that the network's relationship to the physical structure of the protein is evident. On visual inspection, clear differences exist between the low vs. high &Delta;&Delta;G<sub>XSTAL</sub>, or small molecule vs. phospholipid groups. (Fig 3B). Specifically, the nine structures with the highest &Delta;&Delta;G<sub>XSTAL</sub> values, the small-molecule group, favor Helix 6 having a position that constricts the entrance to the ligand binding pocket. Whereas the nine structures with lowest &Delta;&Delta;G<sub>XSTAL</sub> values, the phospholipid group, showed the opposite positioning which opens up the entrance to the ligand binding pocket. This would has a direct effect on the physical ability of the 58 test compounds to bind in the ligand binding pocket and would, therefore, effect their binding energy differentially. 

---
<img width="1126" alt="image" src="https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/cf8cf236-20e4-4f43-92ba-1b936495d3fe">

**Figure 3.** Eigenvector centraility clusters small molecule and phospholipid PSNs and identifies physical mechanisms associated with low vs. high &Delta;&Delta;G<sub>XSTAL</sub> values.

---

## Relevance to My Professional Experience

I am not a structural biologist. I do not have a background in structural biology. However, I have demonstrated the ability to apply my analytical skill set to highly specialized fields to generate results that give explanation to complex phenomena. 

## What the Hell?
