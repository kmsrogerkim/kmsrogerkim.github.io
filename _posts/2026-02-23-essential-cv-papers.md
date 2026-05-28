---
layout: single
title: "8 Essential Computer Vision Papers I Read as a CS Undergrad: From VAE to DiT"
categories: AI
tag: [AI, CV]
use_math: true
---

Here are 8 essential computer vision papers I read that forms the foundation of modern computer vision / generative models; in chronological order.

1. [Variational Autoencoder (VAE) (2013)](https://arxiv.org/abs/1312.6114)
2. [Denoising Diffusion Probabilistic Models (DDPM) (2020)](https://arxiv.org/abs/2006.11239)
3. [Vision Transformer (ViT) (2020)](https://arxiv.org/abs/2010.11929)
4. [Contrastive Language-Image Pretraining (CLIP) (2021)](https://arxiv.org/abs/2103.00020)
5. [Classifier-Free Guidance (CFG) (2021)](https://arxiv.org/abs/2207.12598)
6. [Masked Autoencoder (MAE) (2021)](https://arxiv.org/abs/2111.06377)
7. [Latent Diffusion Models (LDM) (2022)](https://arxiv.org/abs/2112.10752)
8. [Diffusion Transformer (DiT) (2022)](https://arxiv.org/abs/2212.09748)

Modern computer vision and generative modeling evolved through a sequence of connected breakthroughs. In 2013, the Variational Autoencoder (VAE) introduced probabilistic latent-variable modeling and the Evidence Lower Bound (ELBO), providing a practical framework for learning continuous latent representations. Instead of mapping an image into a fixed deterministic vector, VAE modeled the latent space as a distribution, which later became important for scalable generative models and latent-space compression.

For several years, generative models struggled with either unstable training, low sample quality, or limited diversity. In 2020, Denoising Diffusion Probabilistic Models (DDPM) changed the direction of the field by framing image generation as iterative denoising. Rather than generating an image in a single step, DDPM learned to reverse a Markov noising process and gradually recover data from Gaussian noise. Diffusion models produced significantly higher visual fidelity and more stable training behavior than many previous approaches, quickly becoming one of the dominant paradigms in image synthesis. However, diffusion models were computationally expensive because the generation process required many sequential denoising steps and operated directly in high-dimensional pixel space.

During the same period, Vision Transformer (ViT) introduced transformers into computer vision by treating image patches as token sequences. This reduced dependence on convolutional inductive bias and showed that transformer scaling behavior could extend beyond natural language processing. In 2021, Masked Autoencoders (MAE) further strengthened transformer-based vision learning through self-supervised masked reconstruction, allowing ViTs to learn efficient image representations from large-scale unlabeled data. Together, ViT and MAE established transformers as scalable backbone architectures for future generative vision systems.

Also in 2021, CLIP replaced closed-set classification objectives with contrastive image-text representation learning. Instead of predicting fixed labels, CLIP learned a shared embedding space between images and natural language, which later became critical for prompt-conditioned image generation systems. In the same year, Classifier-Free Guidance (CFG) solved another major limitation of diffusion models: weak conditional control. By combining conditional and unconditional diffusion predictions during sampling, CFG greatly improved prompt alignment without requiring an external classifier, making controllable text-to-image generation practical.

In 2022, Latent Diffusion Models (LDM) combined many of these developments into a single efficient framework. LDM used VAE-based latent compression to avoid diffusion in pixel space, reducing computational cost while preserving image quality. It used DDPM-style denoising as the generative mechanism and relied on CLIP-based text conditioning together with CFG-based sampling guidance for controllable generation. LDM demonstrated that high-resolution text-to-image synthesis could become both practical and scalable, and it became the foundation of systems such as Stable Diffusion.

Later in 2022, Diffusion Transformers (DiT) replaced the U-Net diffusion backbone with transformer architectures derived from the ViT lineage. DiT showed that transformers were not only effective for representation learning, but also highly scalable for diffusion-based image generation itself. This marked a broader transition toward transformer-native generative vision systems and influenced later work in image, video, and multimodal generation.

This blog post goes through the core ideas, mathematical formulations, and architectural contributions introduced by each paper, with a focus on how these works connect to each other historically and technically. Rather than treating these papers as isolated breakthroughs, the goal is to examine how concepts such as latent-variable modeling, diffusion-based generation, transformer architectures, self-supervised learning, and multimodal conditioning gradually built the foundation of modern computer vision and generative AI systems. Through this progression, the post introduces eight papers that significantly influenced my understanding of the field.

## 1. Variational Autoencoder (VAE)

A VAE learns:
- an encoder: image -> latent distribution
- a decoder: latent -> reconstructed image

Instead of encoding an image into a single deterministic vector $z$, VAE models the latent representation as a probability distribution:

$$
q_\phi(z|x) \approx p(z|x)
$$

The true posterior:

$$
p(z|x) = \frac{p(x|z)p(z)}{p(x)}
$$

is usually intractable because computing the following is extrememly expensive:

$$
p(x) = \int p(x|z)p(z)dz
$$

VAE solves this through variational inference by optimizing the Evidence Lower Bound (ELBO):

$$
\log p(x) \geq \mathbb{E}_{q(z|x)}[\log p(x|z)] - D_{KL}(q(z|x)\|p(z))
$$

This objective balances:
- reconstruction quality
- structured latent representations

One of the paper's most important contributions is the reparameterization trick. Instead of directly sampling $ z \sim \mathcal{N}(\mu, \sigma^2) $, VAE rewrites the sampling process as:

$$
z = \mu + \sigma \odot \epsilon
\quad
\text{where}
\quad
\epsilon \sim \mathcal{N}(0, I)
$$

This allows gradients to flow through stochastic sampling during backpropagation.

### Core contribution

VAE introduced:
- variational inference for deep generative models
- continuous latent-variable modeling
- the reparameterization trick for differentiable sampling

It established the idea that generation can happen inside a structured latent space rather than directly in pixel space. I cannot stretch enough the importance of this paper. It is really, **REALLY** important that you understnad the **ELBO** introduced in this paper. If you would like to dig deeper, please try out this series of blog posts by Professor Yoo.

1. [초짜 대학원생의 입장에서 이해하는 Auto-Encoding Variational Bayes (VAE) (1)](https://jaejunyoo.blogspot.com/2017/04/auto-encoding-variational-bayes-vae-1.html?m=1)
2. [초짜 대학원생의 입장에서 이해하는 Auto-Encoding Variational Bayes (VAE) (2)](https://jaejunyoo.blogspot.com/2017/04/auto-encoding-variational-bayes-vae-2.html?m=1)

*_They are written in Korean... but this is the best blog post I could find discussing VAE in such depth and detail._*

## 2. Denoising Diffusion Probabilistic Models (DDPM)
DDPM formulates image generation as iterative denoising. The forward process gradually corrupts data with Gaussian noise:

$$
q(x_t|x_{t-1}) =
\mathcal{N}
(
x_t;
\sqrt{1-\beta_t}x_{t-1},
\beta_t I
)
$$

After many timesteps:

$$
x_T \sim \mathcal{N}(0, I)
$$

The model then learns the reverse process:

$$
p_\theta(x_{t-1}|x_t)
$$

which progressively removes noise and reconstructs the data distribution.


<p align="center">
  <img src="/assets/img/ddpm.png" width="90%">
</p>

Instead of directly predicting images, DDPM predicts the noise added at each timestep:

$$
L_{simple} = \mathbb{E}_{x_0,\epsilon,t} \left[\|\epsilon -\epsilon_\theta(x_t, t)\|^2\right]
$$

To dive deeper, please refer to [my blog post about DDPM!](https://kmsrogerkim.github.io/ai/ddpm/)

### Core contribution

DDPM introduced:
- diffusion-based generative modeling
- iterative denoising as a generation process
- stable likelihood-based training for image synthesis

Before diffusion models, GANs dominated image generation but suffered from:
- unstable adversarial optimization
- mode collapse
- limited sample diversity

DDPM replaced adversarial training with a denoising objective and achieved significantly more stable optimization and higher sample quality. Basically, they established the diffusion framework, which is now the standard for generative models. This paper led to:
- CFG for controllable generation
- LDM for latent-space diffusion
- DiT for transformer-based diffusion backbones

## 3. Vision Transformer (ViT)

Before ViT, CNNs dominated computer vision because images were assumed to require convolutional inductive biases such as locality and translation equivariance. ViT challenged this assumption by treating images as token sequences.

<p align="center">
  <img src="/assets/img/vit/vit_architecture.png" width="100%">
</p>

Given an image $ x \in \mathbb{R}^{H \times W \times C} $, ViT splits the image into fixed-size patches:

```text
image -> patches -> tokens -> transformer
```

Each flattened patch is projected into a token embedding $ z_0 = [x_p^1E; x_p^2E; ...; x_p^NE] $. The transformer encoder then processes these patch tokens similarly to words in NLP.

### Core contribution

The key result was that transformer scaling laws also apply to vision when trained on sufficiently large datasets. This paper fundamentally changed vision architectures.

ViT became the architectural foundation for:
- MAE self-supervised learning
- transformer-based diffusion models like DiT
- modern multimodal systems

Transformers later became central not only for representation learning, but also for image generation itself.

## 4. CLIP

<p align="center">
  <img src="/assets/img/vit/clip_architecture.png" width="100%">
</p>

CLIP learns aligned image and text representations through contrastive learning. Instead of predicting fixed class labels, CLIP learns aligned image-text embeddings with a contrastive loss:

$$
L_{\text{CLIP}}
=
-\frac1N
\sum_i
\log
\frac{
\exp(\text{sim}(f(x_i),g(t_i))/\tau)
}{
\sum_j
\exp(\text{sim}(f(x_i),g(t_j))/\tau)
}
$$

Instead of class labels $y\in\{1,\ldots,K\}$, CLIP produces a semantic conditioning vector

$$
c=g(\text{prompt})
$$

which later becomes the text condition used in diffusion.

### Core contribution

The important shift was replacing fixed-label supervision with natural language supervision at internet scale.

CLIP enabled:
- text-conditioned image generation
- prompt understanding
- multimodal systems

Later text-to-image systems used CLIP embeddings to condition diffusion models on natural language prompts. Without CLIP, prompt-based generation would have been significantly weaker.

## 5. Classifier-Free Guidance (CFG)

### Background: From ELBO To Diffusion Objectives

To understand why CFG mattered, it is important to trace the evolution of diffusion training objectives back to VAE.

VAE introduced the Evidence Lower Bound (ELBO):

$$
\log p(x) \geq
\mathbb{E}_{q(z|x)}[\log p(x|z)]

D_{KL}(q(z|x)|p(z))
$$

This objective turned probabilistic latent-variable modeling into a tractable optimization problem.

Instead of directly maximizing:

$$
\log p(x)
$$

which is often intractable, VAE optimized a lower bound of the data likelihood. This became one of the most important ideas in deep generative modeling. Later diffusion models inherited this probabilistic viewpoint.DDPM also derives from a variational objective and optimizes a form of ELBO over the entire diffusion trajectory:

$$
L_{VLB}

\mathbb{E}_q
\left[

\log p_\theta(x_0)
+
\sum_{t=1}^{T}
D_{KL}
\left(
q(x_{t-1}|x_t,x_0)
|
p_\theta(x_{t-1}|x_t)
\right)
\right]
$$

This connects VAE and diffusion models more closely than they first appear.

Both frameworks:

* define probabilistic latent variables
* optimize variational bounds
* learn generative processes through tractable approximations

However, DDPM later simplified this objective into a practical denoising loss:

$$
L_{simple}
\mathbb{E}_{x_0,\epsilon,t}
\left[
|
\epsilon

\epsilon_\theta(x_t,t)
|^2
\right]
$$

This simplification made diffusion models significantly easier and more stable to train.

---

### Core idea

Early conditional diffusion systems relied on separately trained classifiers to guide generation toward desired conditions.

The idea was to modify the reverse diffusion process using classifier gradients:

$$
\nabla_{x_t} \log p(c|x_t)
$$

where:

* $x_t$ is the noisy image at timestep $t$
* $c$ is the conditioning input

The guided sampling process became:

$$
\hat{\epsilon}_\theta(x_t,c) = \epsilon_\theta(x_t) s \sigma_t \nabla_{x_t} \log p(c|x_t)
$$

However, this approach had several problems:

* an additional classifier had to be trained
* classifier gradients became unstable at high noise levels
* training and inference complexity increased

CFG removed the need for external classifiers entirely.

Instead, the diffusion model jointly learned:

* conditional generation
* unconditional generation

During training, conditions are randomly dropped:

$$
p(c = \varnothing)

p_{drop}
$$

This allows the same model to learn both:

$$
\epsilon_\theta(x_t,c)
$$

and:

$$
\epsilon_\theta(x_t)
$$

The final guided prediction becomes:

$$
\hat{\epsilon}_\theta

\epsilon_\theta(x_t)
+
w
(
\epsilon_\theta(x_t,c)

\epsilon_\theta(x_t)
)
$$

where:

* $w$ controls guidance strength
* larger $w$ increases prompt adherence
* $w=0$ becomes unconditional generation
* larger $w$ trades diversity for stronger conditioning

The key intuition is that:

$$
\epsilon_\theta(x_t,c)

\epsilon_\theta(x_t)
$$

isolates the conditional signal introduced by the prompt.

CFG then amplifies this signal during sampling.

---

### Core contribution

CFG introduced:

* classifier-free conditional guidance
* controllable prompt-conditioned sampling
* stronger conditioning without external classifiers

More importantly, CFG made diffusion models practically controllable.

Earlier diffusion systems could generate high-quality images, but prompt alignment was often weak or unstable.

CFG solved this problem with a surprisingly simple modification to sampling.

This paper became one of the most important practical improvements in diffusion models.

## 6. Masked Autoencoder (MAE)

MAE performs self-supervised learning through masked image reconstruction. Large portions of image patches, often around 75%, are removed.

<p align="center">
  <img src="/assets/img/vit/mae.png" width="100%">
</p>

Unlike earlier reconstruction methods, MAE uses:
- a heavy encoder for visible patches
- a lightweight decoder for reconstruction

This makes training significantly more efficient.

### Core contribution

MAE introduced:
- scalable self-supervised learning for ViTs
- high-ratio masked reconstruction for images
- efficient transformer pretraining for vision

The paper demonstrated that transformer-based vision models can learn strong image representations from unlabeled data alone. MAE strengthened the ViT ecosystem and accelerated transformer adoption in vision. This indirectly helped transformer-based generative systems like DiT become practical and scalable.

## 7. Latent Diffusion Models (LDM)

<p align="center">
  <img src="/assets/img/LDM.png" width="100%">
</p>

LDM compresses images with an autoencoder:

$$
z=\mathcal{E}(x)
$$

and diffuses in latent space rather than pixel space. The diffusion loss remains structurally the same as DDPM:

$$
L_{\text{LDM}}
=
\mathbb{E}
\left[
\|\epsilon-\epsilon_\theta(z_t,t,c)\|^2
\right]
$$

compared with

$$
L_{\text{DDPM}}
=
\mathbb{E}
\left[
\|\epsilon-\epsilon_\theta(x_t,t)\|^2
\right]
$$

The main change is

$$
x_t\rightarrow z_t
$$

so the model works in a lower-dimensional manifold. Conditioning enters through text embeddings

$$
c=f_{\text{text}}(\text{prompt})
$$

and CFG strengthens sampling:

$$
\hat\epsilon_\theta
=
\epsilon_\theta(z_t,t)
+
w\Big(\epsilon_\theta(z_t,t,c)-\epsilon_\theta(z_t,t)\Big)
$$

LDM is therefore a composition of

$$
\text{VAE}+\text{DDPM}+\text{CLIP}+\text{CFG}
$$

### Core contribution

LDM introduced:
- latent-space diffusion
- practical high-resolution diffusion generation
- efficient large-scale text-to-image synthesis

This paper combined several earlier breakthroughs into a single practical system:
- VAE-style latent compression
- DDPM-style denoising diffusion
- CLIP-based text conditioning
- CFG-based controllable sampling

This is where many earlier research ideas became a usable real-world generative system.

### Why it mattered later

LDM became the foundation of systems such as Stable Diffusion.

It demonstrated that high-quality text-to-image generation could become practical on consumer hardware rather than requiring extremely expensive compute.

## 8. Diffusion Transformer (DiT)

<p align="center">
  <img src="/assets/img/dit_architecture.png" width="100%">
</p>

Earlier diffusion systems mainly used convolutional U-Nets as denoising backbones. DiT replaced this architecture with transformers operating directly on latent patches. DiT replaces the U-Net denoiser with a transformer over latent patches:

$$
z\rightarrow\{z_p^1,\ldots,z_p^N\}
$$

with the same attention rule used in ViT:

$$
\text{Attention}(Q,K,V)
=
\text{softmax}\!\left(\frac{QK^T}{\sqrt d}\right)V
$$

The diffusion loss is unchanged in form:

$$
L_{\text{DiT}}
=
\mathbb{E}
\left[
\|\epsilon-\epsilon_\theta(z_t,t,c)\|^2
\right]
$$

The architectural change is

$$
\text{U-Net}\rightarrow\text{Transformer}
$$

so DiT keeps the diffusion objective while swapping in a transformer backbone.

### Core contribution

DiT introduced:
- transformer-native diffusion architectures
- scalable transformer backbones for image generation
- diffusion scaling laws for transformers

The key result was that diffusion performance scaled predictably with:
- model size
- training compute
- dataset scale

### Why it mattered later

DiT accelerated the transition toward transformer-native generative systems.

This influenced later work in:
- video generation
- multimodal generation
- world models
- large-scale generative architecture

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

What makes these papers particularly important is not only their individual contributions, but also how naturally they compose into a unified generative framework. VAE introduced latent-variable inference and variational optimization. DDPM reformulated generation as iterative denoising through probabilistic diffusion. ViT and MAE established transformers as scalable visual architectures, while CLIP transformed natural language into a usable conditioning interface. CFG then made diffusion models practically controllable, and LDM combined these ideas into an efficient latent-space generative system. Finally, DiT demonstrated that transformer scaling behavior extends directly into diffusion-based image generation itself.

Viewed historically, modern generative AI did not emerge from a single breakthrough, but from the gradual convergence of probabilistic modeling, diffusion processes, representation learning, multimodal conditioning, and transformer scaling. Many modern systems still inherit the same mathematical structure introduced across these papers: variational objectives, denoising losses, latent representations, attention mechanisms, and conditional guidance. Understanding how these ideas connect provides a much clearer picture of why current generative models work, how they evolved, and where future architectures may continue to develop.


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
