Getting to know your data
===================

Learning Objectives:
-------------------
#### What's the goal for this lesson?
* You should be able to identify common features of "data" and data formats and what those features imply
* You should be able to look at a file and be able to identify the following types of data: fasta, fastq, fastg, sra, sff, vcf, sam, bam, bed, etc...
* You should be able to identify where your data came from (provenance)

#### At the end of this lesson you should be able to:
* Recognize file formats
* Whether your data files are zipped or unzipped. You should have an understanding of file compression.
* How to determine the file size
* How many units are in the file (i.e. nucleotides, lines of data, sequence reads, etc.)
* How to look at data structure using the shell -- does it agree with the file extension?
* Identify a binary, flat text file? 
 


**The following table shows some of the common types of data files and includes some information about them:**

| File Extension |	Type of Data |	Format |	Example(s) | 
| :------------- | :------------- | :---------------- | :----------------| :----------------| :---------------|
| txt | multi-format | Text | study metadata, tab-delimited data | <a href="https://en.wikipedia.org/wiki/Text_file" txt</a> | |
| fastq	| nucleotide  | Text |	sequencing reads |<a href="https://en.wikipedia.org/wiki/FASTQ_format" fastq </a> |  |
| fasta	| nucleotide, protein | Text | the human genome | <a href="https://en.wikipedia.org/wiki/FASTA" fasta</a>| |
| sff	| nucleotide	| Binary |	Roche/454 sequencing data |	<a href="http://www.ncbi.nlm.nih.gov/Traces/trace.cgi?cmd=show&f=formats&m=doc&s=format#sff" sff</a> |	|
| vcf | multi-format | Text	 |	variation/SNP calls |	|  |
| sam | alignment | Text  |	reads aligned to a reference  | <a href="https://samtools.github.io/hts-specs/SAMv1.pdf" sam </a> |	 |
| bam | alignment	| Binary  |	reads aligned to a reference | <a href="https://samtools.github.io/hts-specs/SAMv1.pdf" bam </a> |	 |
| bed | metadata / feature definitions  | Binary  | genome coverage | <a href="http://www.ensembl.org/info/website/upload/bed.html" bed </a> |  |
| h5 | binary hierarchical | Binary | PacBio sequencing data | <a href="https://en.wikipedia.org/wiki/Hierarchical_Data_Format" h5 </a>| |
| pileup | alignment | Text | mpileup, SNP and indel calling| <a href="https://en.wikipedia.org/wiki/Pileup_format" pileup</a>| |

##Looking at the data for this workshop

In this workshop, there are a few bioinformatics-related data types we will focus on (beyond simple text files - although in principle many of the files are text). First let's consider the definition/documentation for these file types:

**Plain-text**

* fastq   - [definition](https://en.wikipedia.org/wiki/FASTQ_format)
* sam file - [definition](https://samtools.github.io/hts-specs/SAMv1.pdf)
* vcf file - [definition](https://samtools.github.io/hts-specs/VCFv4.1.pdf)


**Compressed/binary**

* zip file - [definition](https://en.wikipedia.org/wiki/Zip_%28file_format%29)
* bam file (binary sam file) - [definition](https://www.broadinstitute.org/igv/BAM)

#### md5sum
In addition to understanding how to work with these files, we also need to understand how to verify the integrity of these files. It is not uncommon to download a file, and get error messages, have to restart downloads, move files, etc. In these cases, knowing how to verify that two files are the same (not simply named the same) is very important. To do this we use a process called checksums:

According to [wikipedia](https://en.wikipedia.org/wiki/Checksum) a checksum is 'a small-size datum from a block of digital data for the purpose of detecting errors which may have been introduced during its transmission or storage.'In other words it is a result we can generate that uniquely corresponds to a file. Any change to that file (adding a space, deleting a character, etc.) will change the file's checksum. 

##Exercises 

### A. File integrity - download a reference genome and verify the download 

1. Use ``wget`` to download two 'test' genomes from the following url:

   ```bash
$ wget http://de.iplantcollaborative.org/dl/d/6E4E9943-93F8-4136-86E3-14DA6D1B604F/GCF_000017985.1_ASM1798v1_genomic_2.fna
```
and
   
   ```bash
$ wget http://de.iplantcollaborative.org/dl/d/6E4E9943-93F8-4136-86E3-14DA6D1B604F/GCF_000017985.1_ASM1798v1_genomic_2.fna
```
2. Next for each of the use md5sum and compare the results

   ```bash 
$ md5sum <file>
```

### B. Download a reference genome from Ensembl

1. Visit the Ensembl database at [http://bacteria.ensembl.org/index.html](http://bacteria.ensembl.org/index.html). In the 'Search for a genome' search box search for 'Escherichia coli B str. REL606'; this should bring you to the genome of the strain used in the Lenski experiment ([ensemble direct link](http://bacteria.ensembl.org/escherichia_coli_b_str_rel606/Info/Index))
2. There will be a link '[Download DNA Sequence](ftp://ftp.ensemblgenomes.org/pub/bacteria/release-27/fasta/bacteria_5_collection/escherichia_coli_b_str_rel606/dna/)(FASTA)'. Click on the link an copy the URL from the web browsers navigation/location display (i.e. http://bacteria.ensembl.org/escherichia_coli_b_str_rel606/Info/Index). 
3. Use the ``wget`` command to download the contents of the ftp site (don't forget to use the '*' wildcard to download all files)

   ```bash
$ wget ftp://ftp.ensemblgenomes.org/pub/bacteria/release-27/fasta/bacteria_5_collection/escherichia_coli_b_str_rel606/dna/*
```
You should have downloaded the following files:

   ```
CHECKSUMS
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna.chromosome.Chromosome.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna.genome.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna_rm.chromosome.Chromosome.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna_rm.genome.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna_rm.toplevel.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna_sm.chromosome.Chromosome.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna_sm.genome.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna_sm.toplevel.fa.gz
Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna.toplevel.fa.gz
README
```
4. Use the ``less`` command to examine the README file - in particular, look at the <sequence type> definition to understand what the differently zipped files are. 
5. Generate a checksum using the ``sum`` command(``sum`` is used by Enseml and is  an alternative to ``md5sum``) for the **'Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna.genome.fa.gz'** file and compare with the last few digits of the sum displayed in the CHECKSUMS file. 
6. Preview the first few lines (``head``) of the compressed (gzip'd) reference genome using the ``zcat`` command:

   ```bash
$ zcat Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna.genome.fa.gz |head
```
7. Finally, unzip the E.coli reference genome, which will be part of the variant calling lesson and place it in your 'data folder' in a new 'ref_genome' folder. 

   ```bash
$ gzip -d Escherichia_coli_b_str_rel606.GCA_000017985.1.27.dna.genome.fa.gz
```
**Tip:** create the 'ref_genome' folder in '~/dc_workshop/data' and use the *cp* command to move the data




