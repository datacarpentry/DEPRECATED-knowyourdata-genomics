---
layout: lesson
root: .
title: Fasta Format
minutes: 5
---

## Learning Objectives 

    In this lesson we will learn how to recognize fasta format files and to how to create your own fasta format sequences.


## Lesson 

Fasta format is a common used text sequence representing format which is required for common used bioinformatic's programs. It can be used for both Nucleotide or Amino Acid sequences.
Fasta format is constructed from two parts for each sequence: header and sequence.

The header line always start with a ">" symbol following by a small description of the sequence.
The description can include for example: gene name, accession number, organism, etc'... 
The header is extremely important when we work on more than one sequence at once, as uploading it to another program will generate an output file where each sequence needs to be recognized.

The sequence part start at the second line and can be constructed from more than one line. However, each line is limited to max of 80 characters.

Example of fasta sequence:

>gi|72198189|ref|NP_000624.2| apoptosis regulator Bcl-2 alpha isoform [Homo sapiens]
MAHAGRTGYDNREIVMKYIHYKLSQRGYEWDAGDVGAAPPGAAPAPGIFSSQPGHTPHPAASRDPVARTS
PLQTPAAPGAAAGPALSPVPPVVHLTLRQAGDDFSRRYRRDFAEMSSQLHLTPFTARGRFATVVEELFRD
GVNWGRIVAFFEFGGVMCVESVNREMSPLVDNIALWMTEYLNRHLHTWIQDNGGWDAFVELYGPSMRPLF
DFSWLSLKTLLSLALVGACITLGAYLGHK

At next generation sequencing we can generate a fasta sequences file which can includes all the reads or contigs from one sample in example. 
When we upload it to another program it will start reading the first line which includes the ">" symbol in order to extract it from the header line, then it will jump to the next lines
in order to extract all the sequence. When the program reach the next ">" symbol it will recognize that a new sequence has started and repeat the same procedure.

Example of a fasta sequences file:

>gi|72198189|ref|NP_000624.2| apoptosis regulator Bcl-2 alpha isoform [Homo sapiens]
MAHAGRTGYDNREIVMKYIHYKLSQRGYEWDAGDVGAAPPGAAPAPGIFSSQPGHTPHPAASRDPVARTS
PLQTPAAPGAAAGPALSPVPPVVHLTLRQAGDDFSRRYRRDFAEMSSQLHLTPFTARGRFATVVEELFRD
GVNWGRIVAFFEFGGVMCVESVNREMSPLVDNIALWMTEYLNRHLHTWIQDNGGWDAFVELYGPSMRPLF
DFSWLSLKTLLSLALVGACITLGAYLGHK

>gi|119583543|gb|EAW63139.1| B-cell CLL/lymphoma 2, isoform CRA_b [Homo sapiens]
MAHAGRTGYDNREIVMKYIHYKLSQRGYEWDAGDVGAAPPGAAPAPGIFSSQPGHTPHPAASRDPVARTS
PLQTPAAPGAAAGPALSPVPPVVHLTLRQAGDDFSRRYRRDFAEMSSQLHLTPFTARGRFATVVEELFRD
GVNWGRIVAFFEFGGVMCVESVNREMSPLVDNIALWMTEYLNRHLHTWIQDNGGWVGALGDVSLG


Common file extension:
Normally, must programs don't require a specific file extension for the fasta file, but those that do usually use the common ones: *.fa , *.fasta *.fsa

? How can I download a fasta sequence for a specific gene, lets say the IAP3 protein sequence at human?
! One way to do it is to use the NCBI entrez engine using these following steps:
1. Enter the NCBI site: http://www.ncbi.nlm.nih.gov/
2. Choose the Protein database at the scroll down list.
3. Enter at the text box: "IAP3 AND homo sapiens" and press on search (please notice that if you have the accession number you can just write it and press search).
4. At the next page you will get one record of the IAP3 in GenPept format, in order to past it to a fasta format press on the FASTA link that appears under the header.
5. Copy the sequence to text file. You should get the following sequence:

