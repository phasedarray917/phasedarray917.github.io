---
layout: post
title: MOS Varactor 簡介
categories: Research 
tags: [microwave engineering]
---

author: 網路資料整理

> Description:
>
> 這篇文章主要講述MOS Varactor的連接方式和運作原理，以及不同模式的MOS Varactor 各自的特性。

<!-- more -->

# MOS Varactor 簡介

可變電容(varactor)在壓控振盪器中有著頻率調諧的功能，是不可或缺的重要元件。一般在金氧半(MOS)標準製程中，二極體電容(p+_Nwell 接面電容)和 MOS 可變電容為常使用的兩大類，後者根據其端點連接的不同可操作於不同模式，又可分為強反轉型(strong inversion mode)和累積型(accumulation mode)[1]。

## MOS Capacitor Characteristic

利用MOS製作電容，具體的方法如下，將Gate端作為一端，另一方面將Source，Drain，Body三端相連，作為另外一端。 
MOS 電容最大的優勢是具有最大的電容密度，當需要大電容的時候進行穩壓，濾波和去耦，通常會使用MOS電容。 
但 MOS 電容有一個致命的缺點，由於是 MOS 元件，他的電壓相關係數非常大，會因為兩端電壓的改變而改變容值，很難有穩定的容值。在一些情況下我們也可以利用這個特性制作壓控電容Varactor，應用於VCO中，進行調諧。

![png](/public/img/mos_varactor/1.png)

當我們固定Source，Drain，Body三端電壓為1.8V，調整Gate點電壓，可以得到MOS電容的C-V曲線，其中分為三個區域，積累區(Accumulation)，空乏區(Depletion)，反轉區(Inversion)。MOS的電容特性曲線，我們會分區域進行講解[2]。

![png](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjd87jFdbevfhNH1l7hRteOspQwC-h7tOz-YPa4jGKRPMHHRQ7LjDQBpeXpJd3OUE1uIF54QMUNrgZb-FPfIqWRYLwjoW4cr2sBmRZVorg-GyS4Zqga7A8crKd-QrsDy5CZlC8ZMkYDbkE/s1600/c-v-curve-of-mos-capacitor.gif)



### Accumulation Area

此時 PMOS 的 Gate 端電壓大於 Body 端電壓。即 Vgb > 0，則 Gate 氧化層下面會吸引Nwell 中的多數載子，從而形成積累層。我們可以認為是兩個極板被隔離開，主要組成為 Gate 氧化物的電容，所以電容值較為穩定。注意在設計中一般喜歡讓 MOS 電容工作在這個區域，因為這個區域電容容值穩定，並且相比於 Inversion Area 他的高頻性能更好。

### Depletion Area

此時 PMOS 的 Gate 端電壓小於 Source 端電壓，但是仍然小於閾值電壓 |Vth|，即 |Vth| > |Vgs| > 0。此時用 MOS 的工作狀態是指處於 Sub-thresold Area，也就是弱反型，溝道還未形成，但 Gate 氧化層下面已經形成空乏層。此時 MOS 電容我們認為是空乏層和閘氧電容的串聯，主要由較小的空乏層電容占主導，所以電容值較小，且空乏層在未完全形成時，與電壓關聯大，所以中間一段電壓變化較為陡峭。

### Inversion Area

此時 PMOS 的 Gate 端電壓很小，且和 Source 端電壓差大小於閾值電壓 |Vth| ，即 |Vth| < |Vgs| 。此時 MOS 的工作狀態是處於強反型層，溝道形成，在空乏層之上。空乏區電容被溝道隔絕，此時 MOS 電容我們認為也是閘氧電容，所以與電壓變化不大。但是工作在反型區的電容高頻性能較差。

## 可變電容的分類

本節主要介紹金氧半製程所能提供的可變電容分類，包括二極體電容、標準 MOS 可變電容、反轉型 MOS 可變電容，以及累積型可變電容，並由其中選擇出符合實際上應用的可變電容。

### 二極體電容(p+_Nwell junction Capacitance)

二極體電容主要是利用 p+ 和 Nwell 兩層形成的 PN 接面(junction)來實現之，接面的空乏區(depletion region)受逆偏壓(reverse bias)影響而形成一個壓控可變電容。此種電容具有極佳的品質因數，然而只有在逆偏壓的時候具有電容特性，當振盪訊號為大訊號的時候，PN 接面有機會進入順偏區使其喪失電容的功能。再者此類電容的調動範圍小，僅有在接近順偏區的時候有較明顯的容值變化。不適用於文獻參考中的振盪器設計中。

![png](/public/img/mos_varactor/2.png)

### 標準 MOS 可變電容(Standard-mode MOS Varactor)

相較於二極體可變電容，MOS 可變電容不存在順偏壓的問題，具有較大的電壓控制與動態範圍。以 NMOS 為範例，其汲極(Drain)、源極(Source)與基底(Bulk)三個端點相連接,利用與閘極(Gate)端的跨壓來進行電容調諧。其中我們可以看出此類可變電容之電容特性非單調曲線，其調諧範圍受到限制，且當振盪器應用於鎖相迴路時，此特性會使得電路的鎖定時間(lock time)變長甚至無法成功鎖定。

![png](/public/img/mos_varactor/3.png)

### 反轉型 MOS 可變電容(Inversion-mode MOS Varactor)

一般壓控振盪器需要單調(monotonic)特性的調諧，改變標準型態 MOS 可變電容中的節點連接方式，將汲極與源極連接，基底接到最低電位(NMOS)或是最高電位(PMOS)。反轉型可變電容之可調範圍比標準型可變電容的來得大，因為反轉型可變電容不再進入累積區(Accumulation region)，而是工作於強反轉區與中(弱)反轉區，另外基底端接到最正或最負電壓，消除了基底效應(Body effect)，使得電壓電容特性曲線稍微往外移。在強反轉區有高通道電阻存在。電阻大小關係到品質因數，故在強反轉區可變電容有最小的品質因數。NMOS 具有較大的載子移動率，所以跟 PMOS 相較之下其寄生電阻較低，但由於基底共用的原因使得 NMOS 可變電容易受基底雜訊影響，此因素使得 PMOS 可變電容反而比NMOS 有較佳的品質因數表現。然而考慮到 layout 與可變電容的調諧方式，參考文獻裡頭採用的為反轉型的可變電容。

![png](/public/img/mos_varactor/4.png)

![png](/public/img/mos_varactor/5.png)

### 累積型 MOS 可變電容(Accumulation-mode MOS Varactor)

與反轉型 MOS 可變電容一樣，為了達到單調的調整，發展出累積型 MOS 可變電容。在一般的 PMOS 元件中，改變其汲極與源極的參雜型態(doping type)，由 p+ 改成 n+，抑制少數載子電洞在通道中產生，防止進入強反轉區，而工作在累積區與空乏區，較反轉型的可變電容變化趨勢來得緩和，且因為 Nwell 上的 n+ 參雜使得寄生電阻來得較小，同時 Nwell 亦有隔絕基底雜訊的功能，使得此類電容具有較佳的品質因數。但是在我們所採用的 tsmc 0.18μm 製程並無提供此類電容，電路設計者欲使用此電容需要製作測試元件(testkey)建立等效模態參數，始能應用於電路模擬之中。

![png](/public/img/mos_varactor/6.png)

# References

1. https://ndltd.ncl.edu.tw/cgi-bin/gs32/gsweb.cgi?o=dnclcdr&s=id=%22095NCTU5435060%22.&searchmode=basic
2. https://zhuanlan.zhihu.com/p/709425719?share_code=43vHqxT4BR35&utm_psn=1922236923080081629

