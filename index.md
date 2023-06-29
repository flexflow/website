---
layout: splash
permalink: /
hidden: true
header:
  overlay_color: "#010005"
  overlay_image: /assets/images/Banner.png
excerpt: >
  Automatically Discovering Fast Parallelization Strategies for Distributed Deep Neural Network Training<br />

feature_row:
  - title: "Joint Optimization"
    excerpt: "FlexFlow uses a novel hierarchical search algorithm to jointly optimize algebraic transformations and parallelization while maintaining scalability."
    url: "https://www.cs.cmu.edu/~zhihaoj2/papers/unity_osdi22.pdf"
    btn_class: "btn--primary"
    btn_label: "Learn more" 
  - title: "Flexible Parallelization"
    excerpt: "FlexFlow supports parallelizing DNN training through combinations of the Sample, Operator, Attribute, and Parameter dimensions."
    url: "https://cs.stanford.edu/~zhihao/papers/sysml19a.pdf"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Speculative Inference"
    excerpt: "FlexFlow accelerates generative LLM inference with speculative inference and token tree verification."
    url: "/specInfer/"
    btn_class: "btn--primary"
    btn_label: "Learn more"  
  - title: "Videos"
    excerpt: "Peruse a collection of youtube videos about FlexFlow."
    url: "https://www.youtube.com/"
    btn_class: "btn--primary"
    btn_label: "Watch" 
 
---

<div style="padding-right: 10%;padding-left: 10%;" >

FlexFlow is a DNN framework that automatically discovers fast parallelization strategies for distributed DNN training.
FlexFlow generalizes and goes beyond today's manually designed parallelization strategies (e.g., data and model parallelism) for distributed DNN training by exploring parallelization opportunities across different Samples, Operators, Attributes, and Parameters.

FlexFlow includes a novel execution simulator to evaluate the runtime performance of different strategies and uses an automated search algorithm to discover highly optimized strategies, which generally outperform today's manually designed strategies.

{% include feature_row %}

</div>

