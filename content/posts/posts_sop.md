+++
date = '2026-04-30T14:21:46+08:00'
draft = true
title = 'Posts_sop'
+++

这里记录我们写个人blog的大致流程。不包括之前创建个人账户的过程，只包括怎么在mac上继续来写作blog内容。

在terminal中
```
cd ~/Documents/my_blog
```

之后创建新的内容

```
hugo new posts/quantum-optics-intro.md
```

在~/Documents/my_blog/content/posts下可以找到我们新创建的文件，之后我们可以直接打开这个文件进行编辑，注意如果有数学内容，记得把math调整成true

```
---
title: "量子光学简介"      # 网页上显示的中文大标题
date: 2026-04-28
draft: false           # 【重要】确保这里是 false，否则发布后别人看不到
math: true             # 如果有公式，确保开启这个
---
这里开始写正文...
```

之后就是打包发送到github发布，但只要我们把draft设置为true