# Hi-C library QC report

&copy; 2018 Phase Genomics Inc.

## Library statistics
<center>

| Label                                                           | Your library          | Expected values                               |
|-----------------------------------------------------------------|:---------------------:|----------------------------------------------:|
| BAM file                                                        | {BAM_FILE_PATH}         | N/A                                           |
| Number of read pairs analyzed                                   | {NUM_PAIRS}             | N/A                                           |
| Fraction of read pairs >10KB apart                              | {NUM_10KB_PAIRS}        | 0.01-0.10                                    |
| Fraction of read pairs mapping to different contigs/chromosomes | {NUM_DIFF_CONTIG_PAIRS} | 0.1-0.5 (contigs)<br>0.01-0.1 (chromosomes)      |
| Fraction of split reads                                         | {NUM_SPLIT_READS}       | 0.1-0.4 (PG libraries) 0.3+ (other libraries) |
| Fraction of zero-distance pairs                                 | {ZERO_DIST_PAIRS}       | 0-0.25                                        |
| Fraction of duplicate reads*                                 | {NUM_DUPE_READS}       | 0-0.5                                        |
| Number of total reads desired for scaffolding                                 | {NUM_READS_NEEDED}       | 100M - 500M                                        |
| Number of total reads desired for deconvolution                                 | {DECON_READS_NEEDED}       | 10M - 200M                                        |


</center>
*If this quantity is zero, see duplicate read section below.

See below for information on differences between Phase Genomics Hi-C libraries and traditional Hi-C libraries.

## Aligned mate distance histograms
!["Long range interaction histogram"]({PATH_TO_LONG_HIST})
!["Short range interaction histogram"]({PATH_TO_SHORT_HIST})


## Alignment distance statistics and plots
We briefly describe some of the statistics we compute below to aid interpretation of this report.
### Fraction of read pairs > 10KB apart
More is better.
### Fraction of read pairs mapping to different contigs or chromosomes
More is better.
### Fraction of zero-distance pairs
Less is better. Seems to be due to very short library inserts or sometimes mapping artifacts; can be an issue on some Illumina instruments such as iSeq and HiSeqX. Still, even libraries with up to 70% zero-distance pairs can yield usable results sometimes.

### Split reads
Traditionally, split reads have been a favored measure of Hi-C library quality. This is because traditional Hi-C library preparations are expected to produce many reads reading through junctions. 

Phase Genomics libraries, whether produced in our laboratory or by means of ProxiMeta &copy;, Animal, Plant, or Human kits, will have a generally lower fraction of split reads. This is because we have optimized our Hi-C protocol to enrich for slightly longer fragments around Hi-C junctions, such that each read is less likely to read through a junction even when a junction is present. This innovation improves mappability.
 
We therefore rely more heavily on metrics that directly relate to the usefulness of Hi-C reads for proximity analysis, such as the percentage of read pairs with mates mapping far away, or mapping to different contigs.

### Duplicate reads
**IMPORTANT NOTE: THE DUPLICATE FLAG IS NOT SET BY DEFAULT IN A BAM FILE. YOU NEED TO EXPLICITLY SET IT BY E.G. RUNNING SAMBLASTER ON YOUR BAM FILE. IF THE FRACTION OF DUPLICATES IS EXACTLY ZERO, IT PROBABLY MEANS THAT THE FLAG HAS NOT BEEN SET.**

Sequencing libraries frequently contain duplicate reads, due to PCR or optical issues. These are generally considered to be non-informative, and are thus bad. Higher proportions of duplicate reads are also correlated with low library complexity and poor library performance generally.