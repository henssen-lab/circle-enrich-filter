[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)


# circle-enrich-filter

Pipeline to identify candidate circular regions in Circle-seq short-read paired-end sequecing data.
Developed by Richard Koche, adapted to BIH cluster by @haasek and maintained by @madagiurgiu25.

- [Installation](#installation)
- [Usage](#usage)
- [Run circle-enrich-filter example](#run-circle-enrich-filter)
- [Run circle-enrich-filter with PDX data](#run-pdx)
- [Citation](#citation)
- [License](#license)

## Installation <a name="installation"></a> 

Prequisites are conda and pgltools v2.2.0. Compatible with `python 2.7` and `python 3.7`.<br/>
Compatible with human (`GRCh38.p13`, `GRCh37.p13`, `hs37d5`, `hg38`, `hg19`) and mouse (`GRCm38`) genome assemblies.

### 1. Create conda environment

Choose one of the python versions to install the conda environment.

#### Option1: Python 2.7

Use `circleEnrich_env.yml` to download and install the following dependencies:

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

#### Option2: Python 3.7

Use `circleEnrich_env_py37.yml` to download and install the following dependencies:

- python==3.7
- bedtools==2.30.0
- picard==2.27.5
- samtools==1.16
- openjdk==11.0.15
- homer==4.11
- deeptools==3.5.1

```
# create conda environment
git clone https://github.com/henssen-lab/circle-enrich-filter.git
cd circle-enrich-filter
mamba env create -f circleEnrich_env_py37.yml
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

Run test example using the `2:14508020-18508849` region from CHP212 human cellline sequenced using the Circle-seq Illumina sequencing.

```
bash run_CircleEnrichFilter.sh -i example/output/chp212_2_14508020_18508849.bam -o example/2_14508020_18508849.fa 
```

The pipeline generates the all files under `example/ouput`. The final enriched regions found by `circle-enrich-filter` is [Regions.enriched.merged.b2bRefined.Counts.ThreshFinal.bed](example/output/Regions_chp212_2_14508020_18508849.enriched.merged.b2bRefined.Counts.ThreshFinal.bed). The header is described bellow:

| column  | description |
|---------|--------------|
| 1       | reference sequence name |
| 2       | start position | 
| 3       | end position |
| 4       | edge counts (split-reads spanning the junction) |
| 5       | all counts (coverage all reads spanning the junction) | 


## Run PDX samples with circle-enrich-filter <a name="run-pdx"></a>

In case you run PDX samples, please consider annotating all chromosomes from the mouse using `m.*`, .e.g `m.1` or `m.chr1`. 


## Citation <a name="citation"></a>

Koche, R.P., Rodriguez-Fos, E., Helmsauer, K. et al. Extrachromosomal circular DNA drives oncogenic genome remodeling in neuroblastoma. Nat Genet 52, 29-34 (2020). 
[https://doi.org/10.1038/s41588-019-0547-z](https://www.nature.com/articles/s41588-019-0547-z)


## License <a name="license"></a>

Circle-enrich-filter is distributed under the GNU General Public License v3.0. Consult the accompanying [LICENSE](https://github.com/henssen-lab/circle-enrich-filter/blob/main/LICENSE) file for more details.


