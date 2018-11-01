## ee282homework3
Homework 3 for EE282 class (Qingda Hu)


# Pull the most current Drosophila genome from flybase

`wget ftp://ftp.flybase.net/releases/FB2018_05/`
to get the list of files in that directory. From this file we can find the link for the files we want.

Since we just want the genome:
`wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/dmel-all-chromosome-r6.24.fasta.gz`

Since we need to check MD5 sum, we will need to get the MD5sums:
`wget ftp://ftp.flybase.net:21/genomes/Drosophila_melanogaster/current/fasta/md5sum.txt`
The md5sum for dmel-all-chromosome-r6.24.fasta.gz is 71a25289ae2e630d5247856dc2a67ab1.

Running md5sum on the dowloaded gives 71a25289ae2e630d5247856dc2a67ab1. 
`md5sum dmel-all-chromosome-r6.24.fasta.gz`
