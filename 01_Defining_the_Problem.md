# Defining the Problem:
![image](https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/eebf192c-ca97-43b3-8251-7c0f8034fa3a)

**Figure 1.** A cartoon representation of the human liver receptor homologue-1 (LRH-1) protein.

---

## **Background:** 
LRH-1 (Liver Receptor Homolog-1), also known as NR5A2 (Nuclear Receptor Subfamily 5 Group A Member 2), plays important roles in glucose metabolism and insulin sensitivity, making it relevant to the understanding of diabetes. Studies have suggested that LRH-1 may be implicated in the pathogenesis of type 2 diabetes mellitus (T2DM). Altered expression or activity of LRH-1 has been observed in animal models of diabetes and in individuals with T2DM. LRH-1 dysregulation may contribute to insulin resistance, impaired glucose tolerance, and other metabolic abnormalities associated with diabetes.

[Dr. Ray Blind](https://www.vanderbilt.edu/csb/faculty-core/ray-blind/) is a professor with Vanderbilt University Medical Center and School of Medicine. In part, Dr. Blind's research focuses on the development of novel compounds targeting nuclear signaling enzymes in cancer and diabetes. One of the proteins of interest is the LRH-1 protein. LRH-1 activation is associated with antidiabetic effects. To identify potential activators of LRH-1 The Blind Lab performed wet lab experiments which scanned a library of 2322 compounds. Dr. Blind identified a set of 58 that positively regulated LRH-1 in cells. Through further computational investigation, a potentially novel method for ranking drug candidates as potential regulators for LRH-1 was developed. Denoted by &Delta;&Delta;G this method is given as 

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

**The significance:** Given that higher &Delta;&Delta;G positively associates with LRH-1 regulation, then further investigation should focus on candidates ranked by higher &Delta;&Delta;G.

Physical mechanisms driving the &Delta;&Delta;G were investigated by docking each compound to 18 co-crystal structures. Of the 18, 9 were co-crystalized with small molecules and 9 with phospholipids. Then the &Delta;&Delta;G for each of the 58 compounds were averaged for each crystal structure so that a new metric denoted by &Delta;&Delta;G<sub>XSTAL</sub> was created for each of the co-crystalized structures. As shown in Fig.2, regardless of LRH-1 regulation the phospholipid structures possessed a &Delta;&Delta;G<sub>XSTAL</sub> $\leq$ 1.0 and small molecule structures a &Delta;&Delta;G<sub>XSTAL</sub> $\geq$ 2.0.

---
![image](https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/b06091e1-eaab-4426-8efa-ae64b996c13a)

**Figure 2.** Crystal structures and their averaged &Delta;&Delta;G<sub>XSTAL</sub> values.

---

What is noteworthy is that these &Delta;&Delta;G<sub>XSTAL</sub> values are observed for phospholipid and small molecule structures regardless of a compound's LRH-1 regulation. This implies that the &Delta;&Delta;G<sub>XSTAL</sub> values are driven by conformational shifting due to either small molecule or phospholipid bound structures.

# The proposition:

I was invited by Dr. Blind to use my background in network analysis on protein structure networks to 
