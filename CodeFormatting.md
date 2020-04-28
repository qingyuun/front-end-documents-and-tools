# 前端代码规范


## 基本规范

### 命名分类

* {-&nbsp;&nbsp;camelCase&nbsp;&nbsp;-}（驼峰式，也叫小驼峰命名，{-&nbsp;&nbsp;e.g. userInfo&nbsp;&nbsp;-}）

* {-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}（帕斯卡命名式，也叫大驼峰命名，{-&nbsp;&nbsp;e.g. UserInfo&nbsp;&nbsp;-}）

* {-&nbsp;&nbsp;kebab-case&nbsp;&nbsp;-}（短横线连接式，{-&nbsp;&nbsp;e.g. user-info&nbsp;&nbsp;-}）

* {-&nbsp;&nbsp;snake_case&nbsp;&nbsp;-}（下划线连接式，{-&nbsp;&nbsp;e.g. user_info&nbsp;&nbsp;-}）

### 目录命名

组件目录使用&nbsp;&nbsp;{-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}&nbsp;&nbsp;，其他目录统一使用&nbsp;&nbsp;{-&nbsp;&nbsp;kebab-case&nbsp;&nbsp;-}&nbsp;&nbsp;风格

### JS命名

单数复数使用&nbsp;&nbsp;{-&nbsp;&nbsp;kebab_case.js&nbsp;&nbsp;-}&nbsp;&nbsp;风格

### CSS命名

统一使用&nbsp;&nbsp;{-&nbsp;&nbsp;snake_case.css&nbsp;&nbsp;-}&nbsp;&nbsp;

### HTML命名

统一使用&nbsp;&nbsp;{-&nbsp;&nbsp;snake_case.html&nbsp;&nbsp;-}&nbsp;&nbsp;

## HTML 规范

### 语法标准

* 缩进使用 tab（2 个空格）；

* 嵌套的节点应该缩进；

* 在属性上，使用双引号，不要使用单引号；

* 属性名全小写，用中划线（-）做分隔符；

* 要在自动闭合标签结尾处使用斜线；

```

<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/image.png" alt="Image" />

    <!-- 属性名全小写，用中划线（-）做分隔符 -->
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>

```

### 规定字符编码

通过声明一个明确的字符编码，让浏览器轻松、快速的确定适合网页内容的渲染方式，通常指定为'UTF-8'。

```

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
  </head>
  ...
</html>

```

### 减少标签数量

```

<!-- bad -->
<span class="avatar">
  <img src="..." />
</span>

<!-- good -->
<img class="avatar" src="..." />

```

### 语义化标签

html 的标签能使用语义化的，尽量使用语义化标签，避免一个页面都是 div 或者 p 标签

```

<!-- bad -->
<div>
  <p></p>
</div>

<!-- good -->
<header></header>
<footer></footer>

```

## CSS规范

### 缩进

使用 tab 缩进（2 个空格）

```

.element {
  border-radius: 10px;
  width: 50px;
  height: 50px;
}

```

### 分号

每个声明结束都要加分号

```

.element {
  border-radius: 10px;
  width: 50px;
  height: 50px;
}

```

### 注释

注释统一使用 /* */

```

/* 这里是注释 */
.element {
  width: 50px;
  height: 50px;
}

```

### 引号

* url 的内容要用引号

* 属性选择器中的属性值需要引号

```

.element:after {
  content: "";
  background-image: url("logo.png");
}

li[data-type="single"] {
  ...;
}

```

### 命名

* 类名使用小写字母，以中划线分隔

* id 采用驼峰式命名

```

/* class */
.element-content {
  ...;
}

/* id */
#myDialog {
  ...;
}

```

## JavaScript 规范

### 缩进

使用 tab 缩进（2 个空格）

```

if (x < y) {
  x += 10;
} else {
  x += 1;
}

```

### 变量命名

* 变量采用驼峰式命名&nbsp;&nbsp;{-&nbsp;&nbsp;camelCase&nbsp;&nbsp;-}

* 常量使用全大写，用下划线连接

* 构造函数和Class采用&nbsp;&nbsp;{-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}

```

var thisIsMyName;

var MAX_COUNT = 10;

function Person(name) {
  this.name = name;
}

Class Person {
    
}

```

### 变量声明

一个函数作用域中所有的变量声明尽量提到函数首部。优先使用块级变量&nbsp;&nbsp;{-&nbsp;&nbsp;let&nbsp;&nbsp;-}&nbsp;&nbsp;-} 和 &nbsp;&nbsp;{-&nbsp;&nbsp;const&nbsp;&nbsp;-}，如无需修改的常量使用&nbsp;&nbsp;{-&nbsp;&nbsp;const&nbsp;&nbsp;-}

### 单行长度

单行长度不得超过 100，超过部分需要换行

