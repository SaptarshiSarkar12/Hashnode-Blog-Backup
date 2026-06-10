---
title: "The Anatomy of Catastrophic Forgetting"
seoTitle: "From 99% to 34%: Catastrophic Forgetting Demo in CNNs"
seoDescription: "Hands‑on demo of catastrophic forgetting in CNNs with MNIST then fine-tuning on Fashion‑MNIST, showing accuracy collapse, causes and visualisations."
datePublished: 2026-06-10T10:40:46.418Z
cuid: cmq7xu43b00010aht7qo16qg8
slug: the-anatomy-of-catastrophic-forgetting
cover: https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/a2c64047-6f78-4b45-987c-3b8b86f686cf.png
tags: ai, artificial-intelligence, machine-learning, neural-networks, cnn, convolutional-neural-networks, google-colab, continuous-learning, catastrophic-forgetting

---

We train a model on handwritten digit classification. **99% accuracy**. Then we train the same model on a new task — say, fashion item recognition. We go back and test it on digits. **34% accuracy**. It has completely forgotten. Not gradually, not partially — almost entirely.

![Drop in accuracy on MNIST dataset after training on Fashion MNIST dataset](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/5f3522b7-6033-418a-bfe7-db2aabb94d10.png align="center")

## What Just Happened?

We trained a CNN on MNIST digits — **99.2% accuracy**. After fine‑tuning on Fashion MNIST, it reached **91.1% accuracy**. But when re‑evaluated on MNIST, accuracy collapsed to **33.9%**. This collapse is **catastrophic forgetting**: the model’s weights shifted to optimize for the new task, erasing the old solution.

Why did training on more data make the model worse at something it already knew?

> MNIST is handwritten digits (0–9). Fashion MNIST is clothing items like shirts and shoes. Both are 28×28 grayscale images, but the tasks are distinct.

## Why Does It Happen?

The core issue is that the model relies on the same set of weights for both tasks. There is no separation or dedicated memory; **every parameter is shared**. When training shifts from Task A (*MNIST digits*) to Task B (*Fashion MNIST*), gradient descent simply minimizes the loss on the data it sees at that moment. It has no awareness that Task A ever existed.

![loss landscape of task A](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/32802068-140d-42cc-9fcf-01ceaf7757e3.png align="center")

![loss landscape of task B](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/23c736df-b37f-4886-b6e8-bcd3a8b39922.png align="center")

In the loss landscape, imagine two parabolic bowls: one for Task A and one for Task B. The optimum for Task A lies at \\(\theta^*_A\\)*,* while Task B's optimum is at \\(\theta^*_B\\). As training on Task B progresses, the weights \\(\theta\\) move towards \\(\theta^*_B\\). This movement inevitably raises the loss for Task A because its minimum is left behind.

![Image showing the loss surfaces for tasks A and B, and the weight update path followed by the model](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/be6b90ba-4595-4316-a508-cd5e1c804361.png align="center")

The root cause is the shared weight space. Gradient descent is a stateless optimizer; it only follows the current gradient signal. Since the minima for Task A and Task B are far apart, there is no single configuration of θ that satisfies both tasks simultaneously. This is why catastrophic forgetting occurs.

> Weight space can be visualized as an N-dimensional space, where each axis corresponds to one parameter. Every point in this space represents a full set of weights i.e., a complete model. The loss function defines a landscape over this space, and training is the process of moving through it along gradient directions.

## Why "Catastrophic"?

Human memory forgets **gradually** and **selectively**; you forget **less-used memories** slowly over time, and the forgetting is usually **partial**. Neural networks, by contrast, forget catastrophically — performance can collapse within just a few epochs, dropping from near‑perfect accuracy (e.g., 99%) to far lower levels (e.g., 34%) in a single training run. This forgetting is non‑selective: the entire task distribution degrades, not just edge cases.  
  
The underlying tension is the **stability–plasticity dilemma**. High plasticity allows fast learning of new tasks but destabilizes old ones, leading to catastrophic forgetting. Low plasticity preserves prior knowledge but prevents effective learning of new tasks. Continual learning research seeks to balance this trade‑off.

## How Do We Measure It?

The standard evaluation protocol in continual learning is simple but powerful. We train on Task 1 and record accuracy \\(R_{1,1}\\). Then we train on Task 2 and record accuracy on both tasks, \\(R_{2,1}\\) and \\(R_{2,1}\\). We continue for **N tasks**. This produces an accuracy matrix \\(R_{i,j}\\), where each entry is the **accuracy on task j after training on task i**.

From this matrix, we define **Backward Transfer (BWT)**:

$$BWT = \frac {1} {N−1} \Sigma_{j=1}^{N-1} (R_{N,j} - R_{j,j})$$

A negative BWT means catastrophic forgetting: performance on earlier tasks has degraded. In our demo, accuracy on Task A dropped from 99.2% to 33.9% after training Task B, giving a strongly negative BWT of **\-65.3%**.

![Screenshot of output of the calculation of backward transfer value for a training scenario of 2 tasks](https://cdn.hashnode.com/uploads/covers/628869289490454c4d8475de/ae4e4043-d481-40f7-950a-ff0ead845b4b.png align="center")

> There is also **Forward Transfer (FWT)**, which asks whether learning Task B helps Task A’s starting point. It is less central to catastrophic forgetting, but worth noting for completeness.

## Why Not Just Retrain?

The first instinct is obvious: why not just keep all the data and retrain the model from scratch every time new data arrives? It sounds simple but in practice, it’s impossible.

*   **Privacy and regulation**: In domains like medical imaging, GDPR, HIPAA and other privacy acts forbid indefinite storage. Once a patient’s scan is used, it may need to be deleted. You can’t just “keep everything.”
    
*   **Storage limits**: Modern datasets are massive. Retaining every sample forever is infeasible.
    
*   **Compute cost**: Retraining a large model from scratch each time is prohibitively expensive. Imagine re‑training GPT‑scale models weekly; the cost is humongous.
    
*   **Streaming data**: Some data exists only in a stream (sensor feeds, financial ticks) and is never stored. If you don’t learn it as it arrives, it’s gone.
    
*   **Real‑time systems**: In robotics, finance, or autonomous driving, models must adapt continuously without pausing for full retraining.
    

This is why continual learning exists as a distinct field: to make adaptation possible under these constraints. The open question is the one that drives the research forward: ***can we teach a network to learn new things without forgetting old ones, the way humans do?***

**Try it yourself**  
Curious to see catastrophic forgetting in action?

*   See [the demo on Colab](https://colab.research.google.com/github/SaptarshiSarkar12/continual-learning/blob/main/catastrophic_forgetting/notebook.ipynb)
    
*   Explore [the full code on GitHub](https://github.com/SaptarshiSarkar12/continual-learning)