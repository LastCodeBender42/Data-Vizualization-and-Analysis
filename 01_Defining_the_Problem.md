# Defining the Problem:

**Background:** Dr. Ray Blind is a professor with Vanderbilt University Medical Center and School of Medicine. Among other things, Dr. Blind's research focuses on the development of novel compounds targeting nuclear signaling enzymes in cancer and diabetes. One of the proteins of interest is the liver receptor homologue-1 (LRH1) protein. LRH-1 activation is associated with antidiabetic effects. After scanning a library of 2322 molecules, Dr. Blind identified a set of 58 that regulated LRH1. Through further computational investigation a potentially novel scoring mechanism for ranking drug candidates as potential regulators for LRH1 was developed. The rank is denoted by &Delta;&Delta;G* and is given by 

<h3 align="center">
  &Delta;&Delta;G* = |&Delta;G<sub>small molecule</sub>| - |&Delta;G<sub>phospholipid</sub>|
</h3>

where

<ol>
&Delta;G<sub>small molecule</sub> is the total averge binding score of each of the 58 molecules to LRH1 structures bound with small molecules and
</ol>

<ol>
&Delta;G<sub>phospholipid</sub> is the total avaerged binding score of each of the 58 molecules to LRH1 bound with phospholipid molecules.
</ol>

The implication is that since higher &Delta;&Delta;G* has a significant positive correlation with LRH1 regulation, then of the 58 candidates it follows that further investigation would focus on those with higher &Delta;&Delta;G*.

However, among the questions that remain to be answered. One question involves the categorical difference in the averaged &Delta;&Delta;G. Why would each of these 58 candidates have a lower &Delta;&Delta;G for LRH1 structures bound to small molecules as opposed to bound to phospholipids (Figure 1)? 

![image](https://github.com/LastCodeBender42/Data-Vizualization-and-Analysis/assets/159676076/b06091e1-eaab-4426-8efa-ae64b996c13a)

It is a matter of empirical observation that is the case, but what is the physical mechanism that drives that difference? My task was to use statistical and network approaches to uncover the physical associations to answer that question.
