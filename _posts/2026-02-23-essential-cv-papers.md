---
layout: single
title: "8 Essential Computer Vision Papers I Read as a CS Undergrad: From VAE to DiT"
categories: AI
tag: [AI, CV]
use_math: true
---

## 8 Essential Computer Vision Papers I Read as a CS Undergrad: From VAE to DiT

Here are 8 essential computer vision papers I read, in time order.

1. [Variational Autoencoder (VAE) (2013)](https://arxiv.org/abs/1312.6114)
2. [Denoising Diffusion Probabilistic Models (DDPM) (2020)](https://arxiv.org/abs/2006.11239)
3. [Vision Transformer (ViT) (2020)](https://arxiv.org/abs/2010.11929)
4. [Contrastive Language-Image Pretraining (CLIP) (2021)](https://arxiv.org/abs/2103.00020)
5. [Classifier-Free Guidance (CFG) (2021)](https://arxiv.org/abs/2207.12598)
6. [Masked Autoencoder (MAE) (2021)](https://arxiv.org/abs/2111.06377)
7. [Latent Diffusion Models (LDM) (2022)](https://arxiv.org/abs/2112.10752)
8. [Diffusion Transformer (DiT) (2022)](https://arxiv.org/abs/2212.09748)


## Introduction

Modern computer vision and generative modeling evolved through a sequence of connected breakthroughs. In 2013, the Variational Autoencoder (VAE) introduced probabilistic latent-variable modeling and the Evidence Lower Bound (ELBO), providing a practical framework for learning continuous latent representations. Instead of mapping an image into a fixed deterministic vector, VAE modeled the latent space as a distribution, which later became important for scalable generative models and latent-space compression.

For several years, generative models struggled with either unstable training, low sample quality, or limited diversity. In 2020, Denoising Diffusion Probabilistic Models (DDPM) changed the direction of the field by framing image generation as iterative denoising. Rather than generating an image in a single step, DDPM learned to reverse a Markov noising process and gradually recover data from Gaussian noise. Diffusion models produced significantly higher visual fidelity and more stable training behavior than many previous approaches, quickly becoming one of the dominant paradigms in image synthesis. However, diffusion models were computationally expensive because the generation process required many sequential denoising steps and operated directly in high-dimensional pixel space.

During the same period, Vision Transformer (ViT) introduced transformers into computer vision by treating image patches as token sequences. This reduced dependence on convolutional inductive bias and showed that transformer scaling behavior could extend beyond natural language processing. In 2021, Masked Autoencoders (MAE) further strengthened transformer-based vision learning through self-supervised masked reconstruction, allowing ViTs to learn efficient image representations from large-scale unlabeled data. Together, ViT and MAE established transformers as scalable backbone architectures for future generative vision systems.

Also in 2021, CLIP replaced closed-set classification objectives with contrastive image-text representation learning. Instead of predicting fixed labels, CLIP learned a shared embedding space between images and natural language, which later became critical for prompt-conditioned image generation systems. In the same year, Classifier-Free Guidance (CFG) solved another major limitation of diffusion models: weak conditional control. By combining conditional and unconditional diffusion predictions during sampling, CFG greatly improved prompt alignment without requiring an external classifier, making controllable text-to-image generation practical.

In 2022, Latent Diffusion Models (LDM) combined many of these developments into a single efficient framework. LDM used VAE-based latent compression to avoid diffusion in pixel space, reducing computational cost while preserving image quality. It used DDPM-style denoising as the generative mechanism and relied on CLIP-based text conditioning together with CFG-based sampling guidance for controllable generation. LDM demonstrated that high-resolution text-to-image synthesis could become both practical and scalable, and it became the foundation of systems such as Stable Diffusion.

Later in 2022, Diffusion Transformers (DiT) replaced the U-Net diffusion backbone with transformer architectures derived from the ViT lineage. DiT showed that transformers were not only effective for representation learning, but also highly scalable for diffusion-based image generation itself. This marked a broader transition toward transformer-native generative vision systems and influenced later work in image, video, and multimodal generation.

This blog post goes through the core ideas, mathematical formulations, and architectural contributions introduced by each paper, with a focus on how these works connect to each other historically and technically. Rather than treating these papers as isolated breakthroughs, the goal is to examine how concepts such as latent-variable modeling, diffusion-based generation, transformer architectures, self-supervised learning, and multimodal conditioning gradually built the foundation of modern computer vision and generative AI systems. Through this progression, the post introduces eight papers that significantly influenced my understanding of the field.

## Diving into Each Papers

### 1. Variational Autoencoder (VAE)

---

### Core idea

A VAE learns:
- an encoder: image -> latent distribution
- a decoder: latent -> reconstructed image

The important idea is that the latent representation is probabilistic. Instead of encoding an image into a single vector $z$, it learns $q(z|x)$

The training objective is the ELBO:

$$
\log p(x) \geq \mathbb{E}_{q(z|x)}[\log p(x|z)] - D_{KL}(q(z|x)\|p(z))
$$

This balances:
- reconstruction quality
- structured latent spaces

### Why it mattered later

LDM directly depends on this idea.

Stable Diffusion does not diffuse on raw pixels. It first compresses images into a latent space using an autoencoder-like model inspired by VAE ideas.

Without latent-space modeling, diffusion models would be far more expensive.

I cannot stretch enough the importance of this paper. If you would like to dig deeper, please try out this series of blog posts by Professor Yoo.
1. [초짜 대학원생의 입장에서 이해하는 Auto-Encoding Variational Bayes (VAE) (1)](https://jaejunyoo.blogspot.com/2017/04/auto-encoding-variational-bayes-vae-1.html?m=1)
2. [초짜 대학원생의 입장에서 이해하는 Auto-Encoding Variational Bayes (VAE) (2)](https://jaejunyoo.blogspot.com/2017/04/auto-encoding-variational-bayes-vae-2.html?m=1)

*_Yes they are written in Korean...not because I'm Korean but because this is the best blog post I could find that discusses about VAE in such great depth and detail._


### 2. Denoising Diffusion Probabilistic Models (DDPM)

---

### Core idea

DDPM gradually adds noise to images:

$$
x_0 \rightarrow x_1 \rightarrow x_2 \rightarrow ... \rightarrow x_T
$$

Then the model learns to reverse the process:

$$
x_T \rightarrow ... \rightarrow x_0
$$

Training becomes a denoising problem.

The key insight:
- generating images can be framed as iterative denoising

### Why it mattered later

This became the foundation of modern image generation.

LDM is fundamentally a latent-space diffusion model.

DiT is fundamentally a transformer-based diffusion model.

Without DDPM, neither paper exists.

### 3. Vision Transformer (ViT)

---

### Core idea

ViT splits an image into patches:

```text
image -> patches -> tokens -> transformer
```

This treats images similarly to sentences in NLP.

Before ViT:
- CNNs dominated computer vision

After ViT:
- transformers became central to vision

### Why it mattered later

MAE heavily depends on ViT.

DiT also depends on ViT-style transformer architectures.

Modern diffusion systems increasingly use transformer backbones instead of CNNs.

### 4. CLIP

---

### Core idea

CLIP learns image-text alignment.

Instead of predicting labels:

```text
image -> class
```

it learns:

```text
image <-> text similarity
```

using contrastive learning.

### Why it mattered later

CLIP enabled:
- text-conditioned image generation
- prompt understanding
- multimodal systems

Stable Diffusion uses CLIP text embeddings for prompting.

Without CLIP, prompt-based generation would be much weaker.

### 5. Classifier-Free Guidance (CFG)

---

### Core idea

CFG improves conditional diffusion generation.

The model learns both:
- conditional generation
- unconditional generation

Then combines them during sampling:

$$
\epsilon_\theta(x_t, c)
+
w(
\epsilon_\theta(x_t, c)
-
\epsilon_\theta(x_t)
)
$$

This improves prompt alignment without needing a separate classifier.

### Why it mattered later

CFG became a standard technique in diffusion models.

Stable Diffusion heavily relies on CFG for prompt-following behavior.

This paper made diffusion models much more controllable.

### 6. Masked Autoencoder (MAE)

---

### Core idea

MAE masks large portions of image patches and reconstructs them.

Very similar to masked language modeling in NLP.

Example:

```text
input image -> remove patches -> reconstruct missing patches
```

### Why it mattered later

MAE showed:
- self-supervised learning works extremely well for ViTs
- transformers can efficiently learn image structure

This strengthened the transformer ecosystem inside vision.

### 7. Latent Diffusion Models (LDM)

---

### Core idea

Diffusion on pixels is expensive.

LDM compresses images into latent representations first:

```text
image -> latent space -> diffusion -> decoder
```

This drastically reduces compute cost.

### Why it mattered

This paper enabled practical high-resolution diffusion systems like Stable Diffusion.

LDM combines ideas from:
- VAE
- DDPM
- CLIP
- CFG

It is basically a synthesis of multiple earlier breakthroughs.

### 8. Diffusion Transformer (DiT)

---

### Core idea

DiT replaces the U-Net backbone in diffusion models with transformers.

Instead of:

```text
diffusion + CNN/U-Net
```

DiT uses:

```text
diffusion + transformer
```

### Why it mattered

DiT showed transformers scale extremely well for generative vision.

This helped move the field toward:
- transformer-native diffusion systems
- scalable generative architectures
- unified multimodal models

## What's Next?

After DiT, the field is moving toward larger and more unified generative systems. Some of the major directions include: 

### 1. Multimodal models

Models are no longer only vision models. Modern systems combine:
- text
- images
- video
- audio
- actions

Examples:
- GPT-4o
- Gemini
- Sora-like systems

### 2. Video generation

Image generation is becoming video generation. The hard problem now is:
- temporal consistency
- motion understanding
- world simulation

Diffusion transformers are heavily used here.

### 3. Faster diffusion methods

Diffusion models are powerful but slow. A major research direction is reducing sampling steps:
- consistency models
- rectified flow
- flow matching
- distillation methods

### 4. Better world models

The field is moving beyond image quality. Current focus:
- reasoning
- physical consistency
- interaction
- long-horizon generation

This matters for:
- robotics
- agents
- simulation

## Final Thoughts

One thing I found interesting is that modern computer vision did not progress from a single breakthrough. It evolved by combining ideas such as:
- latent spaces from VAE
- denoising from DDPM
- transformers from ViT
- multimodal learning from CLIP
- controllable generation from CFG

LDM and DiT are products of this convergence. That is the biggest lesson from reading these papers.

## References  

1. Kingma, D. P., & Welling, M. (2013). **Auto-encoding variational bayes**. _arXiv preprint arXiv:1312.6114._
    [https://arxiv.org/abs/1312.6114](https://arxiv.org/abs/1312.6114)
2. Ho, J., Jain, A., & Abbeel, P. (2020). **Denoising diffusion probabilistic models**. _Advances in Neural Information Processing Systems, 33._
   [https://arxiv.org/abs/2006.11239](https://arxiv.org/abs/2006.11239)
3. Dosovitskiy, A., Beyer, L., Kolesnikov, A., Weissenborn, D., Zhai, X., Unterthiner, T., Dehghani, M., Minderer, M., Heigold, G., Gelly, S., Uszkoreit, J., & Houlsby, N. (2020). **An image is worth 16x16 words: Transformers for image recognition at scale**. _arXiv preprint arXiv:2010.11929._
   [https://arxiv.org/abs/2010.11929](https://arxiv.org/abs/2010.11929)
4. Radford, A., Kim, J. W., Hallacy, C., Ramesh, A., Goh, G., Agarwal, S., Sastry, G., Askell, A., Mishkin, P., Clark, J., Krueger, G., & Sutskever, I. (2021). **Learning transferable visual models from natural language supervision**. _Proceedings of the 38th International Conference on Machine Learning._
   [https://arxiv.org/abs/2103.00020](https://arxiv.org/abs/2103.00020)
5. Ho, J., & Salimans, T. (2021). **Classifier-free diffusion guidance**. _arXiv preprint arXiv:2207.12598._
   [https://arxiv.org/abs/2207.12598](https://arxiv.org/abs/2207.12598)
6. He, K., Chen, X., Xie, S., Li, Y., Dollár, P., & Girshick, R. (2021). **Masked autoencoders are scalable vision learners**. _Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)._
   [https://arxiv.org/abs/2111.06377](https://arxiv.org/abs/2111.06377)
7. Rombach, R., Blattmann, A., Lorenz, D., Esser, P., & Ommer, B. (2022). **High-resolution image synthesis with latent diffusion models**. _Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)._
   [https://arxiv.org/abs/2112.10752](https://arxiv.org/abs/2112.10752)
8. Peebles, W., & Xie, S. (2022). **Scalable diffusion models with transformers**. _Proceedings of the IEEE/CVF International Conference on Computer Vision (ICCV)._
   [https://arxiv.org/abs/2212.09748](https://arxiv.org/abs/2212.09748)

## Written by  
> **Roger Kim**  
> [![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white)](https://github.com/kmsrogerkim) [![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/kmsrogerkim/)  
