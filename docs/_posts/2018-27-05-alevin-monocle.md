---
title:  "How to Use alevin with Monocle"
date:   2018-05-27 15:04:23
categories: [tutorial]
tags: [alevin]
---
## Alevin-Monocle Connection





```R
library(tximport)
library(monocle3)
```


```R
# path to the output directory of Alevin run of neurons_900 10x data
files <- file.path("alevin_quants/alevin/quants_mat.gz")
file.exists(files)
```
TRUE

```R
# Reading in the alevin quants quants
txi <- tximport(files, type="alevin")
```


```R
# and we are good to go !! Cells after this has been taken from Monocle tutrial:
# http://cole-trapnell-lab.github.io/monocle-release/docs/#constructing-single-cell-trajectories
# Below lines are for example purposes only and could be suboptimal. We recommend
# checking out Monocle tool for more detailed tutorial of the downstream analysis.
```


```R

```


```R
# converting the the sparse matrix to dense for monocle parsing.
pbmc <- new_cell_data_set(as.matrix(txi$counts))
```

```R
## Step 1: Normalize and pre-process the data
pbmc = preprocess_cds(pbmc, num_dim = 100)

## Step 2: Reduce the dimensions using UMAP
pbmc = reduce_dimension(pbmc)

## Step 3: Cluster the cells
pbmc <- cluster_cells(pbmc)

## Step 4: Learn a graph
pbmc <- learn_graph(pbmc)

## Step 5: Order cells
pbmc <- order_cells(pbmc, root_cells=pbmc$cell[[1]] )

plot_cells(pbmc)
```
![png](../../images/output_10_1.png)