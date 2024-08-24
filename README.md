[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/hee9joon/Awesome-Diffusion-Models) 
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Made With Love](https://img.shields.io/badge/Made%20With-Love-red.svg)](https://github.com/chetanraj/awesome-github-badges)

This repository contains a collection of resources and papers on ***guidance methods for diffusion models***.

**This repository is currently under maintenance.**

## Contents
<!-- - [Resources](#resources)
  - [Introductory Posts](#introductory-posts)
  - [Introductory Papers](#introductory-papers)
  - [Introductory Videos](#introductory-videos)
  - [Introductory Lectures](#introductory-lectures)
  - [Tutorial and Jupyter Notebook](#tutorial-and-jupyter-notebook) -->
- [Papers](#papers)
  - [Must-read Papers](#must-read-papers)
  - [Guidance Proposal Papers](#guidance-proposal-papers)
  - [Theoritical Interpretation](#theoritical-interpretation) 
  - [Application](#application)

# Resources
## Survey Papers
TODO

## Must-read Papers
**Diffusion Models Beat GANs on Image Synthesis** \
*Dhariwal, Prafulla, Nichol, Alex* \
[[Paper](https://arxiv.org/abs/2105.05233)]\
Proposes classifier guidance to sample from a sharper conditional distribution by optimizing the diversity-fidelity tradeoff of images.\
(이미지의 diversity-fidelity tradeoff로 더 sharp한 conditional 분포에서 샘플링하도록 가이드하는 classifier guidance를 제안)

**Classifier-Free Diffusion Guidance** \
*Jonathan Ho, Tim Salimans* \
[[Paper](https://arxiv.org/abs/2207.12598)] \
By expanding the conditional probability using Bayes' rule, achieves similar effects to classifier-guidance through the outer product of two scores.\
(conditional probability를 Bayes' rule로 전개해 두 스코어의 외분으로 classifier-guidance와 같은 효과를 얻음)

## Guidance Proposal Papers
### Gradient-based Guidance
**Universal Guidance for Diffusion Models** \
*Bansal, Arpit, Chu, Hong-Min, Schwarzschild, Avi, Sengupta, Soumyadip, Goldblum, Micah, Geiping, Jonas, Goldstein, Tom* \
[[Paper](https://arxiv.org/abs/2302.07121)] \
Guides image generation by minimizing the loss between predictions of various discriminative models (e.g., segmentation model, CLIP) and the condition, enabling targeted image generation (segmentation/detection/face recognition/style).\
(이미지 생성 시 다양한 discriminative 모델(segmentation model, CLIP 등)의 예측과 condition이 같아지도록 loss를 흘려줘서 특정 조건으로 이미지 생성하도록 가이드 (segmentation /detection / face recognition / style))

**Readout Guidance: Learning Control from Diffusion Features** \
*Luo, Grace, Darrell, Trevor, Wang, Oliver, Goldman, Dan B, Holynski, Aleksander* \
[[Paper](https://arxiv.org/abs/2312.02150)] \
Due to the high backpropagation cost of large models in universal guidance, learns a shallow network predicting intermediate features to provide guidance.\
(Universal guidance가 큰 모델을 사용해 backpropagation 비용이 크므로 중간 feature로 예측하는 shallow network 학습해 guidance 줌)

**Diffusion Self-Guidance for Controllable Image Generation** \
*Epstein, Dave, Jabri, Allan, Poole, Ben, Efros, Alexei A., Holynski, Aleksander* \
[[Paper](https://arxiv.org/abs/2306.00986)] \
Designs a loss that uses internal features of the diffusion denoising network for image editing.\
(디퓨전 denoising network 내부 피쳐를 이용한 loss를 설계해 이미지를 편집)

**Refining Generative Process with Discriminator Guidance in Score-based Diffusion Models** \
*Kim, Dongjun, Kim, Yeongmin, Kwon, Se Jung, Kang, Wanmo, Moon, Il-Chul* \
*2022/11/28* \
[[Paper](https://arxiv.org/abs/2211.17091)] \
Enhances sampling quality by learning a discriminator to provide loss guidance.\
(Discriminator를 학습하여 loss를 줌으로써 샘플링 퀄리티 향상)

**Self-Guided Generation of Minority Samples Using Diffusion Models** \
*Um, Soobin, Ye, Jong Chul* \
[[Paper](https://arxiv.org/abs/2407.11555)]\
Proposes minority guidance to sample more from regions with lower probability density.\
(더 확률 밀도가 낮은 곳에서 샘플링하는 Minority guidance 제안)

### Difference-based Guidance
**Improving Sample Quality of Diffusion Models Using Self-Attention Guidance** \
*Hong, Susung, Lee, Gyuseong, Jang, Wooseok, Kim, Seungryong* \
[[Paper](https://arxiv.org/abs/2210.00939)] \
Proposes self-attention guidance (SAG), which applies Gaussian blur to high-probability regions of the self-attention map, similar to the unconditional branch in CFG.\
(이미지에서 self-attention map의 high probability 부분에 가우시안 블러를 적용한 것을 CFG의 unconditional branch처럼 사용하는 self-attention guidance (SAG) 제안)

**Self-Rectifying Diffusion Sampling with Perturbed-Attention Guidance** \
*Ahn, Donghoon, Cho, Hyoungwon, Min, Jaewon, Jang, Wooseok, Kim, Jungwoo, Kim, SeonHwa, Park, Hyun Hee, Jin, Kyong Hwan, Kim, Seungryong* \
[[Paper](https://arxiv.org/abs/2403.17377)] \
Proposes perturbed-attention guidance (PAG) using perturbed self-attention maps as an unconditional branch, applied to inverse problems.\
(self-attention map을 perturb한 것을 unconditonal branch처럼 사용하는 perturbed-attention guidance (PAG)를 제안하고 inverse problem에 적용)

**Guiding a Diffusion Model with a Bad Version of Itself** \
*Karras, Tero, Aittala, Miika, Kynkäänniemi, Tuomas, Lehtinen, Jaakko, Aila, Timo, Laine, Samuli* \
[[Paper](https://arxiv.org/abs/2406.02507)] \
Argues that CFG works because the unconditional model predicts a more spread-out probability distribution (bad version) and samples from a sharper distribution when CFG is applied, proposing autoguidance using a small network, a less-trained network, or a model with different EMA length as the unconditional branch.\
(CFG가 작동하는 원리를 unconditional model이 bad version이기 때문에 더 부정확한 (퍼진) 확률 분포를 예측하고, CFG를 적용하면 이런 영역을 피하기 때문에 더 sharp한 분포에서 샘플링된다고 주장하고, small network, train을 더 적게 한 네트워크, EMA length를 다르게 한 모델 (bad version)을 unconditional branch처럼 사용하는 autoguidance 제안)

**Smoothed Energy Guidance: Guiding Diffusion Models with Reduced Energy Curvature of Attention** \
*Hong, Susung* \
[[Paper](https://arxiv.org/abs/2408.00760)] \
Proposes smoothed energy guidance (SEG) by applying blur to the self-attention map, explained from an energy landscape perspective.\
(self-attention map에 blur를 주는 smoothed energy guidance (SEG)를 제안하고, 이를 energy landscape 관점에서 설명)

**No Training, No Problem: Rethinking Classifier-Free Guidance for Diffusion Models**  \
*Sadat, Seyedmorteza, Kansy, Manuel, Hilliges, Otmar, Weber, Romann M.*  \
[[Paper](https://arxiv.org/abs/2407.02687)] \
Proposes independent condition guidance (ICG) by randomly applying conditions at each step, and time-step guidance (TCG) by perturbing the timestep embedding.\
(매 스텝 랜덤하게 condition 주는 independent condtion guidance (ICG), 타임스텝 임베딩에 perturbation 주는 time-step guidance (TCG) 제안)

### Improvement on CFG
**Inner Classifier-Free Guidance and Its Taylor Expansion for Diffusion Models**  \
*Shikun Sun, Longhui Wei, Zhicai Wang, Zixuan Wang, Junliang Xing, Jia Jia, Qi Tian*  \
[[Paper](https://openreview.net/forum?id=0QAzIMq32X)] \
Proposes that CFG is the first-order form of a more general type (ICFG) and presents a second-order CFG.\
(CFG가 일반적인 형태(ICFG)의 first-order form임을 제안하고, second-order CFG를 보임 (읽어봐야 함))

**CFG++: Manifold-constrained Classifier Free Guidance for Diffusion Models** \
*Chung, Hyungjin, Kim, Jeongsol, Park, Geon Yeong, Nam, Hyelin, Ye, Jong Chul* \
[[Paper](https://arxiv.org/abs/2406.08070)] \
Uses guided epsilon when moving toward $x_0$ in CFG and original epsilon when returning to $x_{t-1}$.\
(CFG에서 $x_0$로 갈 때는 guided epsilon을 사용하고 $x_{t-1}$ 돌아올 때는 original epsilon 사용)

## Theoritical Interpretation
**Classifier-Free Guidance is a Predictor-Corrector** \
*Bradley, Arwen, Nakkiran, Preetum* \
[[Paper](https://arxiv.org/abs/2408.09000)]

## Application
### Language Models
**Stay on topic with Classifier-Free Guidance** \
*Sanchez, Guillaume, Fan, Honglu, Spangher, Alexander, Levi, Elad, Ammanamanchi, Pawan Sasanka, Biderman, Stella*  \
[[Paper](https://arxiv.org/abs/2306.17806)]

<!-- ### Video Models -->


## Weight Schedule
**Analysis of Classifier-Free Guidance Weight Schedulers** \
*Wang, Xi, Dufour, Nicolas, Andreou, Nefeli, Cani, Marie-Paule, Abrevaya, Victoria Fernandez, Picard, David, Kalogeiton, Vicky*  \
[[Paper](https://arxiv.org/abs/2404.13040)]


---
# TODO
**Gradient Guidance for Diffusion Models: An Optimization Perspective** \
*Guo, Yingqing, Yuan, Hui, Yang, Yukang, Chen, Minshuo, Wang, Mengdi* \
[[Paper](https://arxiv.org/abs/2404.14743)]

**Understanding and Improving Training-free Loss-based Diffusion Guidance** \
*Shen, Yifei, Jiang, Xinyang, Wang, Yezhen, Yang, Yifan, Han, Dongqi, Li, Dongsheng* \
[[Paper](https://arxiv.org/abs/2403.12404)] 

**FreeEnhance: Tuning-Free Image Enhancement via Content-Consistent Noising-and-Denoising Process** \
Yang Luo, Yiheng Zhang, Zhaofan Qiu, Ting Yao, Zhineng Chen, Yu-Gang Jiang, Tao Mei \
[[Paper](https://openreview.net/forum?id=MJvG3qKu1v)]

**Theoretical Insights for Diffusion Guidance: A Case Study for Gaussian Mixture Models** \
*Wu, Yuchen, Chen, Minshuo, Li, Zihao, Wang, Mengdi, Wei, Yuting* \
*2024/03/03* \
[[Paper](https://arxiv.org/abs/2403.01639)]

**Training-Free Structured Diffusion Guidance for Compositional Text-to-Image Synthesis** \
*Feng, Weixi, He, Xuehai, Fu, Tsu-Jui, Jampani, Varun, Akula, Arjun, Narayana, Pradyumna, Basu, Sugato, Wang, Xin Eric, Wang, William Yang* \
*2022/12/09* \
[[Paper](https://arxiv.org/abs/2212.05032)]

**Rethinking the Spatial Inconsistency in Classifier-Free Diffusion Guidance** \
*Shen, Dazhong, Song, Guanglu, Xue, Zeyue, Wang, Fu-Yun, Liu, Yu* \
*2024/04/08* \
[[Paper](https://arxiv.org/abs/2404.05384)]

**Compress Guidance in Conditional Diffusion Sampling** \
*Dinh, Anh-Dung, Liu, Daochang, Xu, Chang* \
*2024/08/20* \
[[Paper](https://arxiv.org/abs/2408.11194)]

**Guidance with Spherical Gaussian Constraint for Conditional Diffusion** \
*Yang, Lingxiao, Ding, Shutong, Cai, Yifan, Yu, Jingyi, Wang, Jingya, Shi, Ye* \
*2024/02/05* \
[[Paper](https://arxiv.org/abs/2402.03201)]
