#Getting to know your data

##Looking at data files

Each step of processing and analysis of a genomics pipeline spawns many new files, of many types. Some filetypes, like GFF are only found in a single step of the pipeline, and so are relativly easy to keep track of.
However, most are more like FASTQ files, where any given file could be from many different steps of the pipeline. These are the ones that cause the most trouble, and need the most careful management.

![FileTypes](Files/ngs_map_read_file_formats.png)

First, lets see what data files we have available:
```bash
ls
```
`ls` stands for list, and if you call it all by itself, it just returns a list of whatever is inside the folder you're currently looking at. You should give you a fairly big list of files in alphabetical order. However, they're hard to understand like this, so lets ask `ls` to make the list a little easier to read:

```bash
ls -lah
```
Here we've added modifiers to ls. Computer people usually call these modifiers 'flags' or 'arguments', and here we've added 3 flags:
`-l` directs `ls` to give us the results in 'long format' so we get more information
`-a` tells `ls` to show us 'all' of the things in the folder, even if they're usually hidden
`-h` makes the output 'human readable', so you see file sizes in kb or gb instead of bytes

###Text files
####FASTA
You're likely already familiar with FASTA files, as this is the most common way to distribute sequence information. Let's look at one:

```bash
head Raphanus.fa
```

`head` is another program, and it shows you just the top few lines of a file. By default, it shows ten, (so five sequences) but we can also change that behavior with flags:

```bash
head -4 Raphanus.fa
```
Now, you should see the first four lines of the Raphanus.fa file. 

>Exercise
>Try looking at EV813540.fa

FASTA files always have at least one comment line, which almost always begins with ">", but can start with ";". A given sequence in the file is allowed to have multiple comment lines, but they ususally don't. Extra comment lines for sequences can break some downstream processes. 

After the comment line is the sequence. Usually this is all on one line, but you can see that this one is formatted so that each sequence line is only 80 characters wide. This makes it easy to read, but makes it slightly more difficult to search within the file. For searching, its nice to have files where all of each sequence is on a single line. For instance, lets see whether there are any EcoRI sites are in the Raphanus.fa file:

```bash
grep "GAATTC" Raphanus.fa
```
grep is a program that searches for any string, and by default returns the entire line that your string is found in. For a file this big, this isn't very helpful. So lets modify how grep reports it's findings:

```bash
grep -B 1 "GAATTC" Raphanus.fa
```
`-B number` grep will return the line with your string plus 'number' lines of 'before context', so here we'll get one previous line...the comment that tells us the sequence name

Now we know which of the sequences have the restriction site we're looking for, but there's so many they've overfilled the screen. So lets redirect the output from the screen into a file:

```bash
grep -B 1 "GAATTC" Raphanus.fa > Raphanus_EcoRI.fa

```
The greater than sign takes everything that happens on this side of it `>` and dumps it into the place designated here. So, all of the output from that `grep` command above got saved into a new file called Raphanus_EcoRI.fa 
Since we didn't specify a place to save it, the new file is just saved in the same folder we're in, and we can see it by using `ls` again:

```bash
ls -lahr
```
`-r` makes the list print to our screen in reverse chronological order, so the newest files are on the bottom. This makes it easier to find what we're looking for.

`grep`, `ls` and `head` all have lots of useful flags, but we'll only do one more for now:

```bash
grep -c "GAATTC" Raphanus.fa
```

`-c` grep 'counted' 88 instances of EcoRI

####SSF, FASTQ and FNA & QUAL files
SSF stands for Standard Flowgram Format and is for 454 data
FASTQ is named after FASTA and is the output from most Illumina sequencers
FNA for FASTA nuclic acid, and QUAL for quality. If you have Solexa data you might have these
These are all files that you might get from your sequencing facility, and they all tell you about the machine, the sequence, and the quality of the sequence. 

These are more complex than FASTA files, because they include quality information, but that often makes them more useful. 

Most likely, you'll only be using FASTQ, as most people are doing Illumina sequencing right now.

```bash
head -4 33_20081121_2_RH2.fastq
```

FASTQ files have four lines of data per sequence. 
Line one should look something like `@30LWAAAXX_KD1_4:2:1:1428:1748` or `@EAS139:136:FC706VJ:2:2104:15343:197393 1:Y:18:ATCACG` depending on the vintage of your particular sequencer.
In either case, the jumble of letters between the `@` and the first `:` are a unique instrument name. After that each of the numbers between the colons represents things like run ID, flowcell lane, physical coordinates of the cluster that sequence came from, and whether the sequencing was single or paired end. (See the <a href="https://en.wikipedia.org/wiki/FASTQ_format"> Wikipedia</a> to decipher your own.)
Line two is the sequencers calls based on light/ph/etc
Line three is often just a '+', but can be followed by some description
Line four are the quality scores for each base call, encoded as ASCII symbols

Probably the most confusing thing about FASTQ are the wide variety of quality scores that different sequencing companies have adopted. If you keep good records, including what type of machine each of your sequences was run on, and at what time, this isn't such a problem. However, if you've just inherited a pile of poorly managed sequences, you'll need your detective hat:

```
  SSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSS.....................................................
  ..........................XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX......................
  ...............................IIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII......................
  .................................JJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJ......................
  LLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLLL....................................................
  !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
  |                         |    |        |                              |                     |
 33                        59   64       73                            104                   126
  0........................26...31.......40                                
                           -5....0........9.............................40 
                                 0........9.............................40 
                                    3.....9.............................40 
  0.2......................26...31........41                              

 S - Sanger        Phred+33,  raw reads typically (0, 40)
 X - Solexa        Solexa+64, raw reads typically (-5, 40)
 I - Illumina 1.3+ Phred+64,  raw reads typically (0, 40)
 J - Illumina 1.5+ Phred+64,  raw reads typically (3, 40)
     with 0=unused, 1=unused, 2=Read Segment Quality Control Indicator (bold) 
 L - Illumina 1.8+ Phred+33,  raw reads typically (0, 41)
```
(See complete image and much more discussion at <a href="https://en.wikipedia.org/wiki/FASTQ_format"> Wikipedia</a>)
 
Quality scores range from -5 to 40, on a somewhat overlapping range of ASCII encoded numbers, such that if your data happened to all have quality scores of 'F' and you didn't know how they were sequenced, it would be impossible to know whether 'F' meant the were all quality 38/40 from Sanger(which is quite good), or quality 6 from Illumina 1.5 (which is quite not good). In practice, you'll almost always have a good range of scores in your data, and by carefully comparing your quality scores to the chart above, you can usually work out where your documentation-challenged collegue got those samples they want you to analyze. (There's also a much easier way, which we'll get to at FastQC)

