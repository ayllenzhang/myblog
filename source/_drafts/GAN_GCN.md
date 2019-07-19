---
title: GAN, WGAN & GCN-GAN
date: 2019-07-08 15:00:46
tags: [GAN, GCN, Notes]
categories: 科研 / Research
mathjax: true
---

Here we introduce a novel model [GCN-GAN](https://arxiv.org/pdf/1901.09165.pdf). Before that, we would take a brief look at GAN & WGAN, which were the basic of GCN-GAN.

## GAN

GAN, namely generative adversarial network, is proposed by Ian Goodfellow in 2014. Different from other networks, GAN is about creating, or to be more specific, generate data from scratch.

Generally, GAN composes of two deep networks, the generator $\mathcal{G}$, and the discriminator $\mathcal{D}$. Suppose we sample some noise $\mathcal{z}$ using normal or uniform distribution.

- The generator $\mathcal{G}$ creates an image $x=\mathcal{G}(\mathcal{z})$
- The discriminator $\mathcal{D}$ distinguishes whether the input image to the discriminator is real or generated. Its output $\mathcal{D}(x)$ is the probability of $x$ being a real image.

In GAN, $\mathcal{D}$ and $\mathcal{G}$ play the following two-player minimax game with value function $V(\mathcal{G}, \mathcal{D})$:
$$
\min_{G}\max_{D}V(\mathcal{D},\mathcal{G})=\mathbb{E}_{x\sim p_{data}(x)}\log{\mathcal{D}(x)}+\mathbb{E}_{z\sim p_{z}(z)}\log{\left[1-\mathcal{D}(\mathcal{G}(z))\right]}
$$
On the discriminator side, our goal and loss function becomes
$$
\max_{D}V(\mathcal{D})=\underbrace{\mathbb{E}_{x\sim p_{data}(x)}\log{\mathcal{D}(x)}}_{Recog~real~images~better}+\underbrace{\mathbb{E}_{z\sim p_{z}(z)}\log{\left[1-\mathcal{D}(\mathcal{G}(z))\right]}}_{Recog~generated~images~better}
$$

$$
\begin{equation} \label{eq:1}
\mathcal{L}_\mathcal{D}=-\mathbb{E}_{x\sim P_r}\log{\mathcal{D}(x)}-\mathbb{E}_{x\sim P_g}\log{(1-\mathcal{D}(x))} \tag{1}
\end{equation}
$$

in which $P_r, P_g$ are the distributions of real images and generated images.

On the generator side, the objective function becomes
$$
\min_{G}V(\mathcal{G})=\underbrace{\mathbb{E}_{z\sim p_{z}(z)}\log{\left[1-\mathcal{D}(\mathcal{G}(z))\right]}}_{Optim~G~to~fool~the~discriminator~most}
$$
There are two ways to define the loss function of  $\mathcal{G}$, which are
$$
\begin{align}
\mathcal{L}_\mathcal{G}&=\mathbb{E}_{x\sim P_g}[log(1-\mathcal{D}(x))] \tag{2.1} \\
\mathcal{L}_\mathcal{G}&=\mathbb{E}_{x\sim P_g}[-log(\mathcal{D}(x))] \tag{2.2}
\end{align}
$$
Notice that here our goal is not the global minimum point, but the Nash equilibrium. According to the definition of Nash equilibrium, we can fix parameters of $\mathcal{G}$ to see the ideal discriminator $\mathcal{D}^*$ now.

For a sample $x$, it could be generated by $\mathcal{G}$ or from real dataset. Consider its contribution to $\eqref{eq:1}$, which is
$$
\begin{equation} \label{eq:3}
-P_r(x)\log{\mathcal{D}(x)}-P_g(x)\log{\left[1-\mathcal{D}(x)\right]} \tag{3}
\end{equation}
$$
Let the derivative of $\eqref{eq:3}$ with respect to $\mathcal{D}(x)$ to be zero,
$$
-\frac{P_r(x)}{\mathcal{D}(x)}+\frac{P_g(x)}{1-\mathcal{D}(x)}=0
$$
Therefore the ideal discriminator should be
$$
\mathcal{D}^*(x)=\frac{P_r(x)}{P_r(x)+P_g(x)}
$$
Suppose the generator $\mathcal{G}$ is an idealized generator, we should have $P_r(x)=P_g(x)$. In this case,
$$
\mathcal{D}^*(x)=0.5
$$

## WGAN
