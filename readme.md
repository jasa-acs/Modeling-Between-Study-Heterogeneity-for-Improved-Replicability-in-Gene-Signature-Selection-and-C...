# Modeling Between-Study Heterogeneity for Improved Replicability in Gene Signature Selection and Clinical Prediction


# Author Contributions Checklist Form

## Data

### Abstract

All raw data files referenced in file “code_for_submission/generate_data.R” are available in the directory “code_for_submission/data/”.  These raw data files correspond to the four datasets listed in Table 1 in the paper and apply to the case study described in the manuscript. The data files are given in their raw forms as provided in the manuscripts cited (Moffit, 2015 for example).  The file “code_for_submission/generate_data.R” takes these raw files to create the R data object used in the case study analysis.



### Availability 

All case study data is currently public and is available in “code_for_submission/data/”.  We will upload the folder “code_for_submission/” and all its subdirectories (data and code) to the authors public website upon acceptance of the manuscript.


### Description

Permissions:  All data is published and freely available.  
Licensing information: Default License
Link to data: Data will be uploaded to the authors public website upon acceptance
File format:  Multiple, including .txt (tab delimited) and excel.  We detail each raw data file below.  

v3_20140714_all_filter-14-200-genelist-TumorType_spar250.txt
	File format: Tab Delimited File
	Description: Tumor-specific gene list names from Moffitt (2015)

All_panc_20140714_withMeta2014-09-18.txt
	File format: Tab Delimited File
Description: Microarray expression values from Moffitt (2015).  Rows are genes, columns are samples

v3_20140714_all_filter-14-200-RM-classify-primaries-cells-mets-main.txt
	File format: Tab Delimited File
Description: Patient IDs and corresponding subtype calls from Moffitt (2015).  Class column: 0 = no call, 1 = Classical, 2 = Basal subtype

PAAD.183.FullSet_head.txt
	File format: Tab Delimited File
Description: List of sample names corresponding to each column of expression dataset 
from TCGA Pancreas (PAAD) found in PAAD.183.FullSet_body.txt

PAAD.183.FullSet_left.txt
	File format: Tab Delimited File
Description: List of gene names corresponding to each row of the expression dataset 
from TCGA Pancreas (PAAD) found in PAAD.183.FullSet_body.txt

PAAD.183.FullSet_body.txt
	File format: Tab Delimited File
Description: RNA-seq FPKM expression data matrix from TCGA Pancreas (PAAD). Columns are samples and rows are genes

mRNA-150_tumors-UNC_Tumor_samples_readable.csv
	File format: CSV
Description: Subtype calls pertaining to TCGA Pancreas (PAAD).  1st Column are sample IDs, third column pertains to the corresponding subtype call (Basal, Classical)

BLCA.242.Cluster.20131213.txt
	File format: Tab Delimited File
Description: RNA-seq FPKM expression data matrix from TCGA Bladder  (BLCA). Columns are samples and rows are genes.  1st three columns contain gene annotation information.  1st row contains sample names

TCGA_Subtype_Calls.txt
	File format: Tab Delimited File
Description: Subtype, demographic and clinical information from TCGA Bladder  (BLCA). Rows are samples columns are variables.  Only 1st two columns used (Sample ID and subtype) to match the expression data.  Subtypes considered are Basal vs Otherwise

20131008_trimmed.csv
	File format: CSV
Description: Microarray expression values from UNC Breast Cancer Dataset.  Rows are genes, columns are samples.  1st two columns are gene annotation information

Prat et al SupplementalData.xlsx
	File format: Excel 
Description: Sample metadata for UNC Breast Cancer Dataset.  Sample IDs in 1st column, Subtype information in 15th column.  We consider the “Basal” subtype vs otherwise. 

Annotation-44Kv2.22K.xlsx
File format: Excel 
Description: Array gene annotation information for UNC Breast Cancer Dataset.  Used to remap UCSC gene ids to those in the UNC Breast Cancer Dataset expression file to update the gene names (second column of data file) with the ones in this file. 
	
step5
File format: Rdata object 
Description: Contains final merged datasets after raw data processing using “code_for_submission/generate_data.R” , as well as TSP data matrix and subtype vector for merged studies after data processing and merging.  This is contained in the “dat” list object


##Code

###Abstract

