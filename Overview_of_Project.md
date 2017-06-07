These notes were formed in re-running both LWK and MKK.

**POP** represents any of the 7 HapMap3 Populations used.

1) a) Copy the HapMap3 Genotype Data into own directory.
    `/home/wheelerlab1/Data/Stranger_et_al_pop_eQTLs/HapMap3-genotypes/hapmap3_r2_b36_fwd.consensus.qc.poly.bed`
    
    `/home/wheelerlab1/Data/Stranger_et_al_pop_eQTLs/HapMap3-genotypes/hapmap3_r2_b36_fwd.consensus.qc.poly.bim`
    
    `/home/wheelerlab1/Data/Stranger_et_al_pop_eQTLs/HapMap3-genotypes/hapmap3_r2_b36_fwd.consensus.qc.poly.fam`
    
  b) Copy Stranger Gene Expression Data into own directory.
    /home/wheelerlab1/Data/Stranger_et_al_pop_eQTLs/7-HapMap3-pops-exp/E-MTAB-264.processed.1/POP_p3.expression
  c) Make a POP.list of the population's samples.
    Use head POP_p3_expression.txt to copy the list of the population samples
    Make the POP.list using nano by copying these samples into two identical columns
    ***Honestly could probably write an easy script for this, but it didn't take me too long to do by hand. ¯\_(ツ)_/¯***
      Example:  NA19027 NA19027
                NA19028 NA19028
                NA19031 NA19031
                NA19035 NA19035
                NA19036 NA19036
                etc.
2) Use LiftOver to update reference build from hg18 to hg19.
    a) Update the ".bed file" using R so it is in the proper format for use in LiftOver.
        This file is not the actual .bed file, but is made. Use 01_update_bed_file_liftover.R script in the Population_Expression_Prediction respository.
            Example Output File:    chr1    743267  743268  rs3115860
                                    chr1    766408  766409  rs12124819
                                    chr1    773885  773886  rs17160939
        Output file will be POP_liftOver.bed using script.
    b) Run LiftOver
        First need to download and save the hg18ToHg19.over.chain file to your directory. Also make sure it is gzipped.
            From (http://hgdownload.cse.ucsc.edu/goldenPath/hg18/liftOver/hg18ToHg19.over.chain.gz)
        liftOver POP_liftOver.bed hg18ToHg19.over.chain.gz output.bed unlifted.bed
 3) Update the HapMap3 Genotype Data files (.bed, .bim, .fam) so they are population specific.