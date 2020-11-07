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
  <small><a href="https://github.com/flexflow/FlexFlow/tree/r20.08">Latest release r20.08</a></small>
feature_row:
  - title: "Performance Autotuning"
    excerpt: "FlexFlow accelerates DNN training by automatically discovering fast parallelization strategies for a specific parallel machine."
    url: "/search/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Keras Support"
    excerpt: "FlexFlow provides a drop-in replacement for TensorFlow Keras and requires only a few lines of changes to existing Keras programs."
    url: "/keras/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Large-Scale GNNs"
    excerpt: "FlexFlow enables fast graph neural network training and inference on large-scale graphs by exploring attribute parallelism."
    url: "/gnn/"
    btn_class: "btn--primary"
    btn_label: "Learn more"      
---

{% include feature_row %}