### 分号

~~统一要加分号。~~

### 空格

* 三元运算符'?:'前后

* 逗号后必须要有空格

* 代码块'{'前

* 下列关键字前：else, while, catch, finally

* 下列关键字后：if, else, for, while, do, switch, case, try,catch, finally, with, return, typeof

* 单行注释'//'后（若单行注释和代码同行，则'//'前也需要），多行注释'*'后

* 对象的属性值前

* for 循环，分号后留有一个空格，前置条件如果有多个，逗号后留一个空格

* 无论是函数声明还是函数表达式，'{'前一定要有空格

* 函数的参数之间

例：

~~~

// not good
var a = {
  b : 1
};

// good
var a = {
  b: 1
};

// not good
++x;
y++;
z = x ? 1:2;

// good
++x;
y++;
z = x ? 1 : 2;

// not good
var a = [ 1, 2 ];

// good
var a = [1, 2];

// good
var doSomething = function(a, b, c) {
  // do something
};

// good
doSomething(item);

// not good
for (let i = 0;i < 6;i++) {
  x++;
}

// good
for (let i = 0; i < 6; i++) {
  x++;
}

~~~

### 空行

* 变量声明后（当变量声明在代码块的最后一行时，则无需空行）

* 注释前（当注释在代码块的第一行时，则无需空行）

* 定义函数前

* 文件最后保留一个空行

```

var x = 1;

// 注释前要有空行
if (x >= 1) {
  var y = x + 1;
}

function test () {
  ...
}

```

### 换行

* 代码块'{'后和'}'前

* 变量赋值后

```

// good
var a = {
    b: 1,
    c: 2
};

x = y ? 1 : 2;

// good
if (condition) {
    ...
} else {
    ...
}

try {
    ...
} catch (e) {
    ...
} finally {
    ...
}



// good
function test() {
    ...
}


// good
var a,foo = 7,
    b, c, bar = 8;
    
```

### 注释

##### 单行注释

* 注释单独一行的情况下，注释的//后面要跟一个空格

* 注释如果和代码同一行，代码分号结束后，要跟一个空格，注释的//后也要跟一个空格

```

// 调用函数
foo();

var maxCount = 10; // 这是一个变量

```
##### 多行注释

多行注释使用下面这种形式：

```

/**
 * 代码注释1
 * 代码注释2
 */
 
 ```

多行注释建议在以下几种情况使用：

* 难于理解的代码段

* 可能存在错误的代码段

* 业务逻辑强相关的代码

* 


### 函数注释

复杂的函数，所有类，都必须进行函数注释，函数注释使用业界统一的规范，方便后续使用 jsdoc 生成文档。最好配置VSCode自动生成模板

例：

```

/**
 * @description 函数描述的 必填
 * @param id {Number} 传入需要获取名称的人物id 参数必填
 * @return {String} 返回的姓名 返回值必填，空为void
 * @author shi 2015/07/21 作者可选
 * @version 1.1.0 可以不写 版本可选
 * @example 示例代码，可选
 */
function getTaskName(id) {
  let name = "test";
  return name;
}

```

### 引号

最外层统一使用单引号，除非字符串嵌套的情况使用双引号。

```

var y = 'foo',
    z = '<div id="test"></div>';
    
```

### 对象，数组


* 对象属性名不需要加引号，如对象属性名是中划线命名的需要加引号（eslint 的 rules）


* 对象以缩进的形式书写，不要写在一行（单个属性可以写一行，es6 导入方法时可以使用单行）；


* 数组、对象最后不要有逗号。

```

// good
var a = {
  b: 1,
  c: 2
};

```

### 括号

下列关键字后必须有大括号（即使代码块的内容只有一行）：&nbsp;&nbsp;{-&nbsp;&nbsp;if&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;else&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;for&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;while&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;do&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;switch&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;try&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;catch&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;finally&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;with&nbsp;&nbsp;-}&nbsp;&nbsp;

```

// not good
if (condition) doSomething();

// good
if (condition) {
  doSomething();
}

```

### undefined

永远不要直接使用 undefined 进行变量判断；

使用 typeof 和字符串'undefined'对变量进行判断。

```

// not good
if (person === undefined) {
    ...
}

// good
if (typeof person === 'undefined') {
    ...
}

```
### 不允许存在多层嵌套的条件判断和循环（最多三层）（重点强调⭐）

条件判断能使用三目运算符和逻辑运算符解决的，就不要使用条件判断，但是**谨记不要写太长的三目运算符**。

```

// bad
if (x === 10) {
  return 'valid';
} else {
  return 'invalid';
}

// good
return x === 10 ? 'valid' : 'invalid';

// bad
if (!x) {
  if (!y) {
    x = 1;
  } else {
    x = y;
  }
}

// good
x = x || y || 1;


```
