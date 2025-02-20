# 🧬 Bioinformatics Project: Sequence Analysis

## 📌 Project Overview

This project focuses on analyzing sequencing data from the *Saccharomyces cerevisiae* genome using bioinformatics tools and techniques. The primary goal is to understand sequencing biases, base composition, and quality assessment while developing scripts to clean and process sequencing reads.

## 🎯 Objectives
- Install and utilize bioinformatics libraries such as **Biopython, NumPy, and Matplotlib**.
- Analyze sequencing data obtained from **Illumina HiSeq 2000**.
- Understand sequencing quality variations and biases.
- Implement a **Python-based sequence cleaning algorithm**.
- Compare observed **GC content** with known values.
- Visualize sequencing read characteristics through **plots and statistical analysis**.

## 🛠️ Tools & Technologies
- **Python** 🐍
- **Biopython** for sequence parsing 🧬
- **NumPy** for numerical analysis 📊
- **Matplotlib** for data visualization 📈
- **FASTQ format** for sequencing data
- **Illumina HiSeq 2000** as the sequencing platform

## 📂 Project Structure
```
Bioinformatics_Project/
│── README.md                  # Project documentation
│── sequence_analysis.py        # Python script for analysis
│── data/
│   ├── SRR800768_1.fastq.gz   # Raw sequencing reads (sample 1)
│   ├── SRR800768_2.fastq.gz   # Raw sequencing reads (sample 2)
│── results/
│   ├── base_composition.png   # Base composition visualization
│   ├── phred_scores.png       # Quality score distribution
│   ├── cleaned_reads.fastq    # Cleaned sequencing data
│── references.md              # Literature and sources
```

## 🔬 Data Analysis
### **1. Libraries Installation**
To install required dependencies, use the following commands:
```bash
python3 -m ensurepip --upgrade
python3 -m pip install --upgrade pip
python3 -m pip install Bio Numpy Matplotlib
```

### **2. Sequencing Data Overview**
- **Sequencing Platform**: Illumina HiSeq 2000
- **Library Type**: Paired-end
- **Molecule Type**: Genomic DNA
- **File Format**: FASTQ

### **3. Key Questions & Findings**
#### **Read Characteristics**
- Number of reads: **100,000 per file**
- Read length: **101 bases**

#### **Base Composition & Biases**
- Initial AT bias detected in the first **10 bases** due to sequencing artifacts.
- Base composition stabilizes after the initial positions.
- Observed GC content:
  - *SRR800768_1*: **37.20%**
  - *SRR800768_2*: **37.12%**
  - Known GC content for *S. cerevisiae*: **38-40%**

#### **Quality Score Analysis**
- **Phred scores** decline towards the end of reads.
- **Signal decay, phasing effects, and sequencing errors** contribute to quality loss.
- **Solution**: Implement a **cleaning algorithm** to trim low-quality bases and remove unreliable reads.

## 🏗️ Read Cleaning Algorithm
To improve data quality, the following **Python script** is implemented:
```python
from Bio import SeqIO
import numpy as np

def clean_reads(input_file, output_file, quality_threshold=20, min_length=50):
    cleaned_records = []
    for record in SeqIO.parse(input_file, "fastq"):
        qualities = record.letter_annotations["phred_quality"]
        trimmed_seq = record.seq[:len(qualities)]
        if len(trimmed_seq) >= min_length and min(qualities) >= quality_threshold:
            cleaned_records.append(record)
    
    with open(output_file, "w") as out:
        SeqIO.write(cleaned_records, out, "fastq")
```
- **Trims low-quality bases (<20)**
- **Removes short reads (<50 bases)**
- **Generates clean paired and singleton files**

## 📊 Visualizations
- **Base Composition Across Reads**
- **Phred Score Distribution**
- **Read Length Distribution Before & After Cleaning**

## 📄 References
- Kozerewa et al., 2009: *Illumina library preparation artifacts lead to AT bias.*
- Liti et al., 2009: *Yeast genome evolution and variation in AT-rich regions.*
- Ewing & Green, 1998: *Phred: base-calling accuracy and sequencing quality.*
- Nikolenko et al., 2013: *BFC: Bayesian error correction for Illumina sequencing.*

## 📩 Contact
For any inquiries, contact **Yann Keita** at **yatkeit@yahoo.fr**.

---
This project serves as a **bioinformatics pipeline** for sequencing data quality control, providing insights into sequencing biases and error correction techniques.
