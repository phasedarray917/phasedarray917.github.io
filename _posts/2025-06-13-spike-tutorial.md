---
layout: post
title: Spike Hound 儀器操作教學
categories: Research 
tags: [microwave engineering]
---

author: Kyle Lee

> Description:
>
> 這篇文章主要講述如何使用Spike Software 並配合 TG124A 與 SA124來進行Passive Circuit Insertion Loss 與 Return Loss 的量測。
>
> 同時也會提供將匯出數據用MATLAB進行繪製的程式

<!-- more -->

# Insertion Loss Measurement 

1. 將TG sync 連結至 SA Output sync
2. 將 TG out 跟 SA in 用線材連接
3. 跑完sweep後切到scalar network analysis 
4. 跑完sweep後按下 store thru 完成calibration (每次量測前與更換線材後都要記得calibration)
5. 線材可能不支援高頻
6. 待測電路的兩端要有線材連接到儀器(不要直接接在儀器的端口)

![png](/public/img/spike_tutorial/1.jpeg)

# Return Loss Measurement

1. 將 TG out 接到 directional coupler OUT
2. 將 SA in 接到 directional coupler CPL
3. 將 directional coupler In 保持開路
4. 進行calibration (按下 store Thru)
5. 將待測電路連接到 directional coupler In

![png](/public/img/spike_tutorial/2.jpeg)

# Save Data
在旁邊的 trace 欄位可以看到 export data

```matlab
data = readmatrix('data.csv');

frequency_GHz = data(:, 1) / 1e9;

insertion_loss_dB = data(:, 2);

figure;
plot(frequency_GHz, insertion_loss_dB, 'b-', 'LineWidth', 1.5);
grid on;

title('Insertion Loss vs Frequency');
xlabel('Frequency (GHz)');
ylabel('Insertion Loss (dB)');

xlim([0.1, 13]);
ylim([min(insertion_loss_dB)-1, max(insertion_loss_dB)+1]);
```

![png](/public/img/spike_tutorial/3.png)
