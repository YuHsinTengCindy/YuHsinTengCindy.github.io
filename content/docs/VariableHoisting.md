+++
title = '什麼是 Variable Hoisting ?JavaScript 變數提升'
date = '2025-02-26T21:04:16+08:00'
draft = false
tags = ["JavaScript" , "Hoisting"]
categories =["JavaScript"]
+++
![VariableHoisting](/images/VariableHoisting.png)
一邊整理JavaScript所學知識   
來筆記釐清 JaveScript 在執行階段內文如何運行的思路。  
什麼是 Variable Hoisting ?JavaScript 變數提升  
我們用runtime的角度來看，它不是一口氣跑完，是分層兩階段運行，在創建期(Creation Phase)和執行期(Execution Phase)階段有不同得變化。


---
來分解動作  

在 **建立期** 時，會兩階段運作
1. 註冊名稱identifier（要那個東西的名字）
1-2. 進行初始化（初始化那個東西，通常是undefined)


在 **執行期** 時
1. 執行函數/賦值（動作執行，或是給值，都是這個時候）



---

好的，來看

var a = 1;  
console.log(a);  

```
建立期:
1. var a    1-2.undefined 
```

```
執行期:
a = 1
console.log(a) /印出1
```
---
那同理可知，如果是這樣呢？

console.log(a);  
var a =1;  
console.log(a);  

會印出什麼？
```
答案是：
undefined （第一圈已知有var a也有初始化，但第二圈執行期時先跑了他，但這邊還沒有賦值）
1         （已知a=1,執行出結果1）
```
所以同理就可以理解  
if(false){  
 var a = 1;  
}  
console.log(a);  
`是印出 undefined`  

---
**那let呢？let不會變數提升？**  
No No~  
要記得JS本身就是分層兩階段運行，不管怎麼寫就是兩階段運做，運行時就是會提昇，那到底為什麼會有出錯的狀況呢？  

像是  
console.log(b);  
let b = 1;  
  
我們來看看
``` 
建立期
1. let b   
2.進入TDZ
```

```
執行期
❌ 出現 ReferenceError
訊息是 Cannot access 'b' before initialization
初始化之前無法存取“b”
```
在**ES6**之後加入了let/const，而let他解決了一些var會有的一些問題。  

像是如果var重複宣告，  
var a=1  
*//然後中間寫了很多很多...*後面又寫上，  
var a=2  
接 console.log(a)，答案是什麼？   
`會是  2`  
  
但是，如果是在有let的情況下，不小心發生這樣的狀況，它是會爆炸❌給你看的唷～  不對的事情，就是該出現錯誤訊息。  
  
---
**暫時死區（TDZ, Temporal Dead Zone）**  
那TDZ暫時死區是什麼，聽起來真的好像什麼遊戲很酷的大招？   
:bulb:可以想像，它是像是一個罩子一樣，把它覆蓋了起來。  
與 var 不同的是，let是會進入「暫時死區」（TDZ, Temporal Dead Zone），那怎麼把它罩子解開呢？  就是到程式執行到給值它們為止。  **如果在此之前訪問它們，會拋出錯誤!**  

> 但就特別的是，如果是:  
> let a;  
> console.log(a);  
> 這邊它沒有給他任何值，JS在這裡還是有退讓的。先思考有沒有let a，是有let a的，但沒有後續沒有罩子是什麼？對，就是被動的給了undefined。   

---
**常數宣告，const**  
也是跟let一樣修改了之前var這樣的錯誤。  
但留意因為**const是不能重新給值的**，所以如果是同狀況上面變const a;的情況，  
const沒有任何值是不行的喔，它就是沒有任何意義。  

---

**函式陳述式 (Function Declaration) 提升**

函式陳述式 (Function Declaration)
完整提升，名稱和內容都在建立期就準備好，所以可以提前呼叫

sayHi();

function sayHi() {
  console.log("Hi!");
}
來看看 JS 怎麼運作
```
建立期
1. 註冊名稱：function sayHi
2. 初始化：函式內容完整註冊（所以可以直接用）
```

```
執行期
1. 執行 sayHi() → 印出 "Hi!"
```
因為 function sayHi 在建立期時就已經被完全準備好，執行時可以直接使用！

換句話說，這段程式其實等同於這樣：
function sayHi() {   
  console.log("Hi!");   
}  
  
sayHi();   

---

**函式表達式 (Function Expression)**

sayHi(); `//  ❌TypeError: sayHi is not a function`

var sayHi = function() {    
  console.log("Hi!");  
};  
來看看 JS 怎麼運作  
```
建立期
1. 註冊名稱：var sayHi
2. 初始化：sayHi = undefined
```

```
執行期
1. 執行 sayHi() → ❌ TypeError（因為此時 sayHi 還是 undefined）
```

所以 sayHi() 在還沒賦值前就執行，會報錯

[MDN:提升（Hoisting）](https://developer.mozilla.org/zh-TW/docs/Glossary/Hoisting) 