---
layout: splash
permalink: /
hidden: true
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/front2.jpg
  actions:
    - label: "<i class='fas fa-download'></i> Install now"
      url: "/start/"
excerpt: >
  Automatically Discovering Fast Parallelization Strategies for Distributed Deep Neural Network Training<br />
  <small><a href="https://github.com/flexflow/FlexFlow">GitHub</a></small>
feature_row:
  - title: "Flexible Parallelization"
    excerpt: "FlexFlow supports parallelizing DNN training through combinations of the Sample, Operator, Attribute, and Parameter dimensions."
    url: "https://cs.stanford.edu/~zhihao/papers/sysml19a.pdf"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Joint Optimization"
    excerpt: "FlexFlow uses a novel hierarchical search algorithm to jointly optimize algebraic transformations and parallelization while maintaining scalability."
    url: "https://www.cs.cmu.edu/~zhihaoj2/papers/unity_osdi22.pdf"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Speculative Inference"
    excerpt: "FlexFlow accelerates generative LLM inference with speculative inference and token tree verification."
    url: "/specInfer/"
    btn_class: "btn--primary"
    btn_label: "Learn more"      
---

{% include feature_row %}
