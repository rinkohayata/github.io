---
title: "Hugo_インストールからサーバ起動まで"
date: 2022-07-29T01:04:11-07:00
draft: false
---

Updated: September 19, 2022  
Goal: HugoとGitHub Pagesで静的サイトを作る  
Step1: Hugoを導入する

<!--more-->

### 1 Hugoをインストールする

```
~> sudo apt install hugo
~> y
~> hugo version
```

### 2 Hugo用のディレクトリを作る

```
~> hugo new site NAME_THE_DIRECTORY
```
☆以下、`NAME_THE_DIRECTORY`=`hugo-dir`

### 3 Hugo用のディレクトリにgitのローカルリポジトリを置く

```
~> cd hugo-dir
~/hugo-dir> git init
~/hugo-dir (master)> 
```

### 4 Hugoからテーマを選ぶ PaperMod ver.

```
hugo-dir (master)> git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
hugo-dir (master)> echo 'theme = "PaperMod"' >> config.toml
```

### 5 ローカル環境でテーマを設定できているか確認する

```
hugo-dir (master)> hugo server
```
同じOSのブラウザで`http://localhost:1313/`を検索する

サーバを終了するときは[Ctrl]+[C]