>gi|12643387|sp|P98170.2|XIAP_HUMAN RecName: Full=E3 ubiquitin-protein ligase XIAP; AltName: Full=Baculoviral IAP repeat-containing protein 4; AltName: Full=IAP-like protein; Short=ILP; Short=hILP; AltName: Full=Inhibitor of apoptosis protein 3; Short=IAP-3; Short=hIAP-3; Short=hIAP3; AltName: Full=X-linked inhibitor of apoptosis protein; Short=X-linked IAP
MTFNSFEGSKTCVPADINKEEEFVEEFNRLKTFANFPSGSPVSASTLARAGFLYTGEGDTVRCFSCHAAV
DRWQYGDSAVGRHRKVSPNCRFINGFYLENSATQSTNSGIQNGQYKVENYLGSRDHFALDRPSETHADYL
LRTGQVVDISDTIYPRNPAMYSEEARLKSFQNWPDYAHLTPRELASAGLYYTGIGDQVQCFCCGGKLKNW
EPCDRAWSEHRRHFPNCFFVLGRNLNIRSESDAVSSDRNFPNSTNLPRNPSMADYEARIFTFGTWIYSVN
KEQLARAGFYALGEGDKVKCFHCGGGLTDWKPSEDPWEQHAKWYPGCKYLLEQKGQEYINNIHLTHSLEE
CLVRTTEKTPSLTRRIDDTIFQNPMVQEAIRMGFSFKDIKKIMEEKIQISGSNYKSLEVLVADLVNAQKD
SMQDESSQTSLQKEISTEEQLRRLQEEKLCKICMDRNIAIVFVPCGHLVTCKQCAEAVDKCPMCYTVITF
KQKIFMS




## Exercises

1. Extract the protein fasta sequence of the mouse clock gene using its accession number: AAC53200.1.

Result:
1. First choose the protein database, then enter the accession number AAC53200.1 at the text box and press on search.
At the next page transfer the GenPept format to fasta one by pressing on the FASTA link. Copy and paste.
You should get this sequence:

>gi|2114488|gb|AAC53200.1| CLOCK [Mus musculus]
MVFTVSCSKMSSIVDRDDSSIFDGLVEEDDKDKAKRVSRNKSEKKRRDQFNVLIKELGSMLPGNARKMDK
STVLQKSIDFLRKHKETTAQSDASEIRQDWKPTFLSNEEFTQLMLEALDGFFLAIMTDGSIIYVSESVTS
LLEHLPSDLVDQSIFNFIPEGEHSEVYKILSTHLLESDSLTPEYLKSKNQLEFCCHMLRGTIDPKEPSTY
EYVRFIGNFKSLTSVSTSTHNGFEGTIQRTHRPSYEDRVCFVATVRLATPQFIKEMCTVEEPNEEFTSRH
SLEWKFLFLDHRAPPIIGYLPFEVLGTSGYDYYHVDDLENLAKCHEHLMQYGKGKSCYYRFLTKGQQWIW
LQTHYYITYHQWNSRPEFIVCTHTVVSYAEVRAERRRELGIEESLPETAADKSQDSGSDNRINTVSLKEA
LERFDHSPTPSASSRSSRKSSHTAVSDPSSTPTKIPTDTSTPPRQHLPAHEKMTQRRSSFSSQSINSQSV
GPSLTQPAMSQAANLPIPQGMSQFQFSAQLGAMQHLKDQLEQRTRMIEANIHRQQEELRKIQEQLQMVHG
QGLQMFLQQSNPGLNFGSVQLSSGNSNIQQLTPVNMQGQVVPANQVQSGHISTGQHMIQQQTLQSTSTQQ
SQQSVMSGHSQQTSLPSQTPSTLTAPLYNTMVISQPAAGSMVQIPSSMPQNSTQSATVTTFTQDRQIRFS
QGQQLVTKLVTAPVACGAVMVPSTMLMGQVVTAYPTFATQQQQAQTLSVTQQQQQQQQQPPQQQQQQQQS
SQEQQLPSVQQPAQAQLGQPPQQFLQTSRLLHGNPSTQLILSAAFPLQQSTFPPSHHQQHQPQQQQQLPR
HRTDSLTDPSKVQPQ


 
