---
layout: lesson
root: .
title: Post-assembly - de novo RNA Transcriptome Analysis - handling Blast annotation output
minutes: 5
---

## Learning Objectives 

    In this lesson we will learn how to handle blast output file in order to arrive to the real homologs.

    pre-request learning: How to blast online (ie NCBI) or by unix lesson.

## Lesson 

One of the interesting stages in de-novo RNA sequencing comes when you finally annotate your sequences.
You can annotate your new contigs which theoretically represent your special organism transcriptome (all the RNA that is expressed in the cell) in different ways.
In order to find homologs it is always recommended to work on the protein level, therefor we will first search for CDS in this transcript and then translate them into proteins. 
One way to do so is to use the transdecode program which is included as a part of the Trinity package: http://trinityrnaseq.github.io/
The logic behind this step is to filter all the contigs that have "junk" tails, for example one contig can be constructed from 40% CDS and 60% "junk" DNA. In that way we could latter reach  
better results at the blast stage (It is also recommended to re-aligned the reads against these CDSs and not the original contigs in order to get real expression based on the CDS and not 
on the tails).

The trinity Transdecode package gives as an output both CDSs sequences file and proteins sequences file. For our propose we will use the proteins file.
We will run it at the Blastp program (as demonstrated in the blast lesson) defining the output format parameter to 6 (-outfmt 6). 
To read more on the different blast output formats follow these links:
http://www.ncbi.nlm.nih.gov/books/NBK279690/
http://www.ncbi.nlm.nih.gov/books/NBK279675/

The are 12 columns at the blastp output, however we will not use all of them for the filtering steps. Their titles are as follows:

1. Query Seq-id: normally the accession number of your contig or predicted protein.
2. Subject Seq-id: the accession number of the sequence that got as hit from the protein database (can be swissprot, uniprot, etc')	 
3. percent identity: global alignment %ID between both sequences
4. alignment length
5. number of mismatches
6. number of gap openings
7. query start
8. query end
9. subject start
10. subject end
11. Expect value (e-value)
12. HSP bit score

An exmple for the first blast output lines is (each column is separated by a tab):

cds.comp100010_c1_seq1|m.67288	sp|Q9TW32|PPIB_DICDI	49.35	77	36	2	49	125	26	99	6.00E-12	67
cds.comp100052_c0_seq1|m.67310	sp|Q5TYW6|RSPH9_DANRE	33.46	269	164	5	25	283	14	277	4.00E-37	138
cds.comp100055_c0_seq1|m.67313	sp|P35248|SFTPD_RAT	45.24	84	43	1	137	217	56	139	1.00E-07	56.2
cds.comp100073_c0_seq1|m.67327	sp|Q9M1K2|PI5K4_ARATH	37.24	196	122	1	9	204	70	264	4.00E-31	125
cds.comp100100_c0_seq1|m.67345	sp|Q2QL79|CAV1_DIDVI	38.4	125	76	1	7	130	48	172	2.00E-25	100
cds.comp100117_c0_seq2|m.67368	sp|Q5XEP2|HSOP2_ARATH	40.78	103	61	0	359	461	1	103	3.00E-17	88.2

The next stage is to filter out the blast output file. If you are working on sequencing data it is recommended to work just on the first result for each query sequence. If you are working 
just on few sequences you have the privilage to look at all the results and decide which is better.

The common mistake within scientists is that they filter the results just by e-value and percent of ID. For examples all the alignments that have %ID>70 and e-value<0.00005 will be considered
as potential homolgs. From first looking it sounds great, but the major question that should have be asked is what about the query coverage???
There is an option to get a good p-value with a high %ID when just 10% of your protein appears in the alignment! meaning that possibly both proteins have a common motif
but are definitely not homologs!!!

In order to reach the real homologs follow these steps (if the file is not too big you can perform it in the excel program):

1. Add column 13 represnting the length of the query sequence (there are programs that can calcuate sequence length from a fasta file- make sure that you are working on the protein sequences and not the CDS one).
2. Add column 14 represnting the length of the subject sequence (this data can be downloaded from the database that you used: swissprot, uniprot, etc'...)
3. Add column 15 in which you will calculate the query coverage using this formula: (|query start- query end| / query length * 100) (in excel you can use this formula:  ABS(A7-A8)/A13 * 100).
4. Add column 16 in which you will calculate the subject coverage using this formula: (|subject start- subject end| / subject length * 100) (in excel you can use this formula:  ABS(A9-A10)/A14 * 100).

Now you can finally filter the results. Suggested filtering values are as follows (for far homologs) but you can always interoperate your experimentally biologically meaning defining other 
values in order to get better results:
e-value < 0.00005
%ID > 40
%query coverage > 70%
%subject coverage > 70% (note that this field is less essential, you can choose a smaller value as 50% which mean that at least 50% of the protein was covered by our contig, 
his is still biologically reasonable).


As mentioned in the blast lesson, in order to defined homologs you need to perform a reciprocal blast ,meaning first to blast your query sequence against a DB of sequences (i.e swissprot, uniprot50),
after filtering the blast output file you should take the subject sequence which represents a potential homolog and blast it back against you database (i.e contigs). 
If you get the same query sequence as the one you have started with, it means you probably found the real homolgs.



## Exercises

You have received a blast output file from a de novo transcriptom that was built using the trinity package (including using the step of transdecode packge that generate CDS and proteins).
The transcriptom includes ~60,000 tanscripts. The blast result was first filtered to return one best result for each query sequence and all the results that have a p-value< 0.00005.

Perform the following steps:

1. Download the file from the following link:
http://figshare.com/articles/Blast_output_format_lesson/1460728

2. open it with the excel program.

3. Add column 13 and 14 representing the query coverage and the subject coverage respectivly, using the formula that was previously mentioned.

4. filter the file using the following paramters values (You can use the filter option in excel through the data command):
%ID > 40
%query coverage > 70%

? How many transcripts have now a potential homolog?
! There are about ~24,000 transcripts that now have potential homologs.

? Add the subject coverage filtering value > 70% for your filtering request. How many transcript do you get now?
! ~10,000 transcripts. This demonstrate the importance of defining by yourself the filtering parameters values. In that case we can set a less stringent value like 50%, this will yield 
~ 14,000 transcripts.
You can get the final filtered file here:
http://figshare.com/articles/blast_output_format_6_lesson/1460747

It is important to understand that we have started with about 60,000 transcripts but found homologs to just ~14,000 of them, meaning that now we could name them with a gene name. 
However, it doesn't mean that rest of the ~46,000 transcripts have no importance, Some of them can be "junk" transcript but the others can be uniquely  expressed in our organism.








 
