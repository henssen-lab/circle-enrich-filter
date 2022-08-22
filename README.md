# circle-enrich-filter
Pipeline to identify candidate circular regions in sequencing data.
Developed by Richard Koche, adapted to BIH cluster by @haasek

Two input parameters are: 1) bam file (in which circular regions will be detected), 2) output folder

Line 39 contains threshold for edge reads. Currently set to 0, can be increased (set to 2 e.g.) for bulk sequencing.

Lines 277/278 need to be changed if a different reference genome build is used. Current setting is correct for hs37d5 (line 278),
needs to be switched to line 277 for hg19.

All needed dependencies can be imported with the provided yml file, except for pgltools which needs to be obtained from https://github.com/billgreenwald/pgltools and added to the PATH in line 32.
