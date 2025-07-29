# DPFunc: accurately predicting protein function via deep learning with domain-guided structure information (2025, Nat Commun, Wang et al.)

* * *

<table><tbody><tr><td style="background-color: rgb(246, 248, 250);"><p><strong><span style="color: rgb(60, 90, 204)"><span style="background-color: rgb(246, 248, 250)">Author: </span></span></strong><span style="background-color: rgb(246, 248, 250)">Wenkang Wang; Yunyan Shuai; Min Zeng; Wei Fan; Min Li</span></p></td></tr><tr><td style="background-color: rgb(236, 243, 250);"><p><strong><span style="color: rgb(60, 90, 204)"><span style="background-color: rgb(236, 243, 250)">Source: </span></span></strong><span style="background-color: rgb(236, 243, 250)">Nature Communications (Volume: 16, Issue: 1, Pages: 70)</span></p></td></tr><tr><td style="background-color: rgb(246, 248, 250);"><p><strong><span style="color: rgb(60, 90, 204)"><span style="background-color: rgb(246, 248, 250)">DOI: </span></span></strong><span style="background-color: rgb(246, 248, 250)"><a href="https://doi.org/10.1038/s41467-024-54816-8" rel="noopener noreferrer nofollow">10.1038/s41467-024-54816-8</a></span></p></td></tr><tr><td style="background-color: rgb(236, 243, 250);"><p><strong><span style="color: rgb(60, 90, 204)"><span style="background-color: rgb(236, 243, 250)">Date: </span></span></strong><span style="background-color: rgb(236, 243, 250)">2025-01-02</span></p></td></tr><tr><td style="background-color: rgb(246, 248, 250);"><p><strong><span style="color: rgb(60, 90, 204)"><span style="background-color: rgb(246, 248, 250)">Full Text: </span></span></strong><span style="background-color: rgb(246, 248, 250)"><a href="zotero://open-pdf/0_3W2SNRK9" rel="noopener noreferrer nofollow">Wang et al. - 2025 - DPFunc accurately predicting protein function via deep learning with domain-guided structure inform.pdf</a></span></p></td></tr><tr><td style="background-color: rgb(236, 243, 250);"><p><strong><span style="color: rgb(60, 90, 204)"><span style="background-color: rgb(236, 243, 250)">Abstract: </span></span></strong><em><span style="background-color: rgb(236, 243, 250)">Computational methods for predicting protein function are of great significance in understanding biological mechanisms and treating complex diseases. However, existing computational approaches of protein function prediction lack interpretability, making it difficult to understand the relations between protein structures and functions. In this study, we propose a deep learning-based solution, named DPFunc, for accurate protein function prediction with domain-guided structure information. DPFunc can detect significant regions in protein structures and accurately predict corresponding functions under the guidance of domain information. It outperforms current state-of-the-art methods and achieves a significant improvement over existing structure-based methods. Detailed analyses demonstrate that the guidance of domain information contributes to DPFunc for protein function prediction, enabling our method to detect key residues or regions in protein structures, which are closely related to their functions. In summary, DPFunc serves as an effective tool for large-scale protein function prediction, which pushes the border of protein understanding in biological systems.</span></em></p></td></tr></tbody></table>

* * *

## 🌏Background：

“predicting protein function” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=G9YYKBBV))

“interpretability” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=TJLMVGKZ))

“structures and functions” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=BWKEYGIT))

“for accurate protein function prediction with domain-guided structure information” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=XM5JD2T7))

“detect key residues or regions in protein structures, which are closely related to their functions” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=GP6CPTQF))

“large-scale” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=SMYW9USL))

“Gene Ontology (GO) terms7, which can be divided into three ontologies: molecular functions (MF), cellular components (CC), and biological process (BP)8,9.” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=2434ETDN))

“highthroughput technology” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=WSZU5RWR))

“homology similarity” ([Wang et al., 2025, p. 1](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=1&annotation=44ISZ2X9))

“can predict high-accuracy protein structures from sequences, addressing the limitations of existing sequence-based methods for protein function prediction.” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=8QV4W9DD))

“In fact, proteins consist of many specific domains45–48, which are closely related to both their structures and functions” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=64QN8XW6))

“Since these domains are functional units responsible for specific functions, in this module, they serve as a guide to discovering significant residues in the sequences with the residue-level features generated by the first module.” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=I6ACK3AF))

“post-processing” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=52NJQWV6))

“CASP” ([Wang et al., 2025, p. 3](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=3&annotation=4EAAA7R4))

“Focal loss” ([Wang et al., 2025, p. 10](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=10&annotation=IVQ3PRTR))

## 🔬Method：

“they struggle to be applied to large-scale protein datasets or those predicted from only sequenced genomes, as there is no guarantee that additional information is available for all target proteins28” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=JFE2ANKI))

## 📜Conclusion：

“The core idea is to leverage domain information within protein sequences to guide the model toward learning the functional relevance of amino acids in their corresponding structures, highlighting structure regions that are closely associated with functions. More specifically, DPFunc first extracts residue-level features from a pre-trained protein language model and then employs graph neural networks to propagate features between residues. Simultaneously, it scans the sequences and generates domains, converting them into dense representations through embedding layers. Inspired by the transformer architecture, DPFunc introduces an attention mechanism that learns whole structures and predicts functions under the guidance of corresponding domain information.” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=Y672QSUX))  
**architecture**

## ❓Problem：

“3D coordinates” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=AEMHN73R))

“Graph Neural Networks (GNNs)” ([Wang et al., 2025, p. 2](zotero://select/library/items/RR3U6HA7)) ([pdf](zotero://open-pdf/library/items/3W2SNRK9?page=2&annotation=GJLBSXMP))

* * *