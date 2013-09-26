turbo_krigr
===========

  _Improvements for -omic Kriging R package._


## Data Input  ##

Test and time a few variations:
  - Existing plink --recode + src/readgt.r
  - Package snpStats in Bioconductor.
  - Packages gdsfmt+SNPRelate (which leverages hdf5). 

  
### Timing results ###

Using WTCC T1D data set consisting of 4900 individuals and 388548 SNPs.

gdsfmt:

    f <- function() {
      library(gdsfmt)
      library(SNPRelate)
      ## convert plink file to GDS
      gdsFile <- "wtcct1d.gds"
      snpgdsBED2GDS("data/T1DCC.bed", "data/T1DCC.fam", "data/T1DCC.bim", gdsFile)
      ## open GDS file
      genofile <- openfn.gds(gdsFile)
      g <- read.gdsn(index.gdsn(genofile, "genotype"))
    }

_Results are extremely favorable:_

    > system.time(f())
    SNPRelate: 0.9.16
    Supported by Streaming SIMD Extensions 2 (SSE2).
    Start snpgdsBED2GDS ...
    	open /home/vasya/coxlab_projects/turbo_krigr/data/T1DCC.bed in the SNP-major mode
    	open /home/vasya/coxlab_projects/turbo_krigr/data/T1DCC.fam DONE.
    	open /home/vasya/coxlab_projects/turbo_krigr/data/T1DCC.bim DONE.
    Wed Sep 25 15:43:32 2013 	store sample id, snp id, position, and chromosome.
    	start writing: 4900 samples, 388548 SNPs ...
     	Wed Sep 25 15:43:32 2013	0%
     	Wed Sep 25 15:43:34 2013	100%
    Wed Sep 25 15:43:39 2013 	Done.
       user  system elapsed 
      9.396   2.092  16.432 


snpMatrix:

_Looks like I'll need to upgrade my Ubuntu and R to get the latest Bioconductor to use this package._

    library(snpMatrix)
    read.plink("data/T1DCC.bed", "data/T1DCC.bim", "data/T1DCC.fam")


plink + scan():

_Ask keston for timing results._
