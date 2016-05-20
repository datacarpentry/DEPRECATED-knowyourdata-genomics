Group: Josh Herr, Michael Linderman, Jon Badalamenti, Jeramiah Ory, Shari Ellis 

Learning Objectives:
What's the motivation for this lesson?
Identify common features of "data" and data formats and what those features imply
genomics - what do the files look like: fasta, fastq, fastg, sra, sff, vcf, sam, bam, bed, etc...
genomics platforms and data type? which machine gives you which data...
How to realize which direction to proceed when you know something about the format of your data.

What mindset change should the learner have? (ie, awareness of certain techniques)
recognize file formats and implications thereof
zipped or unzipped? file compression
using some tools that take data in compressed state, i.e. zcat, zhead?
file extension?
file size?
how many units? (nucleotides - read number?)
how to look at data structure using shell -- does it agree with the file extension?
binary, flat text file, data frame? - realize the type of tools to use that type of data
specific tools to use that type of data file
type of downstream file formats that you might need to convert to.

What skills should the learner leave the room with?
Identify key parts of filenames, and common file types
Describe key attributes of different file formats (record, field, compression, binary vs. text, ordering) and how that guides your search/use of (groups of) tools
Identify description of data tables, including non-traditional formats like a directory listing for specifically named files
Download file (different protocols), verify (md5 checksum) and "gut check" with head

What should be discussed during your module?
vocabulary
record, field, delimiter characters, comments
header lines
metadata (README.md files, etc.)
compression (zip, tar (tape archive))
types of genome specific data files (fastq, fasta, fastg, sff, sra, etc.)
downstream data formats (vcf, biom, bam, sam, etc.)
types of flat data files (csv, tsv, txt)
end of line characters (and platform differences)
technical skills
looking at data files and realizing what type of file it is
looking at data - what is appropriate for a GUI (text editor) word processor (never!) and what can be done from the command line (everything!)
converting one type of data file to another
understanding if data is corrupt / data integrity (md5 checksum, etc)
concepts
Data tables come in many forms
Repeating elements (records/fields) is what enables programmatic approaches
What is "too big" for viewing/editing? Some heuristics...
assessments
"Handle" data return e-mail from core with ftp URL including download, verify checksum, quickly browse
Identify key attributes of example file snippet
Recognize "non-traditional" data table, such as file listing, and process it as


### Shari's notes
 
You received email with the following link to get your data APi//yourdata.is.here Before even getting it, what do you know about the data?
 
Attitudes/dispositions
 
With huge data sets, there is little to be gained and potential costs by trying to open it.
 
My intuition about the file is going to drive how I work with it.
 
It is important to double-check the processes to know that the file is not corrupted.
 
As a good citizen, they should do the same thing when uploading their own data.
 
Declarative knowledge
 
There are ways to know attributes about your file without opening it.  Tell me up to 5 things about it.
 
Familiar with vocabulary so can work with distinguish among genome-specific data files, downstream formats, and flat data files.
 
These are the genome specific date file types.
 
Understand the tools needed to work with specific file types.
 
Understand when you need to google for a tool vs know you already have it. 
 
Appreciation of sheer size of the dataset.
 
Unix is designed to look at text. There are established tools to deal with text-based data. Because people wanted to take advantage of these tools.
 
Skills
 
You can perform unix commands on a compressed file without uncompressing it. 
 
Download and perform MD5.
 
Handle a directory of files.
 
File command.
 
Challenge
 
How do I count how many records I have?
 
Use file command to find text vs binary files.
