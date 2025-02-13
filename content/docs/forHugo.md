+++
title = '如何開始建立Hugo Web page?'
date = '2025-02-13T14:50:52+08:00'
draft = false
tags = ["hugo", "how-to"]
categories =["hugo"]
+++



![圖片描述](/images/forHugo.png)

## 如何開始建立Hugo Web page?
### 查詢網上資訊說5分鐘就可以建好？
一開始學習時在網上搜尋資料時，看到這標題真的很吸引人  
看到這個標題還想說，那…應該可以的吧？  
但是怎麼樣就是少了什麼沒有辦法成功...  
然後看助教幫同學處理問題也是花了點時間的,一起學習的同學也說有看到那吸引人眼晴的標題，她也是吶喊「才怪…連老師都抓一個小時，怎麼可能 5 分鐘就建好崩潰」

### 回頭整理
最近想整理資訊，建立自己的blog就又開始搜尋  
後來得知了很棒的建立資源，但版本必較舊了加上都是英文也是花了點時間吸收:laughing:

### 整理一下資訊上來
主要還是不外乎  
安裝環境、挑選主題、上傳 GitHub  
來～上教材：資訊是參考這邊（英文好的小夥伴可以打開來執行了）  
https://themes.gohugo.io/themes/hugo-papermod/
https://theplaybook.dev/docs/deploy-hugo-to-github-pages/  
https://www.youtube.com/watch?v=_QSr2_pxIJs

#### 安裝 Hugo 並創建新網站
```
brew install hugo 
hugo new site theplaybook-demo -f yml
```

使用 Homebrew 安裝 Hugo，並執行 hugo new site <site_name> 來創建一個新的網站資料夾 <site_name>，並包含 Hugo 的模板。
作者這邊執行完後有做`cd`到他建立的theplaybook-demo，所以自己建立時可以檢查一下，自己有沒有確實在建立的檔案裡面。  
#### 設定 baseurl
找到baseURL 目前先不要設定 baseurl，保持空白。  

#### 創建新頁面
```hugo new docs/test.md```  
用 hugo new <filename> 創建一個新的頁面。打開 test 文件，並將 draft: 設為false ，否則頁面將無法呈現。可以在 test. md 中添加隨便的內容。

執行 hugo server 可以在本地端的 localhost:1313 測試應用程式，但如果沒有設置佈景主題，可能會顯示佈局錯誤。  
#### 安裝佈景主題
```
git init 
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1  
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```
在專案根目錄下執行 git init 來初始化 Git 倉庫。安裝 PaperMod 佈景主題，使用上述指令來克隆該主題，或從 Hugo Themes 選擇其他佈景主題。  在 config.yml 中添加 theme: PaperMod。
我是在hugo.toml中添加 theme: PaperMod。
    
#### 配置 Github Actions 以發布到 Github Pages
創建 Git 倉庫並初始化 Git
創建 Git 倉庫、添加 README 文件，並推送第一次提交。

手動添加 gh-pages 分支
在倉庫中手動添加 gh-pages 分支，否則 Github Actions 會拋出錯誤。

設定 Workflow 的讀寫權限
在 Github 的設定中，進入 Settings > Actions > General > Workflow permissions，並允許讀寫權限。

#### 添加 Github Actions 部署檔案
avid hwang作者分享說，在專案根目錄下創建 .github/workflows/deploy.yml，並添加以下內容：
```
name: Publish to GH Pages
on:
  push:
    branches:
      - main
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout source
        uses: actions/checkout@v3
        with:
          submodules: true

      - name: Checkout destination
        uses: actions/checkout@v3
        if: github.ref == 'refs/heads/main'
        with:
          ref: gh-pages
          path: built-site

      - name: Setup Hugo
        run: |
          curl -L -o /tmp/hugo.tar.gz 'https://github.com/gohugoio/hugo/releases/download/v0.110.0/hugo_extended_0.110.0_linux-amd64.tar.gz'
          tar -C ${RUNNER_TEMP} -zxvf /tmp/hugo.tar.gz hugo

      - name: Build
        run: ${RUNNER_TEMP}/hugo

      - name: Deploy
        if: github.ref == 'refs/heads/main'
        run: |
          cp -R public/* ${GITHUB_WORKSPACE}/built-site/
          cd ${GITHUB_WORKSPACE}/built-site
          git add .
          git config user.name 'dhij'
          git config user.email 'davidhwang.ij@gmail.com'
          git commit -m 'Updated site'
          git push

```
但要留意的是  
他使用的是 Hugo v0.110.0 版本。  
我這邊有改成
```
curl -L -o /tmp/hugo.tar.gz "https://github.com/gohugoio/hugo/releases/download/v0.125.7/hugo_extended_0.125.7_linux-amd64.tar.gz"
```
我使用的是 Hugo v0.125.7 版本。  
要使用時可以注意一下自己要使用的版本喔～  
然後提醒一下，記得要把作者的這部分資料改成自己的喔
```
git config user.name 'dhij'
git config user.email 'davidhwang.ij@gmail.com'
```
這個工作流程做了以下幾件事：

1. 檢出源碼並包含子模組（即佈景主題）。  
1. 檢出 gh-pages 分支，並將靜態頁面存儲在 built-site 資料夾。  
1. 安裝 Hugo 並構建靜態頁面。  
1. 部署靜態頁面並推送到 gh-pages 分支。   
    
**注意：**
部署的內容將會預設部署到https://username.github.io/repository_name/
如果需要更改，更新`baseurl` 為自己的資料喔～