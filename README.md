# OneLiners

## NCBI
Generally you can get genes with `esearch`. E.g. for the Caulobacter gene CCNA_01405, I can fetch the sequence with:

```
esearch -db gene -query "CCNA_01405[SYMBOL]" | efetch -format docsum | xtract -pattern GenomicInfoType -element ChrAccVer ChrStart ChrStop | xargs -n 3 sh -c 'efetch -db nuccore -format fasta -id "$0" -chr_start "$1" -chr_stop "$2"'
```
