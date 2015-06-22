---
layout: lesson
root: .
title: Manipulating VCF files
minutes: --
---

## Learning Objectives

    In this lesson you will learn how to manipulate VCF files. For this exercises we will use publicly available data from the 1000 Genomes  Project.

## Lesson

## File format

The file format is explained in detail [here](http://samtools.github.io/hts-specs/VCFv4.1.pdf)

To reduce the size of the files, VFCs are usually compressed and indexed using the bgzip and tabix command from SAMTOOLS http://www.htslib.org/doc/tabix.html

VCFTools and VCFLib are two software tools commonly used for handling VCF data files. This lesson gives instructions on installing these tools on a Linux system.

## Downloading data
An example VCF file can be downloaded from the [1000 Genomes Project](ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/phase1/analysis_results/integrated_call_sets/ALL.chr2.integrated_phase1_v3.20101123.snps_indels_svs.genotypes.vcf.gz).

## vcftools

VCFTools can be downloaded [here](http://sourceforge.net/projects/vcftools/files/). Extract the content of the downloaded vcftools_x.y.z.tar.gz file (*note*: x.y.z is the version of the file downloaded). Navigate to the folder where files have been extracted, and type *make* to compile the files.

```
$ cd vcftools_x.y.z
$ make
```
Once the compilation process is complete, the perl scripts and cpp executable will be installed in the folder: *vcftools_x.y.z/bin/*.

## vcflib

VCFLib can be downloaded [here](https://github.com/ekg/vcflib). To download and compile vcflib, use the following commands:

```
$ git clone --recursive git://github.com/ekg/vcflib.git
$ cd vcflib
$ make
```

Once this is complete, vcflib tools should be available under *vcflib/bin/*.

## Exercises

Slices. In this exercise we want to select a slices of the original VCF files, containing only few individuals and few loci. this can be done in different ways.

we want to extract information for one individual (named HG00117) at one locus (named rs147284345 on chromosome 2 at position 215796346 ). All the commands below are equivalent, and will create a  new vcf files named myslice:

```
$ vcftools --gzvcf test.vcf.gz --indv HG00117   --snp rs147284345  --recode --out myslice
```

here we ask vcftools to use the compressed file test.vcf.gz to extract only the line relative to the variant that is called rs147284345 and the column relative to individual  HG00117 and to recode a new vcf called myslice

```
$ vcftools --gzvcf test.vcf.gz --chr 2 --from-bp  215796346 --to-bp 215796346  --indv HG00117 --recode --out myslice
```
here we ask vcftools to use the compressed file test.vcf.gz to extract only the line relative to the variant that is  on chromosome 2 at position  215796346 and the column relative to individual  HG00117 and to recode a new vcf called myslice

We want to extract VCF information for a list of individuals and a specific set of loci. To do this we will ask vcftools to consider individuals in the file “myindividuals.list”  (a single column with individual’s ID file)  and a list of loci in the file “myloci.list” (a single column with a list of loci names file). We will store the result in a vcf called myslice

```
$ cat myloci.list
rs71399158
rs147284345
rs140828677

$cat myindividuals.list
HG00117
HG00118
HG00119
HG00120

$vcftools  --gzvcf test.vcf.gz --keep myindividuals.list  --snps myloci.list --recode --out myslice
```

2) In this exercise we are only interested in information contained in the “INFO” field. The command used here will extract it and redirect in a tab delimited file that can be easily  visualized and imported in other applications.

As an example the info field of the locus 215796346 on chromosome 2 that is a single string:  

“ERATE=0.0004;AA=C;AVGPOST=0.9994;AN=2184;THETA=0.0005;VT=SNP;RSQ=0.8232;SNPSOURCE=LOWCOV;LDAF=0.0012;AC=2;AF=0.0009;AFR_AF=0.0041”

will be transformed in the tab-delimited file “myinfo.out” with two lines (a header, and one with values):

|CHROM|POS|ID|REF|ALT|QUAL|FILTER|AA|AC|AF|AFR_AF|AMR_AF|AN|ASN_AF|AVGPOST|CIEND|CIPOS|END|ERATE|EUR_AF|HOMLEN|HOMSEQ|LDAF|RSQ|SNPSOURCE|SVLEN|SVTYPE|THETA|VT|
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
|2|215796346|rs147284345|C|A|100|PASS|C|2|0.0009|0.0041|NA|2184|NA|0.9994|NA|NA|NA|0.0004|NA|NA|NA|0.0012|0.8232|LOWCOV|NA|NA|0.0005|SNP|

```
$ vcf2tsv  -n NA  test.vcf.gz > myinfo.out
```
we are using the option -n to ask vcf2tsv to put an NA where data is not available.

3) extract a genotype
4) extract allele frequencies
