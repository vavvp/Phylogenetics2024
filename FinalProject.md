# Report on Phylogenetic Analysis of Klebsormidium and Interfilum Genera Using Nuclear (ITS1) and Chloroplast (rbcL) Markers

## Introduction
In this study, we examine the phylogenetic relationships among species of the Klebsormidium and Interfilum genera by analyzing nuclear (ITS1) and chloroplast (rbcL) genetic markers. The hypothesis suggests that species divergence within these markers is associated with adaptations to terrestrial environments, reflecting evolutionary transitions required for plant life on land.

**Hypothesis:** Species differences in nuclear (ITS1) and chloroplast (rbcL) marker sequences are related to adaptation to terrestrial conditions, reflecting evolutionary changes tied to the transition from aquatic to terrestrial life.

**Rationale:** The shift of plants from aquatic environments to land necessitated adaptations such as mechanisms to prevent desiccation, changes in photosynthetic activity, and other physiological modifications. The ITS1 and rbcL markers may have undergone different evolutionary pressures, reflecting adaptations required for survival in terrestrial habitats.

## Methodology
**Sample Selection:** Organisms selected for this analysis included representatives from the Klebsormidium and Interfilum genera with sequences obtained for ITS1 and rbcL markers.

```
import os
import glob

def replace_fasta_id_with_filename(fasta_file):
    file_name = os.path.splitext(os.path.basename(fasta_file))[0]
    with open(fasta_file, 'r') as file:
        lines = file.readlines()

    with open(fasta_file, 'w') as file:
        for line in lines:
            if line.startswith('>'):
                new_id = f">{file_name}\n"
                file.write(new_id)
            else:
                file.write(line)
fasta_files = glob.glob('/content/*.fasta')

for fasta_file in fasta_files:
    replace_fasta_id_with_filename(fasta_file)
```    
**Data Extraction and Processing:** Sequences were downloaded from GenBank, and the regions corresponding to ITS1 and rbcL markers were extracted using Biopython. The extracted sequences were combined by marker to generate comprehensive ITS1 and rbcL datasets.
```
from Bio import SeqIO

input_file = "/content/Interfilum_massjukiae_2102.fasta"
output_file = "/content/Interfilum_massjukiae_2102_EXTRACT.fasta"

with open(output_file, "w") as output_handle:
    for record in SeqIO.parse(input_file, "fasta"):
        # Извлекаем регион ITS1 (позиции  72818..74245, учитывая Python-счет от 0)
        ITS1_seq = record.seq[72817:74245]
        ITS1_record = record[:]
        ITS1_record.seq = ITS1_seq
        SeqIO.write(ITS1_record, output_handle, "fasta")
```
**Sequence Alignment:** Alignments for each marker were performed independently using the MAFFT software with the `--auto` setting, producing `aligned_ITS.fasta` and `aligned_rbcL.fasta` for subsequent analyses.

## Phylogenetic Tree Construction
### Distance-based Tree
FastTree was used to construct initial phylogenetic trees with the Jukes-Cantor model, which provides a simple model suitable for broad evolutionary insights.
**Command used:**
```
FastTree -nt aligned_ITS.fasta > ITS1.tree
FastTree -nt aligned_rbcL.fasta > rbcL.tree
```

### Maximum Likelihood Tree
The maximum likelihood approach was conducted using IQ-TREE with the GTR+I+G model, incorporating 1000 bootstrap replicates to assess branch support.
**Command used:**
```
iqtree -s aligned_ITS.fasta -m GTR+I+G -B 1000 -nt AUTO
iqtree -s aligned_rbcL.fasta -m GTR+I+G -B 1000 -nt AUTO
```

## Results
### Distance-Based Tree (Neighbor-Joining) Results
**ITS1 Marker:**  
The distance-based tree generated for the ITS1 marker displayed distinct clusters for species within the Klebsormidium and Interfilum genera. Several branches showed robust bootstrap support, suggesting evolutionary coherence within groups.

**rbcL Marker:**  
The rbcL tree constructed using distance methods also revealed clear clustering among species, with terrestrial species grouping together in clades with high bootstrap support. This clustering aligns with the hypothesis that rbcL sequences may reflect adaptations for terrestrial survival.

### Maximum Likelihood Tree Results
**ITS1 Marker:**  
The ITS1 maximum likelihood tree exhibited high bootstrap support in clusters comprising land-adapted species, which may support the hypothesis of nuclear marker divergence correlating with terrestrial adaptation.

**rbcL Marker:**  
Similar to the ITS1 results, the rbcL maximum likelihood tree indicated well-supported clusters among land-adapted species, suggesting chloroplast marker evolution may also reflect terrestrial adaptations.

## Discussion
### Tree Structure and Hypothesis Support
Both the ITS1 and rbcL trees demonstrate clustering that supports the hypothesis of genetic differentiation related to terrestrial adaptation. In particular, species within the Klebsormidium genus, known for terrestrial adaptations, consistently grouped together with high bootstrap values in both nuclear and chloroplast analyses.

### Bootstrap Support
The high bootstrap values across the terrestrial species clades strengthen the reliability of these relationships. The strong support for land-adapted species clusters may indicate evolutionary pressures on both ITS1 and rbcL regions that align with adaptation to land.

### Evolutionary Distance and Cluster Analysis
Analysis of evolutionary distances within the trees suggests that species with higher adaptation to terrestrial environments exhibit greater sequence divergence, particularly in the ITS1 marker. This divergence may reflect nuclear changes that support adaptations to terrestrial stressors, such as desiccation and increased sunlight exposure.

### Comparative Marker Analysis
While both markers exhibit patterns consistent with terrestrial adaptation, the ITS1 marker, located in the nuclear genome, might be more influenced by cellular and environmental stressors compared to the chloroplast marker rbcL, which is more directly involved in photosynthetic functions. This difference could indicate varied selective pressures acting on these markers in terrestrial environments.

## Conclusion
The phylogenetic analysis of Klebsormidium and Interfilum genera based on ITS1 and rbcL markers reveals clustering patterns that support the hypothesis of genetic adaptations related to terrestrial environments. The high bootstrap values in land-adapted species clades underscore the reliability of these phylogenetic relationships. The study suggests that both nuclear and chloroplast markers have likely evolved in response to the selective pressures associated with land colonization, with ITS1 possibly showing more pronounced divergence due to its nuclear location.

These results contribute to our understanding of plant evolutionary adaptations as they transitioned from aquatic to terrestrial habitats, providing insights into the molecular changes accompanying this significant ecological shift. Future studies could further investigate the specific adaptive mutations within ITS1 and rbcL sequences that enabled survival in land conditions.
