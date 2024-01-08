---
title: scRNA analysis
---

- [Tools available](#tools-available)
- [Getting started](#getting-started)
- [Quality control](#quality-control)
- [Example](#example)
- [Useful resources](#useful-resources)


### Tools available

Our focus will be on using the R package Seurat (v5.0, released in late 2023), but this is a somewhat arbitrary choice. There are other collections of single cell analysis tools that may be better suited for specific use-cases:

[scverse](https://scverse.org/)

[Biocondcutor](https://bioconductor.org/books/release/OSCA/)

To save time, we have a number of single cell functions available as part of our "CuSTOM App" (available [here](https://github.com/ZornLab/CuSTOM_app)) that use Seurat behind the scenes. This page will explain some of the how and why behind our choices and help you write your own scripts.

### Getting started

The classic workflow from raw counts to a final UMAP can be found in the PBMC 3K tutorial shown [here](https://satijalab.org/seurat/articles/pbmc3k_tutorial). 

This example assumes you are working with a single, scRNA-seq dataset, meaning it does not cover integrating multiple datasets or working with multimodal data.

The creators of this tutorial mention it only briefly, but there is a problem with how the normalization is handled. The "LogNormalize" approach performed by the NormalizeData() function has inherent shortcomings detailed in these papers:

[Normalization and variance stabilization of single-cell RNA-seq data using regularized negative binomial regression](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1874-1)

[Feature selection and dimension reduction for single-cell RNA-Seq based on a multinomial model](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1861-6)

We highly recommend looking at the details of the "sctransform" approach shown [here](https://satijalab.org/seurat/articles/sctransform_vignette) and incorporating it into your analysis. This does require making some small modifications downstream for integration and marker idenfication.

Some other general guidelines are not to worry too much about the PCA/dimensionality, and instead use a default value of say 30, but this is not a strict rule. In contrast, you are encouraged to try out multiple resolution values when performing clustering with the FindClusters() function, as this will have a dramatic impact on how many clusters it finds. You will want to compare and draw conclusions based on the cell type composition you expect in the dataset. 

Finally, the "differentially expressed features" section demonstrates the FindMarkers() function. The literature suggests that the default method (the Wilcox rank sum test) is not optimal and "method.use" should instead be set to "MAST" (see this [benchmarking study](https://academic.oup.com/bib/article/23/5/bbac286/6649780) for more information). In the specific circumstance that you are working with biological replicates, pseudobulk is highly recommended and has been implemented within Seurat (detailed [here](https://satijalab.org/seurat/articles/de_vignette)).

### Quality control

Many aspects of single cell analysis can be automated, meaning they will be run the same way across datasets without usually changing any parameters. Quality control or "QC" is an exception to this, as every dataset will have unique challenges depending on the sample preparation, tissue type, platform, etc.

Two important aspects are the removal of doublets/multiplets and the removal of cell-free RNA. Note that these are aspects that need to be handled outside of Seurat by additional tools. Below we provide the details for the two we currently use.

[SoupX](https://github.com/constantAmateur/SoupX)

[DoubletFinder](https://github.com/chris-mcginnis-ucsf/DoubletFinder)

Within Seurat, additional filtering should be performed to remove cells that have signs of low-quality. As the PBMC tutorial shows, the three most important generally are:

- Number of counts
- Number of genes
- Mitochondrial RNA percentage

### Example

The most basic example, assuming you have already converted your counts to an unprocessed Seurat object, will look similar to the following:

```
	seurat <- SCTransform(seurat, variable.features.n = 3000) %>%
	RunPCA(npcs=30) %>%
	FindNeighbors(dims = 1:30) %>%
	FindClusters(resolution = c(0.8) %>%
	RunUMAP(dims = 1:30) %>%
	return(seurat)
```

### Useful resources

[Open Problems](https://openproblems.bio/results/)

[Single-cell best practices](https://www.sc-best-practices.org/preamble.html)


