# PAPipe: a comprehensive pipeline for population genetic analysis

![](./figures/fig1.png)

### Main workflow

1. Read trimming (by [Trim Galore](https://www.bioinformatics.babraham.ac.uk/projects/trim_galore/))
2. Read mapping (by BWA or Bowtie2)
3. Genetic variant calling (by GATK3, GATK4 or BCFtools)
4. Data filtering and format converting (by PLINK v1.9)
5. Population genetic analyses
    - Principal component analysis (by PLINK v1.9 or v2.0)
    - Phylogenetic tree analysis (by SNPhylo)
    - Population tree analysis (by TreeMix)
    - Population structure analysis (by ADMIXTURE)
    - Linkage disequilibrium decay analysis (by PopLDdecay)
    - Selective sweep analysis (by SweepFinder2)
    - Population admixture analysis (by AdmixTools)
    - Pairwise sequentially Markovian coalescent analysis (by psmc)
    - Multiple sequentially Markovian coalescent analysis (by msmc2)
    - Fixation index analysis (by VCFtools)

---

### Install PAPipe image

```bash
wget http://bioinfo.konkuk.ac.kr/PAPipe/bin/PAPipe.tar.gz
docker load -i ./PAPipe.tar.gz

#Check if the image loaded well 
docker image ls
```

### Run PAPipe

**Setting local input directory for running the PAPipe** 

```bash
mkdir RUN_DOCKER/
cd RUN_DOCKER/

mkdir data/
cd data/

mkdir ref/
mkdir input/
```

- Set user reference data in `…/RUN_DOCKER/data/ref`
    - reference genome assembly (~fa.gz)
    - reference DBSNP vcf (~vcf.gz)
- Set user input data in `.../RUN_DOCKER/data/input`
    - Reads or alignments should be in the subdirectory named as user input population names
        - `.../RUN_DOCKER/data/input/population1/`
        - `.../RUN_DOCKER/data/input/population2/`

**Running docker container mounting local data directory** 

```bash
docker run -v [absolute path of local RUN_DOCKER/]:/RUN_DOCKER/  -it pap_docker:latest
```

→ You can generate the parameter file easily at here : [PAPipe Parameter genetator](http://bioinfo.konkuk.ac.kr/PAPipe/parameter_builder/)

→ Check out more details about parameter files : [Parameters](./Parameters/parameter_generator.md)

**Running PAPipe inside the docker container** 

```bash
# Run in the docker container
cd /RUN_DOCKER/
python3 /PAPipe/bin/main.py  -P ./main_param.txt  -I ./main_input.txt -A ./main_sample.txt &> ./log
```

---

### Results of PAPipe

1. Trimmed read data
    - Trimmed read data for all samples
        
        ```
        /Path_to_out_directory/00_ReadQC/TrimmedData/[sample]_1_val_1.fq.gz
        /Path_to_out_directory/00_ReadQC/TrimmedData/[sample]_2_val_2.fq.gz
        
        ```
        
    - fastQC results for all samples before and after trimming
        
        ```
        /Path_to_out_directory/00_ReadQC/QC_Report_Before_Trimming/[population]/[sample]_1_fastqc.html
        /Path_to_out_directory/00_ReadQC/QC_Report_Before_Trimming/[population]/[sample]_2_fastqc.html
        
        ```
        
    - MultiQC summarized QC results for populations before and after trimming
        
        ```
        /Path_to_out_directory/00_ReadQC/QC_Report_Before_Trimming/[population]/multiqc_report.html
        
        ```
        
2. Read alignment data
    - Read mapping files for all samples
        
        ```
        /Path_to_out_directory/01_readMapping/04ReadRegrouping/[population]_[sample].addRG.marked.sort.bam
        
        ```
        
3. Variant call data
    - Variant call generated using all population sequencing data
        
        ```
        /Path_to_out_directory/02_VariantCalling/VariantCalling/[].All.variant.combined.g.vcf.gz
        
        ```
        
4. Post-processed data
    - Variant call gone through Hapmap format conversion/Plink filtering
        
        ```
        /Path_to_out_directory/03_Postprocessing/Hapmap/variant.combined.GT.SNP.flt.hapmap
        /Path_to_out_directory/03_Postprocessing/plink/[prefix].*
        
        ```
        
5. Population analysis
    1. principal component analysis (Plink 1.9)
        - PCA results
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/PCA/PCs.info
            
            ```
            
        - PCA plots of all available combination of two PCs
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/PCA/all.PCA.pdf
            
            ```
            
    2. PCA projection analysis (Plink 2)
        - PCA results
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/PCA/PCs.info
            
            ```
            
    3. Phylogenetic analysis (Snphylo)
        - .NEWICK formatted phylogenetic tree
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/SNPhylo/snphylo.ml.txt
            
            ```
            
        - Visualized phylogenetic tree
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/SNPhylo/snphylo.ml.png
            
            ```
            
    4. Treemix analysis (Treemix2)
        - Treemix results in a single PDF file
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/Treemix/Treemix.results.pdf
            
            ```
            
    5. Population structure analysis (Structure)
        - STRUCTURE results per K in .PNG files and all STRUCTURE results in a single PDF file
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/STRUCTURE/CLUMPAK/K=[n].MajorCluster.png
            
            ```
            
        - STRUCTURE results for all K in single .PDF file
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/STRUCTURE/CLUMPAK/pipeline_summary.pdf
            
            ```
            
    6. Linkage disequilibrium decay analysis (PopLDdecay)
        - Linkage disequilibrium decay results for each maximum distance parameter
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/LdDecay/[maxDist]/Plot/out.pdf
            
            ```
            
    7. Selective sweep finding analysis (SweepFinder2)
        - Selective Sweep results in point plot figures for all chromosom generated per population
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/SweepFinder2/[population]/SweepFinderOut.pdf
            
            ```
            
        - Selective Sweep results per population and per chromosome
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/SweepFinder2/[population]/[population].[chromosome].SF2out
            
            ```
            
    8. Population admixture analysis (Admixtools)
        - Admixture analysis results
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/ADMIXTOOLS/admixtools_3pop/result.out
            /Path_to_out_directory/04_Population/[running datetime]/ADMIXTOOLS/admixtools_4diff/result.out
            /Path_to_out_directory/04_Population/[running datetime]/ADMIXTOOLS/admixtools_f4stat/result.out
            /Path_to_out_directory/04_Population/[running datetime]/ADMIXTOOLS/admixtools_Dstat/result.out
            
            ```
            
    9. Pairwise sequentially Markovian coalescent analysis (PSMC)
        - Effective Size plot
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/EffectiveSize/psmc_plot.pdf
            
            ```
            
    10. Multiple sequentially Markovian coalescent analysis (MSMC)
        - Effective Size plot
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/MSMC/MSMC.pdf
            
            ```
            
    11. Fixation index analysis (Fst)
        - Fixation index results visualized in manhatton plot figures
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/Fst/[pair information]/Fst_result.pdf
            
            ```
            
        - Significant regions results of Fst analysis
            
            ```
            /Path_to_out_directory/04_Population/[running datetime]/Fst/[comparing pair information]/[comparing pair information].sig.region.txt
            
            ```
