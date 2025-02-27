+++
title = 'JavaScript 中用 var, let, 以及 const 有什麼差別？'
date = '2025-02-28T01:59:14+08:00'
draft = false
tags = ["JavaScript" , "var let const"]
categories =["JavaScript"]
+++
![VerLetConst](/images/VerLetConst.png)
繼續這邊來整理JavaScript 中變數跟常數var, let, 以及 const 有什麼差別？  
可以從提升、初始化、重複宣告、重新賦值、作用域看有不同的行為。  

### 提升、初始化
我們可以在上一篇整理文章中，看到兩階段運行中提升的變化。  
var 宣告的變數會自動初始化，因此在宣告前就使用變數，不會出現錯誤，而會是 undefined。  
但是 let 與 const 則，而是會進到暫時死區 (TDZ)，因此在 let 與 const 宣告變數前使用該變數，會出現錯誤。  


---

也可以在當中看到var 可以被重複宣告let 與 const 則不行。  
### var 可以被重複宣告
var 可以被重複宣告，但是 let 與 const 則不行。   
所以當用的是 var 時，可以做到以下這樣：  
```
var greeting = "Hello! ";
var greeting = "Hi Hi";
```

### let 不能重複宣告，但可以重新賦值
所以會如下面這樣：  
如果let 像上面重複宣告，   
let greeting = "Hello! ";  
let greeting = "Hi Hi";  
會出錯 SyntaxError: Identifier 'greeting' has already been declared  
但是可以:  
```
let greeting = "Hello! ";
greeting = "Hi Hi";
```

### const 不行重複宣告、賦值，但可以改變該物件
const是不能被reassign重新賦值，但是可以改變。  
舉例：  
```
const a=1;
console.log(a);
a=2;
```
這邊會出現錯誤TypeError  
Assignment to constant variable  
常數，不能再重新賦值。  


那又說可以改變該物件，是怎麼改？
```
const a = ["a","b","c"];
a[0]="X";
console.log(a);

\\印出 ['X','b','c']
```
---
### 作用域的差別
在作用域上，var 可以是全域、也可以是以function函式中作為範圍。  
let 與 const 則是以區塊block作為範圍。let 跟 const 只在它們所在的區塊內有效，使它們更具可控的預測性。  




#### 延伸問題：什麼時候該用 let ? 什麼時候用 const ?
let 和 const 都是用來宣告的關鍵字，主要的區別在於是否需要重新賦值?  
當變數的值不會變時，優先使用 const，這樣可以確保變數不會被意外修改，提升程式的可讀性與安全性。  

[ExplainThis：在 JavaScript 中用 var, let, 以及 const 有什麼差別？什麼時候該用哪個？ ](https://www.explainthis.io/zh-hant/swe/js-var-let-const-in-javascript)