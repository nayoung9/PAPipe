## PopPipe



 A comprehensive pipeline for population genetic analysis containing Read mapping, Variant calling, and Population genetic analysis

![fig1.png](./figure/fig1.png)

### Workflow

1. Raw read trimming
    1. Trimgalore!
2. Read mapping
    
    Select one from 
    
    1. BWA
    2. Bowtie2
3. Variant calling 
    
    Select one from 
    
    1. GATK3
    2. GATK4
    3. BCFtools call
4. Postprocessing
5. 11 popular Population genetic analysis 
    1. PCA
    2. PCA-projection
    3. Fst

### Requirements

---

- check out ./Requirements for details
- 

*Or you can use msPIPE on docker without having to prepare the environment.*

***< Recommended>***

👉[HOW TO USE msPIPE on docker](https://github.com/jkimlab/msPIPE#using-docker)

### Install PAPipe

```r
git clone https://github.com/jkimlab/PAPipe.git
```

### Run PAPipe using the local environment

```r
/Path_to_PAPipe/Programs/bin/main.py -p main.param.txt -s main.sample.txt - -o OUTDIR
```

### Run PAPipe using Docker image

```r

```