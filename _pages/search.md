---
title: Performance Autotuning
layout: single
permalink: /search/
classes: wide
#toc: true
#toc_sticky: true
author_profile: true
header:
  overlay_image: /assets/images/header.jpg 

---

FlexFlow enables performance autotuning by automatically searching for optimized parallelization strategies during model compilation. FlexFlow explores the [SOAP search space](https://cs.stanford.edu/~zhihao/papers/sysml19a.pdf), which identifies four parallelizable dimensions and captures potential parallelization opportunities across different Samples, Operators, Attributes, and Parameters. 

A key property of the SOAP search space is that all strategies perform the same computation defined by the DNN model and therefore maintain the same model accuracy by design. 
FlexFlow performs Markov Chain Monte Carlo (MCMC) search over the SOAP search space to discover performant parallelization strategies for a given parallel machine.

## Searching For Fast Parallelization Strategies

FlexFlow performs MCMC search during model compilation (i.e., `model.compile`) and uses the following configuration flags to control the search procedure.
* `--search-budget` or `--budget` (default 0): the number of iterations for the MCMC search.
* `--search-alpha` or `--alpha` (default 0.05): a hyper-parameter for the search procedure (see below).
* `--export-strategy` or `--export` (default None): path to export the best discovered strategy.
* `--import-strategy` or `--import` (default None): path to import a previous saved strategy.

FlexFlow uses a hyper-parameter alpha (>= 0) to controls the probability that a newly proposed strategy is accepted by the MCMC search. By setting alpha = 0, the MCMC search becomes a fully randomized search algorithm, which accepts all new proposals. As alpha increases, the search algorithm gradually becomes a greedy algorithm that prefers to accepts new proposals that stictly improve the training performance. For more details, see [our paper](https://cs.stanford.edu/~zhihao/papers/sysml19a.pdf).

The MCMC search algorithm starts from data parallelism by default. To guarantee that data parallelism is valid, make sure the global batch size is a multiplier of the total number of GPUs used for training.

To export the best discovered strategy to an external file, set the `--export-strategy` flag.
```
./flexflow_python dlrm.py -ll:gpu 4 -ll:fsize 12000 --search-budget 10000 --export-strategy /path/to/strategy
```

Alternatively, to import a previous saved strategy, simply set the `--import-strategy` flag.
```
./flexflow_python dlrm.py -ll:gpu 4 -ll:fsize 12000 --import-strategy /path/to/strategy
```
Note that by setting the `--import-strategy` flag, FlexFlow will skip the MCMC search procedure and directly use the imported strategy to parallelize training.

## Case Study: Deep Learning Recommendation Model

We use the [Deep Learning Recommendation Model](https://github.com/facebookresearch/dlrm) (DLRM) to demonstrate the FlexFlow performance autotuning.
The model uses embedding layers to process sparse input features representing
categorical data, and uses the bottom neural network to process dense input features. DLRM has a
feature interaction operator that combines the representations learnt from both the dense and sparse
features (e.g., concatenating the representations). The output of the feature interaction operator is
then sent to the top neural network for downstream prediction tasks.

<p align="center">
<img align="center" src="/assets/images/dlrm_overview.jpg" width="600px" />
</p>

Using the following command line, FlexFlow searches for an optimized strategy to parallelize DLRM training on 4 GPUs on a single node.
```
./dlrm -ll:gpu 4 -ll:fsize 12000 -ll:zsize 20000 --arch-sparse-feature-size 64 --arch-embedding-size 1000000-1000000-1000000-1000000-1000000-1000000-1000000-1000000 --arch-mlp-bot 64-512-512-64 --arch-mlp-top 576-1024-1024-1024-1 --batch-size 1024 --budget 1000
```

Different executions of the search procedure may discover different optimized strategies, one of which is shown as follows.
```
========== Strategy Search Started ==========
iter(0) cur(7.93) next(3.46) best(7.93)
iter(100) cur(6.94) next(6.96) best(5.76)
iter(200) cur(6.54) next(7.03) best(5.76)
iter(300) cur(6.75) next(6.75) best(5.68)
iter(400) cur(2.37) next(6.61) best(2.18)
iter(500) cur(2.23) next(2.23) best(2.18)
iter(600) cur(2.41) next(6.86) best(2.11)
iter(700) cur(2.14) next(2.14) best(2.11)
iter(800) cur(2.32) next(6.74) best(2.11)
iter(900) cur(2.80) next(2.80) best(2.11)
iter(1000) cur(2.49) next(6.96) best(2.11)
========== Strategy Search Completed ==========
[Dense_512_100] num_dims(2) dims[1,4] device_ids[0,1,2,3]
[Dense_512_101] num_dims(2) dims[1,1] device_ids[1]
[Dense_64_102] num_dims(2) dims[1,1] device_ids[1]
[Embed_64_103] num_dims(2) dims[1,1] device_ids[0]
[Embed_64_104] num_dims(2) dims[1,1] device_ids[2]
[Embed_64_105] num_dims(2) dims[1,1] device_ids[3]
[Embed_64_106] num_dims(2) dims[1,1] device_ids[2]
[Embed_64_107] num_dims(2) dims[1,1] device_ids[3]
[Embed_64_108] num_dims(2) dims[1,1] device_ids[0]
[Embed_64_109] num_dims(2) dims[1,1] device_ids[2]
[Embed_64_110] num_dims(2) dims[1,1] device_ids[0]
[Concat_1_111] num_dims(2) dims[1,4] device_ids[0,1,2,3]
[Dense_1024_112] num_dims(2) dims[1,4] device_ids[0,1,2,3]
[Dense_1024_113] num_dims(2) dims[1,4] device_ids[0,1,2,3]
[Dense_1024_114] num_dims(2) dims[2,1] device_ids[1,2]
[Dense_1_115] num_dims(2) dims[2,1] device_ids[1,2]
```
Each line describes the parallelization configuration for one operator: `dims` indicates the degree of parallelism for each dimension, and `device_ids` shows the device assignment for each task within an operator.
This strategy combines parallelization opportunities across different Samples, Operators, and Parameters, and is 3.8x faster than data parallelism.
