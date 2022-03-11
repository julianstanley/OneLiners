# OneLiners

## Fasta files
Get the first 50 nucleotides in every sequence in a fasta file:

```
seqkit subseq -r 1:49 my_sequences.fasta
```


## Bash loops
Do some operation that outputs a list of things you want to loop over. For example, if I just want one column of a tab-delim file:
```
for line in $(cut -f1 Expression_leadered.txt); do echo $line; done
```

## NCBI
Generally you can get genes with `esearch`. E.g. for the Caulobacter gene CCNA_01405, I can fetch the sequence with:

```
esearch -db gene -query "CCNA_01405[SYMBOL]" | efetch -format docsum | xtract -pattern GenomicInfoType -element ChrAccVer ChrStart ChrStop | xargs -n 3 sh -c 'efetch -db nuccore -format fasta -id "$0" -chr_start "$1" -chr_stop "$2"'
```
