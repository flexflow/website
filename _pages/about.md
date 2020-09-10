---
title: About FlexFlow
layout: single
permalink: /about/
#toc: true
#toc_sticky: true
author_profile: true
classes: wide
header:
  overlay_image: /assets/images/header.jpg 
---

FlexFlow is a DNN system that automatically discovers fast parallelization strategies for distributed DNN training.
FlexFlow generalizes and goes beyond today's manually designed parallelization strategies (e.g., data and model parallelism) for distributed DNN training by exploring parallelization opportunities across different Samples, Operators, Attributes, and Parameters.

FlexFlow includes a novel execution simulator to evaluate the runtime performance of different strategies and uses an automated search algorithm to discover optimized strategies that outperform existing manually designed strategies.

FlexFlow provides the following main features:

* **Flexible Parallelization**. FlexFlow supports parallelizing DNN training through combinations of the Sample, Operator, Attribute, and Parameter dimensions, and guarantees that different strategies maintain the same model accuracy by design.

* **Performance Autotuning**. To parallelize DNN training on a specific parallel machine, FlexFlow uses guided randomized search algorithm to automatically find fast parallelization strategies while requiring no manual effort.

* **Keras Support**. FlexFlow offers a drop-in replacement for TensorFlow Keras and transparently accelerates existing Keras programs by discovering faster parallelization strategies.

* **Large-Scale GNNs**. FlexFlow enables fast graph neural network (GNN) training on large graphs (e.g., billion-edge) by distributing GNN computations across multiple GPUs (potentially on multiple compute nodes) using [attribute parallelism](https://cs.stanford.edu/~zhihao/papers/mlsys20.pdf).


