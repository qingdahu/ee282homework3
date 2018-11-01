# ee282homework3
Homework 3 for EE282 class (Qingda Hu)

`wget ftp://ftp.flybase.net/releases/FB2018_05/
wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/dmel-all-chromosome-r6.24.fasta.gz
wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/md5sum.txt
md5sum dmel-all-chromosome-r6.24.fasta.gz
md5sum -c md5sum.txt 
zgrep '^[AGCTN]' dmel-all-chromosome-r6.24.fasta.gz | wc -m
zgrep '^[AGCTN]' dmel-all-chromosome-r6.24.fasta.gz |tr -cd 'N'|wc -m 
zgrep '^>' dmel-all-chromosome-r6.24.fasta.gz | wc -l
`



##Summarize a genome assembly
### Pull the most current Drosophila genome from flybase

`wget ftp://ftp.flybase.net/releases/FB2018_05/`
to get the list of files in that directory. From this file we can find the link for the files we want.

Since we just want the genome:
`wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/dmel-all-chromosome-r6.24.fasta.gz`

###File integrity

Since we need to check MD5 sum, we will need to get the MD5sums:
`wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/md5sum.txt`
The md5sum for dmel-all-chromosome-r6.24.fasta.gz is 71a25289ae2e630d5247856dc2a67ab1.

Running md5sum on the dowloaded gives 71a25289ae2e630d5247856dc2a67ab1. 
`md5sum dmel-all-chromosome-r6.24.fasta.gz`

Alternatively I can automatically check the MD5sum but since I didn't download all the files, I have to search for the 'OK'. I tried to pipe md5sum -c into grep but it didn't work. 
` md5sum -c md5sum.txt  `

###Calculate the following for the whole genome:

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

##Summarize an annotation file



