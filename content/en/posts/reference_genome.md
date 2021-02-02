+++
title = "Reference genome"
date = "2021-01-28T16:17:15-05:00"
categories = ["bioinfo"]
tags = [""]
slug = "reference_genome"
toc = true
draft = false
+++

A brief introduction for reference genome in FASTA and other format.

<!--more-->

## Human reference genome

[Genomes – NCBI Datasets BETA](https://www.ncbi.nlm.nih.gov/datasets/genomes/): Download a genome dataset including genome, transcript and protein sequence, annotation and a data report

**GRCh38** (latest version -GRCh38.p13): 

Introduction: https://www.ncbi.nlm.nih.gov/assembly/GCF_000001405.39

ftp://ftp.ensembl.org/pub/current_fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz

By chromosome: ftp://ftp.ensembl.org/pub/current_fasta/homo_sapiens/dna/

**GRCh37** (latest version -GRCh37.p13):

Introduction: https://www.ncbi.nlm.nih.gov/assembly/GCF_000001405.13/

ftp://ftp.ensembl.org/pub/grch37/current/fasta/homo_sapiens/dna/Homo_sapiens.GRCh37.dna_sm.primary_assembly.fa.gz

ftp://hgdownload.cse.ucsc.edu/goldenPath/hg19/hg19Patch13/hg19Patch13.fa.gz 


### Download command
```
wget ftp://ftp.ensembl.org/pub/current_fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz \
-O -| gunzip -c > target_location
```

### Create the fasta index file
```
samtools faidx ref.fasta
```

## Other issue

### toplevel fasta VS primary_assembly fasta

**toplevel fasta**

Ensembl advise using the full toplevel fasta reference when doing CrossMapping, and for GRCh38, that file is HUGE, (36G instead of the usual 3G, containing all the ALT sequences). As CrossMap loads the reference into memory, this makes a big difference. However, the resulting mapped files are identical for mappings made with the toplevel file as with the primary_assembly file (which does not contain all the ALT seqs), so it is preferable to use the latter from a resources point of view.

**Primary assembly**

contains all toplevel sequence regions excluding haplotypes and patches. This file is best used for performing sequence similarity searches
where patch and haplotype sequences would confuse analysis. 

### .fa / .fna / .faa/ .ffn/ .mpfa/ .frn/ .fastq

.fasta, .fas, .fa, .seq, .fsa: Generic FASTA

.fna: FASTA nucleic acid 

.faa: FASTA amino acids, for protein sequences

.ffn: FASTA nucleotide coding regions for a genome

.mpfa: FASTA amino acides in multiple proteins

.frn: FASTA non-coding RNA

.fastq: FASTQ

### GRCh37 issue

**GRCh37 hg19 b37 humanG1Kv37 - Human Reference Discrepancies**

There are 4 common "hg19" references, and they are NOT directly interchangeable:

-hg19 (`ucsc.hg19.fasta`, MD5sum: `a244d8a32473650b25c6e8e1654387d6`). hg19 is UCSC's variant of the official GRCh37 assembly.

-b37 (`Homo_sapiens_assembly19.fasta`, MD5sum: `886ba1559393f75872c1cf459eb57f2d)`

-GRCh37 (`GRCh37.p13.genome.fasta`, MD5sum: `c140882eb2ea89bc2edfe934d51b66cc`)

-humanG1Kv37 (`human_g1k_v37.fasta`, MD5sum: `0ce84c872fc0072a885926823dcd0338`)

More details: https://gatk.broadinstitute.org/hc/en-us/articles/360035890711-GRCh37-hg19-b37-humanG1Kv37-Human-Reference-Discrepancies

**prefix "chr" issue**

hg19 or early releases of GRCh37 like `GRCh37-lite`, did not use chr-prefixes, but newer releases like `GRCh37.p13` adopted the chr-prefix, and use a newer mitochondrial (MT) sequence than hg19 does. chrM in hg19 is named MT in GRCh37. 
```
(base) [c-panz@sumner-log2 reference]$ head GRCh37.fa
>1 dna_sm:chromosome chromosome:GRCh37:1:1:249250621:1 REF
nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn
nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn
nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn
```
!Attention: DO NOT use `sed`/`cat` or other find/replace tools to fix this problem yourself (unless you are extremely bandwidth-constrained or no option to download a properly-formatted reference FASTA).

More discussion: [Question: Human dna reference file with no prefix 'chr'](https://www.biostars.org/p/119295/#119308)

## Reference

[GATK: Reference genome](https://gatk.broadinstitute.org/hc/en-us/articles/360035891071)

[GATK: Human genome reference builds - GRCh38 or hg38 - b37 - hg19](https://gatk.broadinstitute.org/hc/en-us/articles/360035890951-Human-genome-reference-builds-GRCh38-or-hg38-b37-hg19)

[Heng Li: Which human reference genome to use?](https://lh3.github.io/2017/11/13/which-human-reference-genome-to-use)

[Get to Know Your Reference Genome (GRCh37 vs GRCh38)](https://bitesizebio.com/38335/get-to-know-your-reference-genome-grch37-vs-grch38/)

[关于人类基因组的一些说明](https://wenlongshen.github.io/2020/03/26/Reference-Genome/)

https://wabi-wiki.scilifelab.se/display/SHGATG/gatk+bundle+in+hg38

ftp://ftp.ensembl.org/pub/grch37/current/fasta/homo_sapiens/dna/README

