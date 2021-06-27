---
title:  "Ruby 使用 Double Splat Operator 修飾參數"
date:   2021-06-27 12:50:00 +0800
categories: Tutorial
tags:  [Ruby]
--- 
我是wells，擔任過室內配線的國手，征服了電氣領域後，現在正跨大版圖到資訊界。
## 簡介
此篇是延伸至上一篇 [Ruby 使用 Splat Operator 修飾參數](../Ruby-使用-Splat-Operator-修飾參數/index.html)，上篇介紹的是 Splat Operator (*)，會將傳入的引數變成一個 Array，而此篇的 Double Splat Operator (**) 則是會把引數變成 Hash，詳細內容就繼續看下去吧。

## 使用方式
在參數前方加入`**`，如以下：
```ruby
def test(**arg)
    ...
end
```

## Splat Operator (*)
使用 Splat Operator 修飾的參數會有以下幾個特性：
1. 可以傳入不限數目的引數，並將所有傳入的引數變成一個 Array，內容依傳入順序排序
2. 該參數為選填，假如沒有傳入引數，該參數的變數會是一個空的 Array
3. 不能有兩個以上 Splat Operator 修飾的參數
4. 可以在其他參數中間
5. 假如其他參數有預設值，一定得在有預設值的參數後面，但建議不要用~~沒必要刁難自己~~

### 使用範例


## 結語
此篇是用來介紹 Splat Operator，在下一篇會介紹 Double Splat Operator 的用法。

## 參考連結
- [Parameter with double splat operator (**) in Ruby](https://medium.com/@sologoubalex/parameter-with-double-splat-operator-in-ruby-d944d234de34)