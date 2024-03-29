---
title:  "使用 Google Cloud DNS 設定域名"
date:   2021-05-31 09:15:00 +0800
categories: Tutorial
tags:  [GCP,DNS]
--- 
我是wells，擔任過室內配線的國手，征服了電氣領域後，現在正跨大版圖到資訊界。

## 料理食材(內文內容)
- [X] 簡介
- [X] DNS設定流程

## 誰可以安心食用(適合誰讀)
- [X] 有閒錢
- [X] 已經有外部 IP 但還沒有域名

## 服用完你會獲得什麼
- [X] 知道如何亂花錢
- [X] 知道如何設定 GCP Cloud DNS
- [X] 知道如何把域名連到你的 IP

## 簡介
設定域名是部署專案的起手式，在使用雲端伺服器，如 GCP、Linode，雖然在建立時會提供給你外部 IP，但是你我都絕對不會想要給客戶一組 IP 位址，然後跟客戶說「以後你就輸入這個 IP 連到專案。」，如果你這麼做大概八成會被老闆打死，而這種作法還有一個缺點，就是原本可以用來部署多個專案的伺服器就變成只能部署一個了，十分的浪費，這是因為每一台的機器外部 IP 是唯一的，而在設定好紀錄集後，我們就可以把多個域名指向同一個 IP,並且以域名劃分多個專案，這樣子在同一台伺服器跑多個專案了。

## 設定流程
以下示範從購買域名到設定好對應的 IP
1. 向域名註冊商購買域名
2.   更改域名的名稱伺服器（Name Server）
3. 新增紀錄集

### 向域名代理商購買域名使用權
目前市面上有許多域名註冊商，如 [Gandi](https://www.gandi.net/)、[GoDaddy](https://tw.godaddy.com/)甚至也可以在[google domains](https://domains.google.com/registrar/search)購買，隨便挑選一間即可，內容不會差多少。

這邊我們以[Gandi](https://www.gandi.net/)為例 ，首先先搜尋自己想要的域名能不能購買

![picture 2](/assets/images/2021-05-31-使用GCP設定DNS-4206095e809cdc4cf374f8d1d32370b98e675400d574ad6b7b16f064f35dc659.png)  
依照畫面顯示，`abc987.tw`這個域名可以被購買，一般都是以年為單位計算。
順帶一提，越接近根域名就越貴，這是什麼意思呢？簡單來說就是域名越短就越貴，如果再搭配`.com`、`.net`這些頂級域名的話，價格就會更高。

加入購物車後就可以付錢~~推坑~~了。

### 更改域名的名稱伺服器（Name Server）
購買完域名後，預設會使用該廠商的名稱伺服器（Name Server），但如同本篇文的題目，我們打算改用google的名稱伺服器，首先先到購買廠商的域名設定，找到名稱伺服器的欄位

![picture 3](/assets/images/2021-05-31-使用GCP設定DNS-c8954dddbfd449bd496ae21223eae76453dd5485a7da0f3b1ad90aaf8bee4274.png)  
預設的畫面可能不會長得像這樣，名稱伺服器可能是空的，也可能是使用該廠商的名稱伺服器，但不管怎樣我們想要的結果是像現在的畫面一樣。

首先先找到GCP的Cloud DNS
![picture 4](/assets/images/2021-05-31-使用GCP設定DNS-9c4b0298c47f4521f27566f7ac021eb97305fbd6b0ac0f97f66eb5cf9d8d35da.png)  
  
進入後新增DNS區域，如下圖
![picture 5](/assets/images/2021-05-31-使用GCP設定DNS-d4ff48455f7cacacc36d0e810ee5ccbb0449afeb80a9f580de823a27fb51e091.png)  
在DNS名稱的地方填入你購買的域名

新增完成後你就可以看到你的以下這個畫面
 ![picture 6](/assets/images/2021-05-31-使用GCP設定DNS-75d9677bfad32c6f70a48805ea3a4a55e4e49250f29ce5d6bf9a1b7167e7afe4.png)  
之後把紅框中的內容貼到你購買域名的外部伺服器設定 ，這樣子使用GCP的名稱伺服器就設定完成了。

### 新增紀錄集
在完成上述兩個步驟後，你還是沒有辦法連到你的伺服器，因為你還缺少設定域名與 IP 的關係

![picture 8](/assets/images/2021-05-31-使用GCP設定DNS-52a2d2ce0ffe696fbf40c6035096607348e555bdd8f2c9cc7c9f38656806ac42.png)  
點擊上方工具列的新增紀錄集，會進入以下畫面
![picture 7](/assets/images/2021-05-31-使用GCP設定DNS-834d0015a3d347b95bbaf56e5d65216f53c6fedf2351d96c195536ce32489eb4.png)  
這裡我們可以看到資源紀錄類型是A，這也就是我們最常見的紀錄集`A record`，它用來設定域名與  IP 的關係，例如設定`abc.wells.tw`指向`33.23.141.32`，那麼我們在瀏覽器搜尋`abc.wells.tw`就會自動對應到`33.23.141.32`

輸入完後按下新增，接著過一下再去 瀏覽器搜尋`abc.wells.tw`你就可以連到你設定的 IP 了，或是使用[site24x7](https://www.site24x7.com/find-IP-address-of-web-site.html)來確認是不是有設定完成。

## 結語
DNS的設定其實並不難，但是有很大一部分是對於網路的基礎知識並不了解，但只要從頭到尾~~踩過一次坑~~設定過一次，就可以應付大部分的情況了。