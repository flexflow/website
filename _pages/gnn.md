---
title: Large-Scale GNNs
layout: single
permalink: /gnn/
classes: wide
#toc: true
#toc_sticky: true
author_profile: true
header:
  overlay_image: /assets/images/header.jpg 
---

Graph neural networks (GNNs) combine DNN techniques (e.g., convolution) with iterative graph propagation (e.g., neighbor aggregation) and have been demonstrated to be an effective model for learning tasks related to graph structured data.
However, existing DNN frameworks cannot easily support GNN training and inference on large-scale graphs, since different from conventional DNN models, GNNs generally use small DNN models on very large and irregular input graphs that do not fit in a single GPU.

FlexFlow enables fast GNN training on large (e.g., billion-edge) graphs using [attribute parallelism](https://cs.stanford.edu/~zhihao/papers/mlsys20.pdf), which leverages the compute resources of multiple GPUs to train GNN models on large (e.g., billion-edge) real-world graphs.

<figure>
<img src="/assets/images/attribute_parallelism.jpg">
</figure>

See [examples](https://github.com/jiazhihao/roc) for using FlexFlow to train GNN models.
