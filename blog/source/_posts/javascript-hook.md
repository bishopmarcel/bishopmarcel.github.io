---
title: javascript-hook
date: 2023-07-14 15:05:22
tags:
---

[TOC]



### Function

##### debugger

###### 示例代码

~~~javascript
(function() {}).constructor("debugger")()

// 等价于

Function("debugger")()
~~~

###### hook代码

~~~javascript
(function() {
  'use strict';

  const constructor_ = Function.prototype.constructor;
  Function.prototype.constructor = function(value) {
    if (value === "debugger") {
      return;
    }
    return constructor_(value);
  }
})();
~~~



### eval

##### 普通

###### 示例代码

~~~javascript
(function() {}).constructor("debugger")()

// 等价于

Function("debugger")()
~~~

###### hook代码

~~~javascript
(function() {
  'use strict';

  const eval_ = window.eval;
  window.eval = function(value) {
    debugger;
    return eval_(value);
  }
})();
~~~