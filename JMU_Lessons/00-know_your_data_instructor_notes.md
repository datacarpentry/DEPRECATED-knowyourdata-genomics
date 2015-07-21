Getting to know your data
===================

Learning Objectives:
-------------------
#### What's the goal for this lesson?
* You should be able to identify common features of "data" and data formats and what those features imply
* You should be able to look at a file and be able to identify the following types of data: fasta, fastq, fastg, sra, sff, vcf, sam, bam, bed, etc...
* You should be able to identify what type of sequencing platform provides which type of data.
* You should be able to idenitfy where your data came from and what should be the direction you would take for data analysis 

#### At the end of this lesson you should be able to:
* Recognize file formats and implications thereof
* Whether your data files are zipped or unzipped. You should have an understanding of file compression.
* Use tools that take data in compressed state (i.e. zcat, zhead)
* Identify the file extension and if it matches with actual file type.
* How to determine the file size
* How many units are in the file (i.e. nucleotides, lines of data, sequence reads, etc.)
* How to look at data structure using the shell -- does it agree with the file extension?
* Identify a binary, flat text file, and data frame? 
* You will be able to realize the type of tools to use for each specific type of data
* Identify the type of downstream file formats that you might need to convert your initial data to 


**The following table shows some of the common types of data files and includes some information about them:**

| File Extension |	Type of Data |	Format |	Example(s) | More Info | Type |
| :------------- | :------------- | :---------------- | :----------------| :----------------| :---------------|
| txt | multi-format | Text | study metadata, tab-delimited data | <a href="https://en.wikipedia.org/wiki/Text_file"> txt</a> | |
| fastq	| nucleotide  | Text |	sequencing reads |<a href="https://en.wikipedia.org/wiki/FASTQ_format>" fastq </a> |  |
| fasta	| nucleotide, protein | Text | the human genome | <a href="https://en.wikipedia.org/wiki/FASTA"> fasta</a>| |
| fastg | nucleotide | Text | <a href="http://www.homolog.us/blogs/blog/2012/12/27/fastg-a-new-format-for-representing-sequence/"> fastg</a> | | |
| sff	| 	|  |	Roche/454 sequencing data |	<a href="http://www.ncbi.nlm.nih.gov/Traces/trace.cgi?cmd=show&f=formats&m=doc&s=format#sff"> sff</a> |	|
| vcf | multi-format | Text	 |	 |	<a href="https://en.wikipedia.org/wiki/Variant_Call_Format"> vcf </a>	|  |
| sam | alignment | Text  |	reads aligned to a reference  | <a href="https://samtools.github.io/hts-specs/SAMv1.pdf"> sam </a> |	 |
| bam | alignment	| Binary  |	reads aligned to a reference | <a href="https://samtools.github.io/hts-specs/SAMv1.pdf"> bam </a> |	 |
| bed | metadata / feature definitions  | Binary  | genome coverage | <a href="http://www.ensembl.org/info/website/upload/bed.html"> bed </a> |  |
| biom | multi-format | Text | | <a href="http://biom-format.org/"> biom </a>| |
| h5 | binary hierarchical | Binary | PacBio sequencing data | <a href="https://en.wikipedia.org/wiki/Hierarchical_Data_Format"> h5 </a>| |
| pileup | alignment | Text | mpileup, SNP and indel calling| <a href="https://en.wikipedia.org/wiki/Pileup_format"> pileup</a>| |


#### What skills should the learner leave the room with?
* Identify key parts of filenames, and common file types
* Describe key attributes of different file formats (record, field, compression, binary vs. text, ordering) and how that guides your search/use of (groups of) tools
* Identify description of data tables, including non-traditional formats like a directory listing for specifically named files
* Download file (different protocols), verify (md5 checksum) and "gut check" with head

#### What should be discussed during your module?

#####vocabulary
* record, field, delimiter characters, comments
* header lines
* metadata (README.md files, etc.)
* compression (zip, tar (tape archive))
* types of genome specific data files (fastq, fasta, fastg, sff, sra, etc.)
* downstream data formats (vcf, biom, bam, sam, etc.)
* types of flat data files (csv, tsv, txt)
* end of line characters (and platform differences)

##### technical skills
* looking at data files and realizing what type of file it is
* looking at data - what is appropriate for a GUI (text editor) word processor (never!) and what can be done from the command line (everything!)
* converting one type of data file to another
* understanding if data is corrupt / data integrity (md5 checksum, etc)

##### concepts
* Data tables come in many forms
* Repeating elements (records/fields) is what enables programmatic approaches
* What is "too big" for viewing/editing? Some heuristics...

##### assessments
* "Handle" data return e-mail from core with ftp URL including download, verify checksum, quickly browse
* Identify key attributes of example file snippet
* Recognize "non-traditional" data table, such as file listing, and process it as

