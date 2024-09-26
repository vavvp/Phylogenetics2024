# Phylogenetic Analysis of Human mtDNA Data

## 1. Construction of the Evolutionary Tree

### Objective:

The goal of this task was to construct an evolutionary tree based on human mitochondrial DNA (mtDNA) sequences. For this analysis, I used MAFFT for sequence alignment and FastTree for phylogenetic tree construction. The tree includes bootstrap support values to ensure the reliability of the nodes.

### Tools and Methods:

- **Sequence Alignment**: MAFFT (Multiple Alignment using Fast Fourier Transform)
- **Tree Reconstruction**: FastTree (for Neighbor-Joining tree generation)
- **Bootstrap Support**: FastTree provides local support values (approximate bootstrap) for assessing node confidence.

### Procedure:

1. **Data Preparation**:  
   All `.fasta` files were gathered in the working directory. To simplify the analysis, I replaced each sequence ID with the filename, ensuring easy tracking during tree construction. This was achieved using the following Python script:
   
   ```python
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
## Sequence Alignment using MAFFT

After concatenating all `.fasta` files into a single input file (`input.fasta`), MAFFT was used for alignment:

```bash
mafft --auto input.fasta > output_mafft.fasta
```

The --auto option allows MAFFT to automatically choose the best alignment strategy based on input data size.

### Tree Construction with FastTree

Once the alignment was generated, FastTree was used to construct the Neighbor-Joining tree and calculate bootstrap support values:

```bash
FastTree -quote output_mafft.fasta > output_fasttree.nwk
```

The resulting tree is in Newick format (output_fasttree.nwk), with bootstrap values included.

### Results

The constructed tree is a Neighbor-Joining tree with bootstrap support values. The nodes with higher bootstrap values indicate higher confidence in the evolutionary relationship between the mtDNA sequences. The tree topology highlights the evolutionary divergence of human populations based on mtDNA.
