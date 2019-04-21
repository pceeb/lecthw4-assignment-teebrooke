# Homework4. Write a bash script.  

## The deadline to turning this homework is ** Wednesday at 11:00:00pm **   

In this homework you will work with the file `hg19.gtf` located at `~/classdata`. This is a simple tab-delimited text file for describing genomic features and 
consists of one line per feature, each containing 9 columns of data:  

- **seqname**: name of the chromosome or scaffold; chromosome names can be given with or without the 'chr' prefix. Important note: the seqname must be one used within Ensembl, i.e. a standard chromosome name or an Ensembl identifier such as a scaffold ID, without any additional content such as species or assembly. See the example GFF output below.  
- **source**: name of the program that generated this feature, or the data source (database or project name)  
- **feature**: feature type name, e.g. Gene, Variation, Similarity  
- **start**: Start position of the feature, with sequence numbering starting at 1.  
- **end**: End position of the feature, with sequence numbering starting at 1.  
- **score**: A floating point value.  
- **strand**: defined as + (forward) or - (reverse).  
- **frame**: One of '0', '1' or '2'. '0' indicates that the first base of the feature is the first base of a codon, '1' that the second base is the first base of a codon, and so on..  
- **attribute**: A semicolon-separated list of tag-value pairs, providing additional information about each feature.  

First copy the file `hg19.gtf` located at `~/classdata` into your `HOME` directory. 
Let's look at the file:  
```bash
[c177-t0@n9998 ~]$ head less
```

```
chr2	hg18_knownGene_GnfAtlas2	exon	31608	31627	0.000000	-	.	gene_id "DUMMYCLUSTER.1"; transcript_id "uc002qvt.1";
chr2	hg18_knownGene_GnfAtlas2	exon	35440	36385	0.000000	-	.	gene_id "DUMMYCLUSTER.1"; transcript_id "uc002qvt.1";
chr2	hg18_knownGene_GnfAtlas2	exon	229563	232178	0.000000	-	.	gene_id "DUMMYCLUSTER.1"; transcript_id "uc002qwb.2";
chr2	hg18_knownGene_GnfAtlas2	exon	208155	209001	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	214864	214920	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	219966	220044	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	221023	221191	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	223101	223229	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	224160	224272	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	237538	237602	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
```

This file contains information related to three different chromosomes.  

```bash
[c177-t0@n9998 ~]$ cut -f 1 hg19.gtf | uniq
```
~~~
chr2
chr21
chr3
~~~

Supose you want to create a file with information related to `chr2`. First you may 
want to use `grep` to show only the lines that have the field `chr2`. To evaluate if `grep` is doing the job you can
summarize the output with a combination of 
`cut` to display only the 1st column and `uniq` to display unique values.  

```bash
[c177-t0@n9998  ~]$ grep "chr2" hg19.gtf | cut -f 1 | uniq
```
~~~
chr2
chr21
~~~

The problem with the code above is that is taking both "chr2" and "chr21". To solve this you can do:  

```bash
[c177-t0@n9998  ~]$ grep -P "chr2\t" hg19.gtf | cut -f 1 | uniq
```
~~~
chr2
~~~
`-P` allows grep to read `\t` as an actual tab. Nice! Now we can create a file that contains only information of `chr2`

```bash
[c177-t0@n9998 ~]$ grep -P "chr2\t" hg19.gtf > <some_file>.gtf
```


# What do you have to do?    
**Create a bash script called `Split_GTF.sh` which will split the `hg19.gtf` into files corresponding to every chr (2,3,21), 
save every file in separate directory called chr${i}_gtf.**

Your script should be called like this:  
```bash
sh Split_GTF.sh hg19.gtf   
```
If everything works you should see the following:  
Three directories  
```bash
[c177-t0@n9998 ~]$ ls -d chr*
```
~~~
chr21_gtf  chr2_gtf  chr3_gtf
~~~

Every directory should contained a file with information about a particular chromosome, like this:  
```bash
[c177-t0@n9998 ~]$ head chr21_gtf/chr21.gtf
```
~~~
chr21	hg18_knownGene_GnfAtlas2	exon	9928614	9928911	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9930696	9930766	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9932178	9932270	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9936234	9936313	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9938241	9938346	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9941955	9942035	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9943805	9943866	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9955723	9955811	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9955910	9955991	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
chr21	hg18_knownGene_GnfAtlas2	exon	9956808	9956868	0.000000	-	.	gene_id "220205_at"; transcript_id "uc002yip.1";
~~~
```bash
[c177-t0@n9998 ~]$ head chr2_gtf/chr2.gtf
```
~~~
chr2	hg18_knownGene_GnfAtlas2	exon	31608	31627	0.000000	-	.	gene_id "DUMMYCLUSTER.1"; transcript_id "uc002qvt.1";
chr2	hg18_knownGene_GnfAtlas2	exon	35440	36385	0.000000	-	.	gene_id "DUMMYCLUSTER.1"; transcript_id "uc002qvt.1";
chr2	hg18_knownGene_GnfAtlas2	exon	229563	232178	0.000000	-	.	gene_id "DUMMYCLUSTER.1"; transcript_id "uc002qwb.2";
chr2	hg18_knownGene_GnfAtlas2	exon	208155	209001	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	214864	214920	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	219966	220044	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	221023	221191	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	223101	223229	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	224160	224272	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
chr2	hg18_knownGene_GnfAtlas2	exon	237538	237602	0.000000	-	.	gene_id "204019_s_at"; transcript_id "uc002qvu.1";
~~~
```bash
[c177-t0@n9998 ~]$ head chr3_gtf/chr3.gtf
```
~~~
chr3	hg18_knownGene_GnfAtlas2	exon	213650	213746	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	261296	261375	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	336366	336550	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	342642	342747	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	344850	345037	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	357477	357599	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	358595	358765	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	359667	359714	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	361272	361392	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
chr3	hg18_knownGene_GnfAtlas2	exon	366042	366226	0.000000	+	.	gene_id "204591_at"; transcript_id "uc003bot.1";
~~~

# How to submit your Homework. 
Include the scripts `Split_GTF.sh` in this repository.  

## Grade HW4: 20/20

| **Rubric** | **5pt** | **4pt** | **3pt** | **2pt** | **1pt** |
| --- | ---| --- | --- | --- | --- |
| In-Lab work | **X** | | | |
| Challenge - Effort | **X** | | | |
| Challenge - Accuracy | **X** | | | |
| Challenge - Timely Submission | **X** | | | |
