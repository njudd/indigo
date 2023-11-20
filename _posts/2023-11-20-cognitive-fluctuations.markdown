---
title: "Cognitive fluctuations"
layout: post
date: 2023-11-22 08:10
#tag: jekyll
# image: /assets/proj_imgs/spatialcognition/img1.png
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "Cognitive fluctuations: How a variability perspective can offer a novel phenotype"
category: project
#author: johndoe
externalLink: false
---

# How a variability perspective can offer a novel phenotype


We set out to answer a few fundamental questions on variability:

1. **Ubiquity** are interindividual differences in intraindividual variability a consistent property of cognitive tasks?

2. **Structure** how are individual differences in variability across tasks related?

3. **Discrimination** is variability a distinct concept from mean performance?


For an in-depth look check out the [**preprint**](https://psyarxiv.com/b29rn/) or [OSF](https://osf.io/z53an/) for code! If you have any further questions just reach out and ask me :)

 ![img1](/assets/proj_imgs/spatialcognition/img1.png)

### Abstract

Our performance on cognitive tasks fluctuates: the same individual completing the same task will differ in their response’s moment-to-moment. For decades cognitive fluctuations have been implicitly ignored – treated as measurement error – with a focus instead on aggregates such as mean performance. Leveraging dense trial-by-trial data and novel time-series methods we explored variability as an intrinsically important phenotype. Across eleven cognitive tasks with over 7 million trials, we found highly reliable interindividual differences in cognitive variability in every task we examined. These differences are both qualitatively and quantitatively distinct from mean performance. Moreover, we found that a single dimension for variability across tasks was inadequate, demonstrating that previously posited global mechanisms for cognitive variability are at least partially incomplete. Our findings indicate that variability is a fundamental part of the human phenotype, with the potential to offer rich, novel insights into cognitive performance.

<iframe src="https://docs.google.com/file/d/1RY6igAo6OHZ7_L4cUQKx7pNZI5sKsU02/preview" width="560" height="310" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>

---
### Brief Overview

Every child completed identical training in the first week, on the 2nd week (out of 7) they were randomized into one of the 5 training plans below. These plans differed on the amounts of working memory, rotation, or non-verbal reasoning exercises. 

![img2](/assets/proj_imgs/spatialcognition/img2.png)

![img4](/assets/proj_imgs/spatialcognition/img4.png)

---
We measured mathematics at three timepoints with in-app tests (i.e., addition, subtraction & number comparison) which we combined into a latent mathematical factor.

![measuremod](/assets/proj_imgs/spatialcognition/Vektor_measuremod_strict.png)


<div class="side-by-side">
    <div class="toleft">
        <img class="image" src="https://njudd.com/assets/proj_imgs/spatialcognition/img3.png" alt="Alt Text">
        <figcaption class="caption"></figcaption>
    </div>

    <div class="toright">
        <p> As expected this mathematical factor was highly correlated with mean performance in the training tasks in the first week. As seen on the training curves below all of the trained tasks significantly improved over the seven weeks. The lower correlation between NVR and baseline Math is most likely due to constrained variance in the first week, which can be seen on the training curves of NVR.</p>
    </div>
</div>

![img5](/assets/proj_imgs/spatialcognition/img5.png)

---

<div class="side-by-side">
    <div class="toleft">
        <img class="image" src="https://njudd.com/assets/proj_imgs/spatialcognition/img6.png" alt="Alt Text">
        <figcaption class="caption">Improvement from each domain</figcaption>
    </div>

    <div class="toright">
        <p> After 7 weeks we found non-verbal reasoning (NVR) to have the largest effect on mathematical improvement, followed by working memory. Conceptually we grouped Tangram & 2D rotation as both rotation tasks. Since this study had no passive control we cannot claim rotation has no effect on mathematics, just that it has less than working memory and non-verbal reasoning. </p>
    </div>
</div>


It is hard to estimate the effect size of our intervention since we have no training plans without cognitively demanding tasks. Another consideration is that we only changed 30% of the training programs, therefore all children completed a similar 70% of mathematic and working memory training. The difference between the least effective (rotation heavy) and most effective training plan (NVR only) was .06 SD’s. 

While this would be classically considered a very small effect size. Using modern effect size metrics in education this would be classified as an intervention with a medium effect which has a low cost of implementation and is easy to scale ([Kraft, 2020](https://paperpile.com/shared/ItPIu0)). For a list of relevant recent effect size literature see section '[effectsizes](https://njudd.com/effectsize)'.




