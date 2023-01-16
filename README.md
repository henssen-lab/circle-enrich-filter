# circle-enrich-filter

Pipeline to identify candidate circular regions in Circle-seq short-read paired-end sequecing data.
Developed by Richard Koche, adapted to BIH cluster by @haasek and maintained by @madagiurgiu25.

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

# test pgltools dependency
pgltools

pgltools 2.2.0 Methods:
============================================
2D methods:
samTopgl: convert a sam file to a pgl file
formatbedpe: convert a bedpe like file to a pgl file.
formatTripSparse: convert a Triplet Sparse Matrix file set to a pgl file.
sort: sort a pgl file.  All commands below require sorted inputs
merge:  find the union of two pgl files
intersect:  find the intersection of two pgl files
window:  filter a pgl file on a specified window for either or both contact(s)
subtract:  find the parts of contacts of a pgl file that do not overlap another
closest: find the closest contacts between two pgl files
coverage:  find the coverage of a pgl files contacts on another pgl file
expand:  expand both loci for each paired-loci by a given distance
browser: format a pgl file for viewing with the UCSC Genome Browser
conveRt: format a pgl file for use with the GenomicInteractions R package
juicebox: format a pgl file for viewing with juicebox.
findLoops: output the internal region (including anchors) of each pgl
condense: output a bed file with 2 entries per pgl entry, one for each anchor
============================================
1D methods:
intersect1D: find the intersection of a pgl file and a bed file
subtract1D: find the parts of contacts from a pgl file that do not overlap regions from a bed file
closest1D:  find the closest contacts in a pgl file to a set of regions in a bed file
============================================

```

## Run circle-enrich-filter

The command for running `circle-enrich-filter`:

```

```

Run test example:

```
bash example/in.bam outputdir example/ref.fa 
```


Two input parameters are: 1) bam file (in which circular regions will be detected), 2) output folder

Line 39 contains threshold for edge reads. Currently set to 0, can be increased (set to 2 e.g.) for bulk sequencing.

Lines 277/278 need to be changed if a different reference genome build is used. Current setting is correct for hs37d5 (line 278),
needs to be switched to line 277 for hg19.

All needed dependencies can be imported with the provided yml file, except for pgltools which needs to be obtained from https://github.com/billgreenwald/pgltools and added to the PATH in line 32.
