# PredLMM

## Notebook Description

* The jupyter notebook titled as "PredLMM_notebook" contains all the steps for implementing PredLMM on an example dataset provided in "Data" folder. The notebook reads the phenotype, the covariate, and the GCTA GRM files and estimates heritability based on those. 

* The PredLMM algorithm requires only a few particular blocks of the Genetic Relationship Matrix (GRM) and thus, computing the full GRM is not necessary. In the notebook named "PredLMM_notebook_with_GRM_computation_included", we explain how one can compute only the blocks of the GRM necessary for fitting the PredLMM algorithm and perform the subsequent analysis. We also allow incorporating user-specified SNP-weights e.g., LD-based weights computed using the software LDAK5 into the estimation of the GRM-blocks.

* The main module containing all the necessary python functions can be found inside the folder named "PredLMM". 


## Data Description

The example data files provided are generated following the Section simulation study 1 of the main manuscript. In the folder named "Data", there are multiple files, 

* a phenotype file: example_pheno.csv
* a covariate file: example_covar.csv
* PLINK Binary files: example_geno (.bed, .bim, .fam)
* GCTA GRM files: example_grm (.grm.id, .grm.bin, .grm.N.bin)
* LD-based SNP-weights: weights.all.

There are 5000 individuals and 10,000 SNPs. The first two columns of the phenotype and the covariate files have the family ID (FID) and individual ID (IID) of each individual. The phenotype file has a single phenotype and the covariate file has a single covariate. With the binary files, the GRM files have been computed using GCTA. It is to be craefully noted that the order of the individuals in all the files (phenotype, covariate, GRM) have to be the same.


The file "weights.all" contains the LD-based weights of every SNP computed using the software LDAK5. This file and the bed-format SNP genotype file are only used in the notebook, "PredLMM_notebook_with_GRM_computation_included".


## Code Description

In most cases, one should compute the GRM files first with the binary files using the GCTA software. Then, follow the jupyter notebook, "PredLMM_notebook" for estimating heribaility and variance of a phenotype adjusting for the availble covariates. However, it would be worth using "PredLMM_notebook_with_GRM_computation_included" for a more streamlined analysis without needing to use the GCTA software and for incorporating special SNP-weights in the GRM computation. The weights need to be pre-computed and provided separately.

In both the notebooks, we estimate the heritability and variance of the phenotype twice:

* first, by fitting a LMM only with a random subsample of the individuals (the size of which can be varied by the user) and 
* second, by fitting the PredLMM algorithm treating the selected subsample as the set of knots.

In our example, we considered "subsample_size" (the size of the knot-set) to be 1000. We have found using 20% of the total population size as knots to be generally reliable. One can increase this size depending upon the computational resources. 


### References

1. Speed, D., Hemani, G., Johnson, M. R., & Balding, D. J. (2012). Improved heritability estimation from genome-wide SNPs. The American Journal of Human Genetics, 91(6), 1011-1021.

2. Yang, J., Lee, S. H., Goddard, M. E., & Visscher, P. M. (2011). GCTA: a tool for genome-wide complex trait analysis. The American Journal of Human Genetics, 88(1), 76-82.

