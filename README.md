# 🔬 HN Protein Mutation Visualization in NDV using PyMOL

This repository provides a workflow to visualize **HN gene mutations** in **Newcastle Disease Virus (NDV)** using PyMOL. This project is part of a my PhD research effort studying low NDV from aquatic birds - viral evolution and host adaptation to chicken embryo by passaging.

## 🧠 Why is this important?

Visualizing protein mutations in 3D space is a powerful method to understand how structural changes can impact function, stability, antigenicity, or interactions with host factors. Tools like PyMOL allow researchers to map mutations onto protein structures, helping bridge the gap between genetic variation and biological consequences. This approach is commonly used in structural biology, virology, vaccine design, and drug development.

### 🎓 Example from this project:

In this project, we visualize specific amino acid mutations in the **Hemagglutinin-Neuraminidase (HN) protein** of **Newcastle Disease Virus (NDV)**. The HN protein plays a critical role in host recognition and viral spread, making it a key focus for understanding viral adaptation.

- The 3D structure of the HN protein was predicted using **ColabFold v1.5.5 (AlphaFold2 + MMseqs2)** based on the amino acid sequence from **NCBI GenBank: AAC28376.1**.
  
- The resulting structure was visualized and annotated using **PyMOL v3.1.4**, highlighting sites of interest and performing in silico mutagenesis to model amino acid changes.

**This workflow can be adapted to visualize mutations in any viral or host protein of interest.**


## 🛠 Tools Used

- 🔍 **Structure Prediction**: ColabFold v1.5.5 (AlphaFold2 + MMseqs2)  
  Based on the amino acid sequence of HN gene (NCBI GenBank: **AAC28376.1**)
- 🎨 **Visualization**: [PyMOL Version 3.1.4](https://www.pymol.org/)

---

## ⚙️ Workflow

### 1. Load the Structure
```pymol
# Load structure
load LaSota_HN.pdb

# Remove initial residues (it is not mandatory. However, it is necessary when the Colabfold predicted the amino acid sequence more than the required one)
select pia_residues, resi 1-3 and LaSota_HN
remove pia_residues

# Renumber residues to match reference
alter LaSota_HN, resi=str(int(resi)-3)
sort

#creating mutant LaSota_HN named as mutant_combined
create mutant_combined, LaSota_HN

# Hide original structure and style the new one
hide everything, LaSota_HN
color slate, mutant_combined
set surface_quality, 1

# Highlight mutation sites (I selected here random numbers as I dont want to reveal our data, but the cool thing is that you can work in indivual mutation or all mutation can also be worked at once like below)
select mutation_sites, resi 31+41+43+44+45+266+269+315+369 and mutant_combined
show surface, mutation_sites (Surface is the way to show your mutation. You can also show the mutations in different style like sticks, sphere and other. Just explore which you like)

So now we will show our mutation in compared to our refernce sequence by this process. 
# Optional: Start mutagenesis wizard (GUI)

wizard mutagenesis

# Example mutation: F31L
select target_31, resi 31
cmd.get_wizard().do_select("target_31")
cmd.get_wizard().set_mode("LEU")
cmd.get_wizard().apply()

# Optional: Color specific mutation site
color hotpink, resi 41



