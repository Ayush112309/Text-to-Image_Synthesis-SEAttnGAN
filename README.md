# Text-to-Image-Synthesis-SEAttnGAN
Exploring improvements to **SEA-AttnGAN** for text-to-image synthesis using **InfoNCE**, **WGAN-GP**, and **CLIP** on the **CUB-200 dataset**.

---

## Introduction
Text-to-image synthesis is an exciting direction in Generative AI, enabling realistic images from textual descriptions.  
In this project, we experiment with **SEA Attention GAN (SEAttnGAN)** on the **CUB-200 bird dataset** and propose improvements using:

- **Contrastive InfoNCE loss** → better text–image alignment  
- **WGAN-GP with a ResNet discriminator** → more stable training  
- **CLIP text encoder** → richer semantic embeddings  

We analyze performance using **Fréchet Inception Distance (FID)** and showcase **qualitative results**.

---

## Literature Review 

- **Latent Diffusion Models (LDMs)** → efficient high-resolution synthesis via latent space.  
- **DF-GAN** → one-stage generator with MA-GP discriminator.  
- **SEAttnGAN** → simplified, parameter-efficient AttnGAN.  
- **unCLIP** → diffusion + CLIP embeddings for diversity and editing.  

---

## Model Architecture

- **Dataset**: CUB-200 (200 bird species, 11,788 images, each with 10 captions)  
- **Text Encoder**: BiLSTM (baseline), CLIP (experiment)  
- **SEA Attention Block**:  
  - Word-level attention (aligns words with visual features)  
  - Sentence-level affine modulation (scales & shifts features)  
- **Generator**: Progressive upsampling → 256×256 images  
- **Discriminator**: CNN + residual layers + text fusion  
- **Losses**:  
  - Hinge adversarial loss (baseline)  
  - Matching-Aware Loss  
  - InfoNCE contrastive loss  
  - WGAN-GP loss with gradient penalty  
---

## Experiments

### 🔹 Experiment 1: Baseline
- Loss: Adversarial + Matching-Aware  
- Epochs: 500  
- Training Time: 70h (T4 GPU)  

### 🔹 Experiment 2: +InfoNCE Loss *Best*
- Added contrastive InfoNCE loss (λ = 0.1)  
- Epochs: 500  
- Training Time: 70h  
- **Best results (lowest FID)**  

### 🔹 Experiment 3: ResNet Discriminator + WGAN-GP
- Pretrained ResNet-18 backbone  
- Generator exploited discriminator → required balancing updates  
- Epochs: 200  
- Training Time: 40h  

### 🔹 Experiment 4: CLIP Encoder
- CLIP (ViT-B/32) + adapter  
- Epochs: 389  
- Training Time: 53h  

---

## Results

### Quantitative (FID Scores)
| Model Variant          | Best FID ↓ |
|-------------------------|------------|
| Baseline               | **139.79** |
| +InfoNCE Loss          | **118.76** |
| ResNet-WGAN-GP         | ~217       |
| CLIP Encoder           | ~239       |

## Authors
- Jhori Ayush Prakash Satish (ch23btech11022@iith.ac.in)  
*(IIT Hyderabad)* 
