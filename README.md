# circle-enrich-filter

Pipeline to identify candidate circular regions in Circle-seq short-read paired-end sequecing data.
Developed by Richard Koche, adapted to BIH cluster by @haasek and maintained by @madagiurgiu25.

- [Installation](#installation)
- [Usage](#usage)
- [Run circle-enrich-filter example](#run-circle-enrich-filter)
- [Citation](#citation)
- [License](#license)

## Installation <a name="installation"></a> 

Prequisites are conda, python==2.7 and pgltools v2.2.0.

### 1. Create conda environment

This conda installation will download the following dependencies:

- bedtools=2.29.2
- deeptools=3.1.3
- homer=4.11
- openjdk=11.0.1
- picard=2.22.8
- python=2.7.15


```
# create conda environment
git clone https://github.com/henssen-lab/circle-enrich-filter.git
cd circle-enrich-filter
mamba env create -f circleEnrich_env.yml
```

### 2. Install pgltools 

```
git clone https://github.com/billgreenwald/pgltools.git
# use the v2.2.0 version
export PATH=$PWD/pgltools/sh:$PATH
```

## Usage  <a name="usage"></a>

The tool requires as input mapped reads. 

```
Usage: bash run_CircleEnrichFilter.sh [OPTION..] -i <reads.bam> -o <outdir>
circle-enrich-filter version 1.0.0

Find enriched regions from Circle-seq paired-end short-read sequencing data.
Options:
-i	Input bam file.
-o	Output directory.
-s	Number of circle-supporting (split and/or outward facing) reads at edge of each putative circle (default=2)
-m	Number of bp for initial enriched region merging; based on tests in neuroblastoma data
-@	Number of threads (default=4)
-h	Help
-V	Print program version

```


## Run circle-enrich-filter example <a name="run-circle-enrich-filter"></a>

Run test example using the `2:14508020-18508849` region from a CHP212 cellline sequenced using the Circle-seq Illumina sequencing.

```
bash run_CircleEnrichFilter.sh -i example/output/chp212_2_14508020_18508849.bam -o example/2_14508020_18508849.fa 
```

This will generate a file `example/output/Regions_chp212_2_14508020_18508849.enriched.merged.b2bRefined.Counts.ThreshFinal.bed`

| column  | description |
|---------|--------------|
| 1       | reference sequence name |
|
| 2       | start position |
| 
| 3       | end position |
|
| 4       | edge counts (split-reads spanning the junction) |
|
| 5       | all counts (coverage all reads spanning the junction) | 


## Citation <a name="citation"></a>

Koche, R.P., Rodriguez-Fos, E., Helmsauer, K. et al. Extrachromosomal circular DNA drives oncogenic genome remodeling in neuroblastoma. Nat Genet 52, 29-34 (2020). 
[https://doi.org/10.1038/s41588-019-0547-z](https://www.nature.com/articles/s41588-019-0547-z)


### License <a name="license"></a>

Circle-enrich-filter is distributed under the GNU General Public License v3.0. Consult the accompanying [LICENSE](https://github.com/henssen-lab/circle-enrich-filter/blob/main/LICENSE) file for more details.


--------

Two input parameters are: 1) bam file (in which circular regions will be detected), 2) output folder

Line 39 contains threshold for edge reads. Currently set to 0, can be increased (set to 2 e.g.) for bulk sequencing.

Lines 277/278 need to be changed if a different reference genome build is used. Current setting is correct for hs37d5 (line 278),
needs to be switched to line 277 for hg19.

All needed dependencies can be imported with the provided yml file, except for pgltools which needs to be obtained from https://github.com/billgreenwald/pgltools and added to the PATH in line 32.
