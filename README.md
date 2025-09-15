# multi-omics-
### Download TCGA-BRCA RNA (Transcriptome), DNA methylation data (DNA methylome) and Mutation data (MAF) along with the clinical data 
#### RNA data (Transcriptome)
query_rna <- GDCquery(
  project = "TCGA-BRCA",
  data.category = "Transcriptome Profiling",
  data.type = "Gene Expression Quantification",
  workflow.type = "STAR - Counts" 
)
GDCdownload(query_rna)
rna_data <- GDCprepare(query_rna)

#### DNA methylation data (DNA methylome)
query_meth <- GDCquery(
  project = "TCGA-BRCA",
  data.category = "DNA Methylation",
  data.type = "Methylation Beta Value",
  platform = "Illumina Human Methylation 450"
)
GDCdownload(query_meth, method = "api", files.per.chunk = 5)
meth_data <- GDCprepare(query_meth)

#### Mutationa data (MAF)
query_mut <- GDCquery(
  project = "TCGA-BRCA",
  data.category = "Simple Nucleotide Variation",
  data.type = "Masked Somatic Mutation",
  workflow.type = "Aliquot Ensemble Somatic Variant Merging and Masking"
)
GDCdownload(query_mut, method = "client")
mut_data <- GDCprepare(query_mut)

#### Subset all data sets for matched samples across the datasets to be able to integrate them 

