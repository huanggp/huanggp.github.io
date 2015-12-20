---
layout: post
title: "GitHub 博客搭建与MathJax配置 "
date: 2015-12-20 14:44:06 -0700
comments: false

---
 
[toc] 
 
GitHub  博客搭建过程



# 一、 fork 一个基于jekyll的项目开始

+ 1有多个项目存在

需要设置_config.yml  中的 baseurl: /projectName，并且需要设置分支为 gh-pages

访问路径就是 http://username.github.io/projectName

+ 2 独立项目 

本次设置是用一个独立帐号进行设置，设置分支为 master ,并且将projectName设置为 username.github.io

访问路径就是 http://username.github.io



# 二、 配置MathJax 

因为是页面渲染，所以在 _layout 目录下的所有文件的文件头上加入  MathJax 的js渲染

```
<script type="text/javascript"
 src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

```

_config.yml 中对markdown 的配置保留默认的（本例没有使用 kramdown）

#  三、 最终展示效果如下



##公式一
$$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$
##公式二
$$\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N$$

