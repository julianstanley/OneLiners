# OneLiners

This repository just contains this README. 

There are tons of little commands that often will (embarrassingly) save me hours of time at the terminal, only for me to forget them later and have to dig through my history trying to find them.

Here, I'll messily compile commands that I found useful, just updating whenver I run into them.

## Separate a bed file into plus and minus genes

```
cat ~/labshare/genome_annotations/Synechococcus_elongatus/NCBI/GCF_014698905.1_ASM1469890v1_genomic.bed | awk '$6 == "-" {print $0}'
```

## Extracting subtext

pcregrep is your friend. For example, to get the start sequences from headers in some fasta files:

```
pcregrep -o1 ">NC_011916\.1:([0-9]+)" leaderless_first35_fold.out
```

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

# Helpful R snippets

## Linear equation on ggplot

```{r}
library(ggpmisc)
stat_poly_line() +
  stat_poly_eq(aes(label = paste(after_stat(eq.label),
                                 after_stat(rr.label), sep = "*\", \"*"))) 
```

## More axis ticks on ggplot

```{r}
scale_y_continuous(breaks = scales::pretty_breaks(n = 24))
```
