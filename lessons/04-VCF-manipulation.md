---
layout: lesson
root: .
title: Manipulating VCF files
minutes: --
---

## Learning Objectives

* Install tools for VCF file manipulation.
* Download VCF files from 1000 Genomes project.
* Work with VCF files: slicing and extracting genotypes, locus and frequencies

## Lesson
In this lesson you will learn how to manipulate VCF files. For this exercises we will use publicly available data from the 1000 Genomes  Project.

## File format

The VCF file format is explained in detail [here](http://samtools.github.io/hts-specs/VCFv4.1.pdf)

To reduce the size of the files, VFCs are usually compressed and indexed using the gzip and tabix command from HTSlib.

VCFtools and vcflib are two collections of software tools commonly used for handling VCF data files. This lesson gives instructions on installing these tools on a Linux system.

## VCFtools

VCFtools provides tools for site filtering, individual filtering and genotype filtering along with multiple options for output and comparison. More detailed instructions on using VCFtools can be found [here](http://vcftools.sourceforge.net/man_latest.html).

To install VCFtools, download the source files from [here](http://sourceforge.net/projects/vcftools/files/). Extract the content of the downloaded vcftools_x.y.z.tar.gz file (*note*: x.y.z is the version of the file downloaded). Navigate to the folder where files have been extracted, and type *make* to compile the files.

```
$ tar xzf vcftools_x.y.z.tar.gz
$ cd vcftools_x.y.z
$ make
$ cd ..
```
Once the compilation process is complete, the perl scripts and cpp executable will be installed in the folder: *vcftools_x.y.z/bin/*. For simplicity, add this folder to your system path, so these tools are available even if you navigate to a different folder.

```
$ export PATH=$PATH:/my/work/dir/vcftools_x.y.z/bin/
```

## vcflib

vcflib provides tools for manipulating VCF files such as comparison, format conversion, filtering, etc. More details on all the available options can be found [here](https://github.com/ekg/vcflib).

vcflib can be downloaded [here](https://github.com/ekg/vcflib). To download and compile vcflib, use the following commands:

```
$ git clone --recursive git://github.com/ekg/vcflib.git
$ cd vcflib
$ make
$ cd ..
```

Once this is complete, vcflib tools should be available under *vcflib/bin/*. Again, for simplicity, add this folder to your system path, so these tools are available even if you navigate to a different folder.

```
$ export PATH=$PATH:/my/work/dir/vcflib/bin/
```

## HTSlib

Another useful tool we will be using is *tabix*, which is part of [HTSlib](http://www.htslib.org/download/). You can download the source files for htslib from [here](https://github.com/samtools/htslib/releases/download/1.2.1/htslib-1.2.1.tar.bz2), or from directly from their [github](https://github.com/samtools/htslib) repository. To install HTSlib, use the following commands:

```
$ bunzip2 htslib-1.2.1.tar.bz2
$ tar xf htslib-1.2.1.tar
$ cd htslib-1.2.1/
$ ./configure
$ make
$ make DESTDIR=/my/install/folder/ prefix=/ install
$ cd ..
```
Once more, add the installed folder to your path:

```
$ export PATH=$PATH./my/install/folder/bin
```

## Exercises
### 1 - Downloading data

Sample VCF files can be downloaded from the [1000 Genomes Project](http://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/).

For the following examples we will use the *chromosome Y*  from the 1000 Genomes data repository.

```
http://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/ALL.chrY.phase3_integrated_v1a.20130502.genotypes.vcf.gz
```

We will download the data using the unix [wget](http://www.gnu.org/software/wget/manual/wget.html) command to download the file from the ftp server of the 1000 Genomes Project: *Note:* We have selected this chromosome because it is small and easy to download.On your terminal, type the following:

```
$ wget http://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20130502/ALL.chrY.phase3_integrated_v1a.20130502.genotypes.vcf.gz -O chrY.vcf.gz
```

This will download the chromosome Y VFC file and save it as *chrY.vcf.gz*.
After downloading we need to index the file to allow standard tools for VCF files to quickly jump through the file. To create the index we can use tabix as follows:

```
$ tabix -p vcf  chrY.vcf.gz
```

Notice that we must specify the format of the file (in this case vcf) with the *-p* parameter. After running this command, a new index file *chrY.vcf.gz.tbi* will be created.


### 2 - Slices
In these exercises we want to select slices of the original VCF files.

**(a)**
We can use tabix to select any region of the file, by giving the indices we are interested in. However, if these indices are not included in the file, no data will be returned. For example:

```
$ tabix chrY.vcf.gz Y:1-10
```

We can add the header to the output by using the *-h* flag. If we ask for the header of an empty slice, we will get only the header information:

```
$ tabix -h chrY.vcf.gz Y:1-10
```

For example, if we are interested in the region of chromosome Y from base 2,655,180 to base 2,657,349 we can select this region of the vcf file using the tabix command which takes only the region  we are interested in and keeps the heading (*-h*) of the original file. The resulting file is a plain text file, if you want to see how it looks like you can use the unix command less.

```
$ tabix -h  chrY.vcf.gz Y:2655180-2657349  > mysliceofY.vcf
$ less  mysliceofY.vcf
```

The plain text file can be read and used as it is, however many of the applications in vcflib and vcftools require it to be compressed (using bgzip) and indexed (using tabix). While telling tabix to index the file, we are specifying the file format (*-p*). Two new files will be produced with the same name as the original VCF and a gz (compression) and  tbi (indexing) extensions.  Type the ls -l command to see the files in your folder.

```
$ bgzip mysliceofY.vcf
$ tabix -p vcf  mysliceofY.vcf.gz
$ ls -l
-rw-r--r-- 1 user group  5791 Jun 23 09:37 mysliceofY.vcf.gz
-rw-r--r-- 1 user group   104 Jun 23 09:37 mysliceofY.vcf.gz.tbi
```

**(b)**
We want to extract information for one individual (named HG00117) at one locus (named rs2534636 on chromosome Y at position 2657176). All the commands below are equivalent, and will create new vcf files:

We ask vcftools to use the compressed file *chrY.vcf.gz* to extract only the line relative to the variant called rs2534636 and the column relative to individual HG00117 and to recode (i.e. rewrite, --recode) a new vcf called ex1b. vcftools will add the extension .recode. If you give a look to this uncompressed file you will see the genotypes of a single individual at one locus:


```
$ vcftools --gzvcf chrY.vcf.gz --indv HG00117 --snp  rs2534636 --recode --out ex2b1
$ less ex2b.recode.vcf
```

Another equivalent way to do it is to combine the tabix and the vcflib command *vcfkeepsamples* on the standard out of tabix (*-*) and redirect the output to the *ex2b2.vcf* file:

```
$ tabix -h chrY.vcf.gz Y:215796346-215796346 | vcfkeepsamples -  HG00117 > ex2b2.vcf
```

A third way to do it would be to ask vcftools to use the compressed file *chrY.vcf.gz* to extract only the line relative to the variant that is  on chromosome Y at position  2657176 and the column relative to individual  HG00117 and to recode a new vcf called ex2b3.

```
$ vcftools --gzvcf chrY.vcf.gz  --chr Y --from-bp  2657176 --to-bp 2657176  --indv HG00117    --recode --out ex2b3
```

**(c)**
We want to extract VCF information for a list of individuals and a specific set of loci. To do this we will ask vcftools to consider individuals in the file *myindividual.list*  (a single column with individual’s ID file)  and a list of loci in the file “myloci.list” (a single column with a list of loci names file). We will store the result in a vcf called ex2c.

To quickly make a list of loci we will use the unix command append  (>>):

```
$ echo rs11575897 > myloci.list
$ echo rs2534636 >> myloci.list
$ echo rs1800865 >> myloci.list
$ cat myloci.list
rs11575897
rs2534636
rs1800865
```

To quickly make a list of three individuals we will use the vcflib command *vcfsamplenames* that extract the ID of the individuals in the VCF file:

```
$ vcfsamplenames chrY.vcf.gz  | head -3 > myindividual.list
$ cat myindividual.list
HG00096
HG00101
HG00103
$ vcftools  --gzvcf chrY.vcf.gz --keep myindividual.list  --snps myloci.list --recode --out  ex2c
```

### 3 - Info
In this exercise we are only interested in information contained in the “INFO” field. As an example the info field of the locus 2657176 on chromosome Y is a single string with a bunch of ;-delimited information:  

```
“AA=T;AC=89;AF=0.0721817;AN=1233;DP=5211;NS=1233;AMR_AF=0.0029;AFR_AF=0.0078;EUR_AF=0.0250;SAS_AF=0.1365;EAS_AF=0.0000”
```

We can use the vcflib command  vcft2tsv  to transform this string in a tab-delimited string in a file *myinfoat2657176.out* with two lines (a header, and one with values). We will ask vcf2tsv to  put an NA where data is not available using the option -n. To make it easier we will combine the *vcf2tsv* command with tabix to limit our analysis to one locus:

```
$ tabix -h chrY.vcf.gz Y:2657176-2657176 | vcf2tsv -n NA > myinfoat2657176.out
```

The output will be in the following format:

|CHROM|POS|ID|REF|ALT|QUAL|FILTER|AA|AC|AF|AFR_AF|AMR_AF|AN|DP|EAS_AF|END|EUR_AF|NS|SAS_AF|SVTYPE|
|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|:---|
|Y|2657176|rs2534636|C|T|11169.1|PASS|T|89|0.0721817|0.0078|0.0029|1233|5211|0.0000|NA|0.0250|1233|0.1365|NA|

The command can be run on the whole vcf file:

```
$ vcf2tsv  -n NA  chrY.vcf.gz  > myinfo.out
```

### 4 - Extract a genotype

In this exercise we want to know the genotype of  individuals  HG00117 and HG00101 on chromosome Y in the region between base 2,655,180 and base  2,658,745. This example will show you both how to extract genotype information and how  to combine commands of the vcflib.

We will  first select the region (but it can also be a single locus) with tabix and then ask *vcfkeepsamples* to process the standard out (*-*)  to slice the vcf for individual HG00117. Finally we will ask *vcfgenotypes* to extract the genotype:

```
$ tabix -h chrY.vcf.gz  Y:2655180-2658745 | vcfkeepsamples  -  HG00117 HG00101 | vcfgenotypes   -
Y       2655180 G       A       G,A     HG00101:G       HG00117:G
Y       2655471 A       C       A,C     HG00101:A       HG00117:A
Y       2655754 A       T       A,T     HG00101:A       HG00117:A
Y       2655800 A       G       A,G     HG00101:A       HG00117:A
Y       2655989 A       G       A,G     HG00101:A       HG00117:A
Y       2655994 C       G       C,G     HG00101:C       HG00117:C
Y       2656126 C       T       C,T     HG00101:C       HG00117:C
Y       2656127 G       C       G,C     HG00101:G       HG00117:G
Y       2656276 G       A       G,A     HG00101:G       HG00117:G
Y       2656677 A       G       A,G     HG00101:A       HG00117:A
Y       2657176 C       T       C,T     HG00101:C       HG00117:C
Y       2657205 C       G       C,G     HG00101:C       HG00117:C
Y       2657214 G       C       G,C     HG00101:G       HG00117:G
Y       2657239 C       G       C,G     HG00101:C       HG00117:C
Y       2657247 G       A       G,A     HG00101:G       HG00117:G
Y       2657349 T       C       T,C     HG00101:T       HG00117:T

```
For all loci available in the VCF file in the selected region we will see the chromosome the position, information about reference and alternate alleles and the  genotype of the two selected individuals.

### 5 - Extract allele frequencies
In this exercise we want to  calculate allele frequencies  at all loci contained in the chromosome Y *chrY.vcf.gz* file. This command line will produce a file called *ex5.frq*. Type *less* to see the content:

```
$ vcftools --gzvcf chrY.vcf.gz  --freq --out ex5
$ less ex5.frq
```
If we want to restrict the calculation to a few selected individuals and a few loci, we can combine the command line above with few options:

```
$ vcftools --gzvcf chrY.vcf.gz  --freq --out ex5slice  --keep myindividuals.list  --snps myloci.list
```

The output should look like this:

```
$ cat ex5slice.frq
CHROM    POS    N_ALLELES    N_CHR    {ALLELE:FREQ}
Y    2655180    2    3    G:1    A:0
Y    2657176    2    3    C:1    T:0
Y    2658271    2    3    G:1    A:0
```
