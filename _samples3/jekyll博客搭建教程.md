---
title: "jekyll博客搭建教程"
collection: samples3
type: "Samples3"
permalink: /samples3/jekyll博客搭建教程
venue: "UC San Francisco, Department of Testing"
date: 2025-11-09
location: "San Francisco, California"
number: 1
excerpt: "这里记录jekyll博客的搭建教程"
---

---

从Github上拉取项目（b1分支）

```bash
git clone -b b1 git@github.com:dayaobai/dayaobai.github.io.git
```

清理旧的Gem

```bash
bundle clean --force
```

注册Gem

```bash
gem install bundler jekyll
```

运行

```bash
bundle exec jekyll serve
```