File “code_for_submission/generate_data.R” produces the R data object that is used for the case study analysis from the raw data sources from Table 1 in the manuscript.  File “code_for_submission/main.R” lists the code to generate the simulation results (Tables 2-5, Figure 1) and also to perform the case study analysis (Figures 2-6).  File “code_for_submission/sim3.R” includes the R code to fit the pGLMM, helper functions to submit and run simulations, and helper functions to submit and run the case study results.  These functions are referenced in “code_for_submission/main.R”.  The file “code_for_submission/heatmap.3.R” contains a function to help visualized the TSP matrix shown in Figure 2.  The file “code_for_submission/run_metalasso.R” is used to run the metalasso on the case study data and calls “code_for_submission/metalasso.R”.   This code is sourced from “code_for_submission/main.R” during the case study analysis.  File “code_for_submission/tspair.tar.gz”) contains a modified version of the tspair package that prints out the enumerated list of all TSPs, and is used in “code_for_submission/generate_data.R”.  This file can be untarred and then installed using R CMD INSTALL tspair/.  File “code_for_submission/grpreg.tar.gz”) contains a modified version of the grpreg package that performs groupwise variable selection, and is used in “code_for_submission/main.R”.  This file can be untarred and then installed using R CMD INSTALL grpreg/.  

### Description 
How delivered:  R files
Licensing information: MIT License
Link to code/repository: Code (along with data) will be uploaded to the authors public website upon acceptance.  

### Optional Information 
Hardware requirements: Computing cluster platform is LSF Standard 9.1.3.0, Sep 03 2014.  Computing Environment is Red Hat Enterprise Linux 5.11.

Supporting software requirements:  gcc 4.9.2, R version 3.3.1 with packages lme4, Rcpp, RcppArmadillo, inline, mvtnorm, grpreg, bigalgebra.  Modified version of tspair package is also provided, where modification prints enumerated TSP pairs and should be installed. Modified version of the grpreg package is also provided and should be installed.



## Instructions for Use

### Reproducibility

All tables and figures from paper can be generated using “code_for_submission/main.R” and the processed R objects to directly generate figures are given in  “code_for_submission/data”. 

Below we will detail the workflow to be followed to recreate the analysis from the manuscript

First, to generate the processed data file, first run “code_for_submission/generate_data.R”.  This will generate the Rdata object “code_for_submission/data/step5”.  Alternatively, you may use the “code_for_submission/data/step5” provided to avoid the pre-processing.  Modified packages pertaining to the tspair and grpreg packages are provided and should be installed prior, as well as required R packages listed above. 

2.	Next, given the Rdata object “code_for_submission/data/step5”, we can run the main analyses for the paper, generating all paper figs and tables using “code_for_submission/main.R”.   This code file is dependent on helper functions available from “code_for_submission/sim3.R”.  Key functions include fit.dat(), which performed the MCEM fitting of the pGLMM, and select.tune(), which performs the tuning parameter selection and is a wrapper function for fit.dat().  

3.	In “code_for_submission/main.R”, the simulations and data analyses are performed in the following order in the code file:
Simulation
		Oracle Case with two known covariates, no variable selection (Tables 2-3)
		Illustration of single simulation result (Figure 1)
		Non-oracle case with two true non-zero covariates, variable selection (Table 4-5)
b)	Case Study.  
		Application of strategy 3 (pGLMM) to “dat” list object pertaining to processed
 			merged data from “step5” object in data folder.  Saved to “data/test_BIC”
Application of strategy 2 (pGLM) to “dat” list object pertaining to processed 
merged data from “step5” object in data folder. Saved to “data/test_BIC”
Application of strategy 1 (pGLM) to individual studies separately from “dat” list 
object.  Saved to “data/test_BIC” R data object
Application of the metalasso to “dat” list object pertaining to processed 
merged data from “step5” object in data folder. Saved to “data/ metalasso-out.RData”
		Generate Figure 2:  TSP heatmap, Uses “dat” list object from “data/step5”
		Generate Figure 3:  Coeficient heatmap, uses “data/test_BIC”
		Generate Figure 4:   Coefficient plots for strategies 2-3 using “data/test_BIC”
		Application of strategies 3, 2, 1 to holdout study analysis.  
Saved results to "data/real_result" Rdata object
		Generate Figure 5:  Holdout Study prediction error by strategy using results 
from  "data/real_result" and “data/ metalasso-out.RData”
Generate Figure 6:  Holdout Study prediction confidence histogram by strategy 
from  "data/real_result" and “data/ metalasso-out.RData”
4.	 Computational Run time:  Computational run time is dependent on dimension of the fixed and random effects assumed for the model being fit, as well as the tuning parameter grid dimension when performing variable selection.  Increasing sample size and number of studies also increase run time.  We simulate data from a random effects logistic regression model assuming N = 500 samples total (from 5 studies), two fixed effects, three random effects (random intercept + random slopes for each predictor) with random effect variance = 1 for each.  Applying fit.dat() to this dataset with no penalization assuming the same fixed and random effects design matrices used for the simulation (similar to the oracle simulation setup, Tables 2,3), computation time was 51.2 seconds.  Default parameters were utilized for fit.dat.  Timing was performed on a Windows 10 laptop with Intel Core i7-6500U CPU @ 2.50 GHz processor and 8 GB RAM. Exact code used for this timing is provided at the end of “code_for_submission/main.R”.  
