---
layout: post
title: Xschem 操作教學 
categories: Research 
tags: [microwave engineering]
---

author: Kyle Lee

> Description:
>
> 這篇文章主要講述如何使用Xschem進行電路操作與模擬，並且會提供Skywater130nm 製成下，Inverter的設計與模擬教學

<!-- more -->

# Before We Start

- 請先確認 Xschem 與 sky130 製程都已安裝完成
- 請先自行設定存放 Project 的資料夾
- 在 Project 的資料夾使用 mkdir 建立名為 test_inv 的資料夾

# sky130 Integration

進入 test_inv 資料夾，並輸入以下指令來進行設定

```sh
echo 'source /usr/local/share/pdk/sky130B/libs.tech/xschem/xschemrc' > ./xschemrc
```

# Inverter Design Example

輸入 xschem 就可以開啟並新建電路圖

![png](/public/img/xschem_tutorial/1.png)

使用 left click + shift + i 來新增元件

![png](/public/img/xschem_tutorial/2.png)

請依序拉出 vsource, pfet, nfet, lab_pin, gnd, code_shown

電路完成圖會像下圖

![png](/public/img/xschem_tutorial/3.png)

## 電路圖元件設計重點

- vsource, lab_pin, gnd, code_shown 在 xschem_library 資料夾

- pfet, nfet 在 sky130_fd_pr 資料夾

- 選擇 pfet_01v8 與 nfet01v8

- Pulse 訊號的 SPICE 語法為 PULSE(V1 V2 TD TR PW PER NP)

- 電路使用的 Pulse 訊號為 PULSE(0 1.8 1ns 1ns 5ns 10ns)

- code_shown 的 value 要改成

   ".lib /usr/local/share/pdk/sky130A/libs.tech/ngspice/sky130.lib.spice tt

  .tran 0.1n 100n

  .save all"

## Simulation Result

![png](/public/img/xschem_tutorial/4.png)

![png](/public/img/xschem_tutorial/5.png)

# References

1. [video](https://www.youtube.com/watch?v=cUx2cBYAZOk)

