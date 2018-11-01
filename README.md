# ee282homework3

Homework 3 for EE282 class (Qingda Hu)

```
wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/dmel-all-chromosome-r6.24.fasta.gz
wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/md5sum.txt
md5sum dmel-all-chromosome-r6.24.fasta.gz
md5sum -c md5sum.txt 
zgrep '^[AGCTN]' dmel-all-chromosome-r6.24.fasta.gz | wc -m
zgrep '^[AGCTN]' dmel-all-chromosome-r6.24.fasta.gz |tr -cd 'N'|wc -m 
zgrep '^>' dmel-all-chromosome-r6.24.fasta.gz | wc -l
wget ftp://ftp.flybase.org:21/genomes/dmel/current/gtf/dmel-all-r6.24.gtf.gz
wget ftp://ftp.flybase.org:21/genomes/dmel/current/gtf/md5sum.txt
md5sum -c md5sum.txt.1
zcat dmel-all-r6.24.gtf.gz | gawk -F '\t' '{print $3}'  | sort | uniq -c |sort -nr
zcat dmel-all-r6.24.gtf.gz | gawk -F '\t' '$3 == "gene" {print $1}'  | sort | uniq -c |sort -nr
```


## Summarize a genome assembly

### Pull the most current Drosophila genome from flybase

`wget ftp://ftp.flybase.net/releases/FB2018_05/`

to get the list of files in that directory. From this file we can find the link for the files we want.

Since we just want the genome:

`wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/dmel-all-chromosome-r6.24.fasta.gz`

### File integrity

Since we need to check MD5 sum, we will need to get the MD5sums:

`wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/md5sum.txt`

The md5sum for dmel-all-chromosome-r6.24.fasta.gz is 71a25289ae2e630d5247856dc2a67ab1.

Running md5sum on the dowloaded gives 71a25289ae2e630d5247856dc2a67ab1. 

`md5sum dmel-all-chromosome-r6.24.fasta.gz`

Alternatively I can automatically check the MD5sum but since I didn't download all the files, I have to search for the 'OK'. I tried to pipe md5sum -c into grep but it didn't work. 

` md5sum -c md5sum.txt  `

### Calculate the following for the whole genome:

1. Total number of nucleotides

Since fasta is formatted with labels starting with '>' and sequences starting with A/G/C/T/N, I can use grep to only take the lines with sequences and then count the number of characters.

`zgrep '^[AGCTN]' dmel-all-chromosome-r6.24.fasta.gz | wc -m` 

The number of nucleotides is 145523498.

2. Total number of Ns

To count the number of Ns, I can trim all the characters other than N with tr. This is likely not the most effecient way to do this. 

`zgrep '^[AGCTN]' dmel-all-chromosome-r6.24.fasta.gz |tr -cd 'N'|wc -m `

The output is 1152978.

3. Total number of sequences

To count the number of sequences, I can count the number of lines starting with '>' which signifies a sequence in FASTA format.

`zgrep '^>' dmel-all-chromosome-r6.24.fasta.gz | wc -l`

1870

## Summarize an annotation file

### File integrity

Similar to above.

```
wget  ftp://ftp.flybase.org/genomes/dmel/current/gtf/
wget ftp://ftp.flybase.org:21/genomes/dmel/current/gtf/dmel-all-r6.24.gtf.gz
wget ftp://ftp.flybase.org:21/genomes/dmel/current/gtf/md5sum.txt
md5sum -c md5sum.txt.1 
```

### Print a summary report with the following information:

1. Total number of features of each type, sorted from the most common to the least common

Remove all lines that are sequence, label, or with #. Take the 3rd column and count unique elements. 

` zcat dmel-all-r6.24.gtf.gz | gawk -F '\t' '{print $3}'  | sort | uniq -c |sort -nr`

|  count | type  |
|---|---|
 |187315| exon|
 |161014| CDS|
 |46339| 5UTR|
 |33358| 3UTR|
 |30591| start_codon|
 |30533| stop_codon|
 |30507| mRNA|
 |17772| gene|
 |2961| ncRNA|
 |485| miRNA|
 |334| pseudogene|
 |312| tRNA|
 |299| snoRNA|
 |262| pre_miRNA|
 |115| rRNA|
 |32| snRNA|
      
2. Total number of genes per chromosome arm (X, Y, 2L, 2R, 3L, 3R, 4)

`zcat dmel-all-r6.24.gtf.gz | gawk -F '\t' '$3 == "gene" {print $1}'  | sort | uniq -c |sort -nr`


|  count | chromosome/scaffold  |
|---|---|
|4202 |3R|
|3628 |2R|
|3501 |2L|
|3464 |3L|
|2676 |X|
|113 |Y|
|111 |4|
|38 |mitochondrion_genome|
|21 |rDNA|
|2 |Unmapped_Scaffold_8_D1580_D1567|
|2 |211000022280494|
|1 |211000022280703|
|1 |211000022280481|
|1 |211000022280347|
|1 |211000022280341|
|1 |211000022280328|
|1 |211000022279681|
|1 |211000022279392|
|1 |211000022279264|
|1 |211000022279188|
|1 |211000022279165|
|1 |211000022278760|
|1 |211000022278449|
|1 |211000022278436|
|1 |211000022278279|
