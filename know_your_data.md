Getting to know your data
===================

Group: 
-----
Josh Herr, Michael Linderman, Jon Badalamenti

Learning Objectives:
-------------------
#### What's the motivation for this lesson?
* Identify common features of "data" and data formats and what those features imply
* genomics - what do the files look like: fasta, fastq, fastg, sra, sff, vcf, sam, bam, bed, etc...
* genomics platforms and data type? which machine gives you which data...
* How to realize which direction to proceed when you know something about the format of your data.

#### What mindset change should the learner have? (ie, awareness of certain techniques)
* recognize file formats and implications thereof
* zipped or unzipped? file compression
* using some tools that take data in compressed state, i.e. zcat, zhead?
* file extension?
* file size?
* how many units? (nucleotides - read number?)
* how to look at data structure using shell -- does it agree with the file extension?
* binary, flat text file, data frame? - realize the type of tools to use that type of data
* specific tools to use that type of data file
* type of downstream file formats that you might need to convert to.

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


The following table shows some of the common types of data files and includes some information about them:

| Data type |	Kind Of Data |	Format |	Type | Type | Type |
| :------------- | :------------- | :---------------- | :----------------| :----------------| :---------------|
| 	|  | |	 | |  |
| 	| | | | | |
| 	| 	| |	 |	 |	
|  |  |	 |	 |		|  |
|  |  |  |	 |  |	 |
|  | 	|  |	 | |	 |
| |  |  |  |  |  |
