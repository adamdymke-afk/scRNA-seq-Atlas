# scRNA-seq-Atlas

This project demonstrates a robust end-to-end workflow for analyzing single-cell RNA sequencing (scRNA-seq) data using the Scanpy framework. Using a dataset of 3,000 Peripheral Blood Mononuclear Cells (PBMCs) from 10x Genomics, the pipeline transforms raw count matrices into an annotated cellular atlas.

Overview 
This repository contains a complete bioinformatics pipeline for the analysis of Single-Cell RNA sequencing (scRNA-seq) data. Using a dataset of ~3,000 Peripheral Blood Mononuclear Cells (PBMCs) from a healthy donor, this project demonstrates the transition from raw count matrices to a biologically annotated cellular atlas.

The goal of this analysis is to identify distinct immune cell subpopulations and characterize their unique transcriptomic "fingerprints" using unsupervised machine learning and statistical differential expression.

Technical Workflow
The pipeline is implemented in Python using the Scanpy framework and follows the current "best practices" for single-cell analysis:
Quality Control (QC):
-Filtered low-quality cells based on gene counts and library size.
-Applied mitochondrial DNA (mtDNA) filtering ($<5\%$) to exclude apoptotic or damaged cells.
Preprocessing & Normalization:
-Total Count Normalization: Scaled cell libraries to 10,000 reads to ensure comparability across sequencing depth.
-Log-Transformation: Applied $log(x+1)$ to stabilize variance and handle the stochastic nature of gene expression.
Feature Selection:
-Identified the top 2,000 Highly Variable Genes (HVGs) to focus the model on biological signal rather than technical noise.
Dimensionality Reduction:
-PCA > Reduced the 2,000-gene feature space into the top 40 Principal Components.
-UMAP > Visualized the high-dimensional data in 2D space while preserving local and global neighbor relationships.
Clustering & Annotation:
-Leiden Algorithm > Performed unsupervised community detection to group similar cells.
-Rank Genes Groups > Conducted statistical t-tests to identify cluster-specific marker genes.

📊 Key Results & Biological Interpretation
Based on the differential expression analysis, the following immune populations were identified:

Cluster ID,   Likely Cell Type,      Key Markers
Cluster 0,    CD4+ T-cells,          "IL7R, CD3D"
Cluster 1,    CD14+ Monocytes,       "CD14, LYZ"
Cluster 2,    B-cells,               "MS4A1, CD79A"
Cluster 3,    CD8+ T-cells,          "CD8A, CCL5"
Cluster 4,    NK cells,              "GNLY, NKG7"

Prerequisites
Ensure you have Python 3.8+ installed. It is recommended to use a virtual environment.

Installation
>git clone https://github.com/your-username/scrna-seq-pbmc.git
>cd scrna-seq-pbmc
>pip install -r requirements.txt

Usage
Open the Jupyter Notebook to view the full analysis:

>jupyter notebook PBMC_Analysis.ipynb

Tools Used
Scanpy - Single-cell analysis library.
Pandas/NumPy - Data manipulation.
Matplotlib - Data visualization.
Leidenalg - Community detection for clustering.