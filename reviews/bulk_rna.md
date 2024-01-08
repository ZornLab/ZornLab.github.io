---
title: Bulk RNA analysis
---

## Introduction

Bulk RNA-seq is a good starting place for familiarizing yourself with bioinformatics, as the analysis methods are well-established by this point. The most important choice is deciding the best alignment/quantification method. 

We will go over an all-in-one solution implemented by nf-core that provides multiple options. The details of the pipeline are provided [here](https://nf-co.re/rnaseq/3.13.2)

## Differential expression

There are two widely known tools I would recommend, DESeq2 and edgeR, both of which are very well-documented:

[DESeq2](https://bioconductor.org/packages/devel/bioc/vignettes/DESeq2/inst/doc/DESeq2.html)

[edgeR](https://www.bioconductor.org/packages/release/bioc/vignettes/edgeR/inst/doc/edgeRUsersGuide.pdf)

If possible, you should try to run both and compare results. We will go over a condensed example for each to help you get started, but the specifics can change depending on your experiment.

### DESeq2

### edgeR