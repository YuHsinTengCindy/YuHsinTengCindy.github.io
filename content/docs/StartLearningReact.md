+++
title = '整理學習React'
date = '2025-02-26T14:56:40+08:00'
draft = false
tags = ["Start Learning React"]
categories =["React"]
+++
![React](/images/react01.png)
## React 是什麼？
先來基本瞭解下，React 是什麼？
* React 是一個陳述式、高效且具有彈性的 JavaScript 函式庫，用以建立使用者介面。它讓你使用小巧而獨立的「component」，來建立複雜的 UI。
* 由Ｆacebook在2013年開發出來的
* 嚴格上來說，React是函示庫（library),而不是框架（framework)

官網也大大地寫著：[(React官網)](https://react.dev/)  

The library for web and native user interfaces  
用於網頁和原生應用的使用者介面函式庫


### 框架（Framework） vs. 函式庫（Library） 簡單區別

| :rocket: 框架（Framework）|:hammer_and_wrench: 函式庫（Library） | 
| ------------------------ | ---------------------------------- |
| 提供完整架構，規定開發方式   | 提供功能，開發者決定怎麼用   |
|「框架呼叫你的程式」（控制反轉）|「你呼叫函式庫」（開發者主導）|
|有規範，要照它的規則寫|彈性高，可以自由組合|


:bulb: 比喻：

框架 = 連鎖手搖飲（基本著有標準 SOP，必須照流程做）  
函式庫 = 夜市小吃（自由選擇想吃什麼、怎麼搭配）

### 例外與灰色地帶：為什麼有人會認為 React 是框架？
雖然 React 被定義為函式庫，但當它與 React Router（路由）、Redux（狀態管理）等強大生態系工具 搭配使用時，它的 完整性 就變得類似於框架。因此，有些開發者在實務上會稱它為「框架級函式庫」。  
然而，React 本身不強制這些工具，因此仍然歸類為函式庫。


### 為什麼要選擇學習使用 React ？  
編寫網頁需要用到三種語言：  
HTML，CSS，JavaScrip   

*那先思考，那為什麼要使用React?*

React 不是取代 HTML、CSS、JavaScript，而是讓 前端開發更高效、更有組織性、更易於維護 的一個工具。  

:bulb: 可以把它想像成：蓋房子的現代化工程技術，在 HTML、CSS、JavaScript 的基礎上，提供更強大的開發方式。

它的核心價值在於 元件化（Component-Based）、狀態管理（State）、虛擬 DOM（Virtual DOM）、單頁應用（SPA）等技術，這些都是它能夠讓前端開發更高效的原因。  
* 元件化開發（Component-Based） → 避免重複代碼，提高維護性
* 狀態管理（State） → 讓 UI 變化更流暢，不需要手動操作 DOM
* 虛擬 DOM → 提高效能：只更新必要的部分，避免頻繁操作真實 DOM，減少渲染成本
* SPA 技術 → 提升使用體驗：讓網站行為更像 App，避免頁面重整，提供更順暢的互動
>延伸閱讀了解資訊  
>  * [React.js 從 【0】 到【1】推坑計畫-【Day 5】 第一個 hook - useState
(...State 是什麼？)](https://ithelp.ithome.com.tw/articles/10214397)
>  * [什麼是 Virtual DOM?](https://www.explainthis.io/zh-hant/swe/react-virtual-dom)
> * [什麼是 SPA (Single-Page Application)？有什麼優點和缺點？](https://www.explainthis.io/zh-hant/swe/spa)
>  * [React 狀態管理大亂鬥](https://5xcampus.com/posts/react-compare-state-management.html?srsltid=AfmBOorGCHXDOVGtTdzu9Sk--8ZTNjwf5qm3Rle8QE_Vdn6PYyCrdIEe)

最後是自己的murmur，在於我個人，其實不管是React還是Vue都是很陌生的,  
從 市場需求、學習曲線、社群資源、企業應用 等面向分析，都有大概了解到他們各自的強大好用、有各自優點。  
但也了解對於初學者而言，React 更強大但學習曲線稍高，Vue 上手快但擴展性稍失色。  
是也有很多提到當學會一個，另一個就會很好上手，原理懂就容易可以多元理解。  
但都很陌生、都是要從頭學起的，就來研究學習React吧

