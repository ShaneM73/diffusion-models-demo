# Diffusion Models Lab

**▶ Live demo: https://shanem73.github.io/diffusion-models-demo/**
 · [简体中文版](https://shanem73.github.io/diffusion-models-demo/?lang=zh)

An interactive, single-page guide to how diffusion models (the family behind Stable Diffusion, DALL·E 3 and Sora) turn random noise into images. Everything runs in the browser: no server, no build step, no model download.

English is the default. Use the **English / 简体中文** switch in the top-right corner of the page, or open the page with `?lang=zh`.

## What's inside

1. **3D demo.** A rolled-up sheet in 3D space stands in for the "manifold" where real images live. You can watch points get scattered by noise (forward process), then generate new points that are pulled back onto the sheet from pure noise (reverse process). Toggle arrows to see the denoising direction (the score) at every point.
2. **The math.** The closed-form noising formula $x_t = \sqrt{\bar\alpha_t}\,x_0 + \sqrt{1-\bar\alpha_t}\,\varepsilon$ with a live mixer and coefficient chart, the noise-prediction training objective $\mathcal{L}(\theta)=\mathbb{E}\,\lVert \varepsilon-\varepsilon_\theta(x_t,t,c)\rVert^2$, why it is correct (the ELBO and Tweedie's formula), DDPM/DDIM sampling, and classifier-free guidance.
3. **The architecture.** Clickable diagrams of a U-Net (Stable Diffusion 1.x/2.x/XL) and a Diffusion Transformer (DiT, as in SD3 and Sora), with an explanation of every block.
4. **A worked example.** Pick a text prompt and watch a $48 \times 48$ image emerge over $50$ DDIM steps. For each step it shows the current noisy image, the predicted noise (what the network actually outputs) and the predicted clean image. You can change the guidance strength $w$ and the random seed.

> The "network" in the examples is an ideal denoiser that computes the optimal answer exactly against a small built-in dataset ($40$ procedurally drawn images, $10$ per prompt). The sampling process is exactly what a real model does, but the results can only land near images in that dataset. A trained model has to learn this answer with hundreds of millions of parameters, which is what lets it produce genuinely new images.

## Run it locally

It is a single static file. All formulas are written in LaTeX and typeset in the browser with [KaTeX](https://katex.org/). Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

It loads [three.js](https://threejs.org/) r128, KaTeX 0.16.9 and Google Fonts from public CDNs, so it needs an internet connection the first time.

## References

- Ho, Jain & Abbeel (2020). *Denoising Diffusion Probabilistic Models* (DDPM).
- Song, Meng & Ermon (2021). *Denoising Diffusion Implicit Models* (DDIM).
- Song et al. (2021). *Score-Based Generative Modeling through Stochastic Differential Equations*.
- Rombach et al. (2022). *High-Resolution Image Synthesis with Latent Diffusion Models*.
- Ho & Salimans (2022). *Classifier-Free Diffusion Guidance*.
- Peebles & Xie (2023). *Scalable Diffusion Models with Transformers* (DiT).

---

## 简介（简体中文）

**▶ 在线演示：https://shanem73.github.io/diffusion-models-demo/?lang=zh**

这是一个交互式单页网页，讲解扩散模型（Stable Diffusion、DALL·E 3、Sora 背后的技术）是怎么把随机噪声变成图片的。全部在浏览器里运行，不需要服务器，也不需要下载模型。页面默认英文，右上角可以切换到简体中文。

页面包括四部分：

1. **三维演示**：用三维空间里一张卷起来的“纸”代表真实图片所在的流形。可以看点被噪声打散（正向加噪），也可以从纯噪声出发把点拉回纸面（反向生成），还能显示每个点的去噪方向。
2. **数学原理**：加噪公式 $x_t = \sqrt{\bar\alpha_t}\,x_0 + \sqrt{1-\bar\alpha_t}\,\varepsilon$（带实时混合演示和系数曲线）、预测噪声的训练目标、为什么这个目标是对的（ELBO 和 Tweedie 公式）、DDPM/DDIM 采样和无分类器引导。
3. **模型结构**：U-Net 和 DiT 的可点击结构图，每个模块都有说明。
4. **生成例子**：选一句描述，看一张图在 $50$ 步里从噪声中浮现，同时显示当前图、网络预测的噪声和猜测的原图。可以调引导强度 $w$ 和随机起点。

> 例子里的“网络”是理想去噪器，直接对照一个 40 张小图的内置数据集算出最优答案。采样过程和真实模型完全一样，但结果只会落在数据集的图附近。真实模型要靠几亿参数把这个答案学出来，才能画出全新的图。

## License

[MIT](LICENSE) © 2026 Xin (Shane) Miao
