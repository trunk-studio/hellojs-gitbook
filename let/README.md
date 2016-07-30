# let 語法

## scope的使用

### 使用var

```bash
var i = 1;
{
  var i = 0;
  console.log(i);
}
console.log(i);
```
學過一般的程式語言ex:c,c++,java<br>
會很直覺的覺得第一個印出來的是0,第二個是1<br>
事實上再javascript裡面兩個都是0<br>

### Why?

在 ES6 之前的 ECMAScript 規範中，對於 scope 的定義只有兩種，一為全域活動範圍(global scope)，一為函數活動範圍(function scope)。<br>
你每定義一個函數，就會建立一個屬於這個函數的活動範圍；不在函數內的資源就屬於全域活動範圍。<br>
ECMAScript 並沒有採用區塊即活動範圍的定義。所以像 C 語言那樣的區塊用法，在 JavaScript 中就是錯的。<br>

ES6 以前，也只有 var 一種變數宣告方式。它的用途和函數活動範圍有關。<br>
在函數內以 var 宣告的變數，僅限函數活動範圍內可用，外部看不到。<br>
而沒有用 var 或在函數外宣告的變數，就屬於全域範圍了。var 是看函數，而不是區塊。<br>
所以像從 C++/Java/C# 使用者帶來的使用習慣，其實在 JavaScript 中皆無預期效果，甚至會是 bug 。<br>

### 使用let

```bash
let i = 1;
{
  let i = 0;
  console.log(i);
}
console.log(i);
```
基本上let全盤適用c,c++,Java在scope上的用法
所以結果會是
第一個印出來的為0
第二個印出來的為1

### Source

[let vs var](http://rocksaying.tw/archives/2015/ES6_var,let,const.html)
