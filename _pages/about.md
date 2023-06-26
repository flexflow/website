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

FlexFlow is a DNN framework that automatically discovers fast parallelization strategies for distributed DNN training.
FlexFlow generalizes and goes beyond today's manually designed parallelization strategies (e.g., data and model parallelism) for distributed DNN training by exploring parallelization opportunities across different Samples, Operators, Attributes, and Parameters.

FlexFlow includes a novel execution simulator to evaluate the runtime performance of different strategies and uses an automated search algorithm to discover highly optimized strategies, which generally outperform today's manually designed strategies.

FlexFlow provides the following key features:

* **Flexible Parallelization**. FlexFlow supports parallelizing DNN training through combinations of the [Sample, Operator, Attribute, and Parameter](https://cs.stanford.edu/~zhihao/papers/sysml19a.pdf) dimensions, and guarantees that different parallelization strategies maintain the same model accuracy by design.

* **Joint Optimization**. FlexFlow uses a novel hierarchical search algorithm
to jointly optimize [algebraic transformations and parallelization](https://www.cs.cmu.edu/~zhihaoj2/papers/unity_osdi22.pdf) while maintaining scalability.

* **Speculative Inference**. FlexFlow accelerates generative LLM inference with [speculative inference and token tree verification](https://arxiv.org/abs/2305.09781).