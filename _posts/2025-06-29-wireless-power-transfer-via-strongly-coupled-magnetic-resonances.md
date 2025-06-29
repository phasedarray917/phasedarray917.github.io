---
layout: post
title: Wireless Power Transfer(MIT)
categories: Research 
tags: [microwave engineering]
---

author: Kyle Lee

> Description:
>
> 這篇文章主要介紹 MIT 在2007年發表的關於 Strongly Coupled Magnetic Resonances 的無線充電技術，這篇文獻為後續的WPT(Wireless Power Transfer)領域奠定了強大的基礎。

<!-- more -->

# Research Objective

- Demonstrate efficient mid-range (up to 2 meters) non-radiative power transfer
- Utilize strongly coupled magnetic resonances (SCMR)
- Target efficiency: ~40% at 60 W output power

# Theory: Coupled-Mode Theory

Efficiency Equation:
$$
 \eta = \frac{k^2 Q_s Q_r}{(1 + k^2 Q_s Q_r)}
$$
where:

- $\eta$: efficiency
- $k$: coupling coefficient
- $Q_s$, $Q_r$: quality factors of source and receiver

- Optimal Efficiency is reached when:
  $$
  k^2 Q_s Q_r \gg 1
  $$
  → i.e., strong coupling and high Q-factors

# Resonator Design

| Parameter     | Value |
| ------------- | ----- |
| Radius $r$      | 30 cm |
| Height $h$      | 20 cm |
| Turns $n$       | 5.25  |
| Wire radius $a$ | 3 mm  |

# Experimental Setup

- 使用 Colpitts oscillator 驅動 source coil (S)，透過 單匝激發圈 (A) 耦合
- Device coil (D) 接收能量，經由感應耦合至負載圈 (B)，點亮燈泡
- 透過旋轉 D 與 A，使其 互感為 0（即 M = 0），避免直接磁耦合干擾
- 這樣可確保能量傳輸是透過共振而非直接耦合

## Mutual Inductance and Coupling

- Mutual Inductance $M$：由功率傳輸狀況估算
- Coupling Coefficient $k$ 與 Quality Factor $Q$ 的乘積為關鍵參數

# Experimental Results

| Specification  | Results                            |
| -------------- | ---------------------------------- |
| 最大傳輸距離   | 2.4 m                              |
| 傳輸效率       | ~40% at 60 W                       |
| Coupling 條件  | $\frac{k}{G} > 1$ at all distances |
| 理論與實驗誤差 | 小於 5%                            |

# Conclusion

- Strongly coupled magnetic resonance enables efficient, practical mid-range wireless power
- 與耦合模態理論相符，誤差極小

## Future Improvements

- 提升 Q 值：如使用 銀鍍線圈
- 縮小接收端線圈尺寸
- 引入 自適應調諧控制（Adaptive tuning with feedback）

# References
1. [André Kurs et al., Wireless Power Transfer via Strongly Coupled Magnetic Resonances, Science, 317, 83–86 (2007).](https://doi.org/10.1126/science.1143254)

