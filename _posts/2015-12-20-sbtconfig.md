---
layout: post
title: "SBT 配置过程"
date: 2015-12-02 14:25:06 -0700
comments: false
---


[TOC]

ubuntu 下安装sbt



#1 安装



```

sudo apt-get install sbt

```

#2 配置

配置信息在

```

ls /etc/sbt-launcher-packaging -l

-rw-r--r-- 1 root root  180 12月 11 09:36 sbtconfig.txt

-rw-r--r-- 1 root root  986 12月 11 09:43 sbtopts



```



## sbtopts

配置相关的sbt的设置

##sbtconfig.txt

配置虚拟机启动参数方面的内容

#3 配置 .sbt 

```

drwxrwxr-x   3 daniel daniel  4096  8月 28 17:55 0.13/

drwxrwxr-x   5 daniel daniel  4096 12月 10 16:59 boot/

-rw-rw-r--   1 daniel daniel   264 12月 10 14:48 repositories

```

这里重点关注 repositories

```

[repositories]

   local

   oschina:http://maven.oschina.net/content/groups/public/

   oschina-ivy:http://dl.bintray.com/typesafe/ivy-releases/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext]

```

设置了oschina下载源，如果有其他下载源都在这里配置
$$	x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a} $$














