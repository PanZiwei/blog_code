+++
title = "Reference genome"
date = "2021-01-28T16:17:15-05:00"
lastmod = "2021-01-28T16:17:15-05:00"
categories = ["bioinfo"]
tags = [""]
slug = "reference_genome"
toc = true
draft = false
+++

# Human genome 

## Link
GRCh38:

GRCh38.p13(latest version): 
https://www.ncbi.nlm.nih.gov/assembly/GCF_000001405.39
ftp://ftp.ensembl.org/pub/current_fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz
By chromosome: ftp://ftp.ensembl.org/pub/current_fasta/homo_sapiens/dna/

GRCh37:
ftp://ftp.ensembl.org/pub/grch37/current/fasta/homo_sapiens/dna/Homo_sapiens.GRCh37.dna_sm.primary_assembly.fa.gz
ftp://hgdownload.cse.ucsc.edu/goldenPath/hg19/hg19Patch13/hg19Patch13.fa.gz 
GRCh37.p13(latest version): 
https://www.ncbi.nlm.nih.gov/assembly/GCF_000001405.13/


## Download command
```
wget ftp://ftp.ensembl.org/pub/current_fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz \
-O -| gunzip -c > target_location
```

## toplevel fasta VS primiary_assembly fasta

**toplevel fasta**

Ensembl advise using the full toplevel fasta reference when doing CrossMapping, and for GRCh38, that file is HUGE, (36G instead of the usual 3G, containing all the ALT sequences). As CrossMap loads the reference into memory, this makes a big difference. However, the resulting mapped files are identical for mappings made with the toplevel file as with the primary_assembly file (which does not contain all the ALT seqs), so it is preferable to use the latter from a resources point of view.

**Primary assembly**

contains all toplevel sequence regions excluding haplotypes and patches. This file is best used for performing sequence similarity searches
where patch and haplotype sequences would confuse analysis. 

# Reference
[GATK: Reference genome](https://gatk.broadinstitute.org/hc/en-us/articles/360035891071)

[GATK: Human genome reference builds - GRCh38 or hg38 - b37 - hg19](https://gatk.broadinstitute.org/hc/en-us/articles/360035890951-Human-genome-reference-builds-GRCh38-or-hg38-b37-hg19)

[Heng Li: Which human reference genome to use?](https://lh3.github.io/2017/11/13/which-human-reference-genome-to-use)

[Get to Know Your Reference Genome (GRCh37 vs GRCh38)](https://bitesizebio.com/38335/get-to-know-your-reference-genome-grch37-vs-grch38/)

[关于人类基因组的一些说明](https://wenlongshen.github.io/2020/03/26/Reference-Genome/)

https://wabi-wiki.scilifelab.se/display/SHGATG/gatk+bundle+in+hg38

ftp://ftp.ensembl.org/pub/grch37/current/fasta/homo_sapiens/dna/README

