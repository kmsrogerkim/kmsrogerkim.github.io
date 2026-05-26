---
layout: single
title: "8 Essential Computer Vision Papers I Read: From VAE to DiT"
categories: AI
tag: [AI, CV]
use_math: true
---

## 8 Essential Computer Vision Papers I Read: From VAE to DiT

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

These papers are not isolated ideas. They build on each other. The story starts with autoencoders. VAE introduced a probabilistic version of autoencoders and, more importantly, the ELBO objective. Instead of compressing images into a fixed vector, VAE treated the latent space as a probability distribution. This idea became extremely important later for generative modeling.

Then DDPM introduced diffusion models. Instead of generating an image in one shot, DDPM gradually denoises random noise into an image. This ended up producing much better image quality than many older generative models.

At almost the same time, ViT adapted transformers to computer vision. Before ViT, CNNs dominated vision. ViT showed that transformers could work on images by splitting images into patches and treating them like tokens.

Then CLIP connected vision and language. CLIP learned image representations using natural language supervision instead of fixed class labels. This changed how people thought about representation learning in vision.

CFG improved diffusion models further. Classifier-Free Guidance made conditional generation much stronger and simpler. Prompt-following image generation became dramatically better because of this paper.

MAE pushed self-supervised learning for vision transformers. MAE masked image patches and reconstructed them, similar to masked language modeling in NLP. This made ViT training more scalable and data-efficient.

Then LDM combined many of these ideas together.

LDM used:
- VAE-style latent spaces
- diffusion models from DDPM
- transformer-era representations
- conditioning techniques like CFG

Instead of diffusing directly on pixels, it diffused inside a compressed latent space. This made high-quality image generation practical.

Finally, DiT pushed transformers directly into diffusion models.

Instead of using U-Nets, DiT used transformers as the backbone of diffusion models. This helped transformers become mainstream in modern generative vision systems.

## Core Ideas And How The Papers Connect

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
