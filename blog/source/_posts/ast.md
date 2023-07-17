---
title: ast
date: 2023-07-17 20:00:19
tags:
---
反爬虫AST混淆JavaScript与还原实战

~~~javascript
Date.prototype.format = function (formatStr) {
    var str = formatStr;
    var Week = ["日", "一", "二", "三", "四", "五", "六"];
    str = str.replace(/yyyy|YYYY/, this.getFullYear());
    str = str.replace(
        /MM/,
        this.getMonth() + 1 > 9
            ? (this.getMonth() + 1).toString()
            : "0" + (this.getMonth() + 1)
    );
    str = str.replace(
        /dd|DD/,
        this.getDate() > 9 ? this.getDate().toString() : "0" + this.getDate()
    );
    return str;
};
console.log(new Date().format("yyyy-MM-dd"));
~~~


环境配置

~~~
Node.js
Visual Studio Code

npm i @babel/core
~~~


常量混淆原理

~~~
对象属性的两种访问方式
十六进制字符串
unicode字符串
字符串的ASCII码混淆
字符串常量加密
数值常量加密

~~~


对象属性的两种访问方式

~~~javascript
function People(name) {
  this.name = name;
}
People.prototype.sayHello = function () {
  console.log("Hello");
};
var p = new People("Tom");
console.log(p.name);
p.sayHello();
console.log(p["name"]);
p["sayHello"]();

~~~
![img.png](images/ast/img.png)


十六进制字符串

~~~javascript

// 字符先转 ascii码 再转 16进制

// charAt 用来取出字符串中对应索引的字符
// charCodeAt 用来取出字符串中对应索引的字符的ASCII码
// toString(16) 转成16进制

function hexEnc(code) {
  for (var hexStr = [], i = 0, s; i < code.length; i++) {
    s = code.charCodeAt(i).toString(16);
    hexStr += "\\x" + s;
  }
  return hexStr;
}

~~~
![img.png](images/ast/img_1.png)


unicode字符串
~~~javascript
function unicodeEnc(str) {
  var value = "";
  for (var i = 0; i < str.length; i++) {
    value +=
      "\\u" + ("0000" + parseInt(str.charCodeAt(i)).toString(16)).substr(-4);
  }
  return value;
}

// 标识符也支持unicode形式表示

// 标识符 以0、o、O组成的名字
// 如：0o000oO
// 注意：标识符不能以数字开头
~~~
![img.png](images/ast/img_2.png)
![img.png](images/ast/img_3.png)


字符串的ASCII码混淆

~~~javascript
// String.fromCharCode(120, 98);   //"xb"
// String.fromCharCode 用来将ascii码转为字符

function stringToByte(str) {
  var byteArr = [];
  for (var i = 0; i < str.length; i++) {
    byteArr.push(str.charCodeAt(i));
  }
  return byteArr;
}
console.log(stringToByte("Tom"));

console.log(String.fromCharCode.apply(null, [84, 111, 109]));

~~~
![img.png](images/ast/img_4.png)


字符串常量加密
![img.png](images/ast/img_5.png)

有些字符串无法加密
![img.png](images/ast/img_6.png)

数值常量加密
![img.png](images/ast/img_7.png)

增加JS逆向者的工作量
~~~
数组混淆
数组乱序
花指令
jsfuck

~~~

数组混淆

~~~javascript
// todo: 字符串可以提取到一个数组里面去，可以让一个函数里面一个数组
~~~
![img.png](images/ast/img_8.png)


数组乱序
