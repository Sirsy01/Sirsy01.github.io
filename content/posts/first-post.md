
---
title: "我的第一篇博客"
date: 2026-04-28
draft: true
math: true
---

### 量子演化公式
这是一个行内公式：$E = mc^2$。

这是一个块级公式：
$$\hat{H} = \hbar \omega \left( a^\dagger a + \frac{1}{2} \right)$$

### 代码测试
```julia
using QuantumToolbox
# 定义一个简单的算符
a = destroy(10)
println(a)