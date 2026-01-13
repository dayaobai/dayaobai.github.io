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

## 1. 远程项目拉取

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
```**bash**
bundle exec jekyll serve
```



## 2. 部署

### 1.  初始化并提交代码
```bash
git add . 
git commit -m "Initial commit"
```

### 2.  添加远程仓库（只需第一次）
```bash
git remote add origin git@github.com:dayaobai/dayaobai.github.io.git
```

### 3. 创建分支并切过去（只需第一次）
```bash
git checkout -b b1
```

### 4. 推送
```bash
git push -u origin b1
```