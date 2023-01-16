# circle-enrich-filter

Pipeline to identify candidate circular regions in Circle-seq short-read paired-end sequecing data.
Developed by Richard Koche, adapted to BIH cluster by @haasek and maintained by @madagiurgiu25.

- [Installation](## Installation)
- [Run circle-enrich-filter](## Run circle-enrich-filter)
- [Citation](## Citation)
- [License](### License)

## Installation 

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
## Run circle-enrich-filter

The command for running `circle-enrich-filter`:

```
conda activate circleEnrich
bash run_CircleEnrichFilter.sh
```

Run test example:

```
bash example/circ0.bam example/output/circ0 example/ref.fa 
```

## Citation

Koche, R.P., Rodriguez-Fos, E., Helmsauer, K. et al. Extrachromosomal circular DNA drives oncogenic genome remodeling in neuroblastoma. Nat Genet 52, 29-34 (2020). 
[https://doi.org/10.1038/s41588-019-0547-z](https://www.nature.com/articles/s41588-019-0547-z)


### License

Circle-enrich-filter is distributed under the GNU General Public License v3.0. Consult the accompanying [LICENSE](https://github.com/henssen-lab/circle-enrich-filter/blob/main/LICENSE) file for more details.


--------

Two input parameters are: 1) bam file (in which circular regions will be detected), 2) output folder

Line 39 contains threshold for edge reads. Currently set to 0, can be increased (set to 2 e.g.) for bulk sequencing.

Lines 277/278 need to be changed if a different reference genome build is used. Current setting is correct for hs37d5 (line 278),
needs to be switched to line 277 for hg19.

All needed dependencies can be imported with the provided yml file, except for pgltools which needs to be obtained from https://github.com/billgreenwald/pgltools and added to the PATH in line 32.
