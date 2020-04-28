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

## Vue规范

### 目录、文件、组件命名规范

##### 1. 目录

目录统一使用&nbsp;&nbsp;{-&nbsp;&nbsp;kebab-case&nbsp;&nbsp;-}&nbsp;&nbsp;风格

##### 2. views下的文件


* js类文件使用&nbsp;&nbsp;{-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}&nbsp;&nbsp;，如&nbsp;&nbsp;{-&nbsp;&nbsp;UserInfo.js&nbsp;&nbsp;-}&nbsp;&nbsp;


* 其他资源文件统一使用&nbsp;&nbsp;{-&nbsp;&nbsp;kebab-case&nbsp;&nbsp;-}&nbsp;&nbsp;风格，如&nbsp;&nbsp;{-&nbsp;&nbsp;user-detail.js&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;user-detail.css&nbsp;&nbsp;-}&nbsp;&nbsp;, &nbsp;&nbsp;{-&nbsp;&nbsp;user-avatar.png&nbsp;&nbsp;-}&nbsp;&nbsp;


##### 3. 组件文件

* 命名遵循&nbsp;&nbsp;{-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}&nbsp;&nbsp;约定。组件文件名除&nbsp;&nbsp;{-&nbsp;&nbsp;index.vue&nbsp;&nbsp;-}&nbsp;&nbsp;之外，一律采用&nbsp;&nbsp;{-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}&nbsp;&nbsp;(大驼峰)写法。原因是引入组件时，组件的变量通常用&nbsp;&nbsp;{-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}&nbsp;&nbsp;格式，以区别于一般变量。组件文件名与变量名一致，方便对应。


```

import UserBook from './user/UserBook'


```

* 组件名应该始终是多个单词的，根组件 App 除外 html元素都是单个单词的（如&nbsp;&nbsp;{-&nbsp;&nbsp; < article > &nbsp;&nbsp;-}&nbsp;&nbsp;,&nbsp;&nbsp;{-&nbsp;&nbsp; < header > &nbsp;&nbsp;-}&nbsp;&nbsp;)，为了区分组件和一般&nbsp;&nbsp;{-&nbsp;&nbsp;html&nbsp;&nbsp;-}&nbsp;&nbsp;元素，组件由多个单词组成，如&nbsp;&nbsp;{-&nbsp;&nbsp;BookItem.vue&nbsp;&nbsp;-}&nbsp;&nbsp;，单独的&nbsp;&nbsp;{-&nbsp;&nbsp;Book.vue&nbsp;&nbsp;-}&nbsp;&nbsp;不推荐。


* 组件使用遵循&nbsp;&nbsp;{-&nbsp;&nbsp;kebab-case&nbsp;&nbsp;-}&nbsp;&nbsp; 约定 在页面中使用组件需要前后闭合，并以短线分隔，如：

```
<user-book></user-book>

<user-book />

```

### 开发规范

##### 文件结构

* **基本结构**

顺序：&nbsp;&nbsp;{-&nbsp;&nbsp;template&nbsp;&nbsp;-}&nbsp;&nbsp; -> &nbsp;&nbsp;{-&nbsp;&nbsp;script&nbsp;&nbsp;-}&nbsp;&nbsp; -> &nbsp;&nbsp;{-&nbsp;&nbsp;style&nbsp;&nbsp;-}&nbsp;&nbsp;。一个组件尽量不要超过**200**行，页面包含独立部分时尽量分离成子组件。**页面应该由各个小组件组成**

```

<template>
  <div>
    <component-a />
    <component-b />
    <component-c />
  </div>
</template>
<script>
  export default {
    components: {},
    data() {
      return {};
    },
    created(){},
    methods: {},
  };
</script>
<!-- 声明语言，并且添加scoped -->
<style lang="scss" scoped>...</style>


```

* **组件/实例的选项顺序**

```

- name          (全局引用)
- components    (模板依赖)
- directives    ...
- filters       ...
- mixins        (组合)
- props         (接口)
- data          (本地状态属性)
- computed      ...
- watch         (响应回调)
- created       (生命周期函数)
- mounted       ...
- methods       (实例属性)


```

### Vue Router 规范

* **router path**采用&nbsp;&nbsp;{-&nbsp;&nbsp;kebab-case&nbsp;&nbsp;-}&nbsp;&nbsp;格式。


> 用下划线（如：&nbsp;&nbsp;{-&nbsp;&nbsp;/user_info&nbsp;&nbsp;-}&nbsp;&nbsp;）或&nbsp;&nbsp;{-&nbsp;&nbsp;camelCase&nbsp;&nbsp;-}&nbsp;&nbsp;（如：&nbsp;&nbsp;{-&nbsp;&nbsp;/userInfo&nbsp;&nbsp;-}&nbsp;&nbsp;)的单词被当成一个单词，搜索引擎无法区分语义。


* **router name**采用&nbsp;&nbsp;{-&nbsp;&nbsp;kebabCase&nbsp;&nbsp;-}&nbsp;&nbsp;格式。

```

// bad
{
    path: '/user_info', // user_info当成一个单词
    name: 'UserInfo',
    component: UserInfo,
    meta: {
    title: ' - 用户',
    desc: ''
    }
},

// good
{
    path: '/user-info', // 能解析成user info
    name: 'UserInfo',
    component: UserInfo,
    meta: {
    title: ' - 用户',
    desc: ''
}

```

### 组件开发规范

##### 1. 注册组件

注册组件的时候，全部使用 &nbsp;&nbsp;{-&nbsp;&nbsp;PascalCase&nbsp;&nbsp;-}&nbsp;&nbsp; 格式。

```

import UserBook from './user/UserBook'

```
##### 2. props 命名规范

在声明&nbsp;&nbsp;{-&nbsp;&nbsp;prop&nbsp;&nbsp;-}&nbsp;&nbsp;的时候，其命名应该始终使用&nbsp;&nbsp;{-&nbsp;&nbsp;camelCase&nbsp;&nbsp;-}&nbsp;&nbsp;，而在模板中应该始终使用&nbsp;&nbsp;{-&nbsp;&nbsp;kebab-case&nbsp;&nbsp;-}&nbsp;&nbsp;

```

<welcome-message greeting-text="hi"></welcome-message>

<script>
  props: {
    greetingText: String;
  }
</script>

```

* **prop定义应该尽量详细**

    **1.申明类型type（必填）**

    **2.提供默认值（必填)**
    
    **3.校验类型(可选)**

```

// bad 这样做只有开发原型系统时可以接受
props: ['status']

// good
props: {
 status: {
   type: String,
   required: true,
   default: ''
   }
 }
}

```
### methods 命名规范

* **驼峰式命名&nbsp;&nbsp;{-&nbsp;&nbsp;camelCase&nbsp;&nbsp;-}&nbsp;&nbsp;，操作性函数统一使用动词或者动词+名词形式**

```

jumpPage() {

}

openCarInfoDialog () {
    
}

```

* **请求数据方法，以 data 结尾**

```

getListData () {
 
}

postFormData () {
    
}

```

**注**: 尽量使用常用单词开头（set、get、go、can、has、is）


**附**： 函数方法常用的动词:

```

get 获取/set 设置,
add 增加/remove 删除
create 创建/destory 移除
start 启动/stop 停止
open 打开/close 关闭,
read 读取/write 写入
load 载入/save 保存,
create 创建/destroy 销毁
begin 开始/end 结束,
backup 备份/restore 恢复
import 导入/export 导出,
split 分割/merge 合并
inject 注入/extract 提取,
attach 附着/detach 脱离
bind 绑定/separate 分离,
view 查看/browse 浏览
edit 编辑/modify 修改,
select 选取/mark 标记
copy 复制/paste 粘贴,
undo 撤销/redo 重做
insert 插入/delete 移除,
add 加入/append 添加
clean 清理/clear 清除,
index 索引/sort 排序
find 查找/search 搜索,
increase 增加/decrease 减少
play 播放/pause 暂停,
launch 启动/run 运行
compile 编译/execute 执行,
debug 调试/trace 跟踪
observe 观察/listen 监听,
build 构建/publish 发布
input 输入/output 输出,
encode 编码/decode 解码
encrypt 加密/decrypt 解密,
compress 压缩/decompress 解压缩
pack 打包/unpack 解包,
parse 解析/emit 生成
connect 连接/disconnect 断开,
send 发送/receive 接收
download 下载/upload 上传,
refresh 刷新/synchronize 同步
update 更新/revert 复原,
lock 锁定/unlock 解锁
check out 签出/check in 签入,
submit 提交/commit 交付
push 推/pull 拉,
expand 展开/collapse 折叠
begin 起始/end 结束,
start 开始/finish 完成
enter 进入/exit 退出,
abort 放弃/quit 离开
obsolete 废弃/depreciate 废旧,
collect 收集/aggregate 聚集

```

### 多个属性的标签元素规范


```

<!-- bad -->
<img src="https://user-gold-cdn.xitu.io/2020/4/27/171bab9e9687bb00?w=400&h=400&f=png&s=3451" alt="Vue Logo">
<my-component foo="fooattribute" bar="barattribute" baz="bazattribute"></my-component>

<!-- good -->
<img
  src="https://user-gold-cdn.xitu.io/2020/4/27/171bab9e9687bb00?w=400&h=400&f=png&s=3451"
  alt="Vue Logo"
>
<my-component
  foo="fooattribute"
  bar="barattribute"
  baz="bazattribute"
>
</my-component>

```

### 元素属性的顺序

原生属性放前面，指令放后面


```

  - class
  - id,ref
  - name
  - data-*
  - src, for, type, href,value,max-length,max,min,pattern
  - title, alt，placeholder
  - aria-*, role
  - required,readonly,disabled
  - is
  - v-for
  - key
  - v-if
  - v-else-if
  - v-else
  - v-show
  - v-cloak
  - v-pre
  - v-once
  - v-model
  - v-bind,:
  - v-on,@
  - v-html
  - v-text
  
```

### 指令规范

指令有缩写则一律采用缩写形式

```
// bad
v-bind:code="code"
v-on:click="getUserData"

// good
:code="code"
@click="getUserData"

```

v-for 循环必须加上 key 属性，在整个 for 循环中 key 需要唯一，添加key可提高性能

```

<!-- bad -->
<ul>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
</ul>

<!-- good -->
<ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
    </li>
</ul>

```

* 避免 v-if 和 v-for 同时用在一个元素上（性能问题）


出现这样的需求，有两种解决方案：

1.将数据替换为一个计算属性，让其返回过滤后的列表

```

 <!-- bad -->
  <ul>
    <li v-for="user in users" v-if="user.isActive" :key="user.id">
      {{ user.name }}
    </li>
  </ul>

  <!-- good -->
  <ul>
    <li v-for="user in activeUsers" :key="user.id">
      {{ user.name }}
    </li>
  </ul>

  <script>
  computed: {
    activeUsers: function () {
      return this.users.filter(function (user) {
        return user.isActive
      })
    }
  }
  </script>

```

2.将 v-if 移动至容器元素上 (比如 ul, ol)

```
  <!-- bad -->
  <ul>
    <li v-for="user in users" v-if="shouldShowUsers" :key="user.id">
      {{ user.name }}
    </li>
  </ul>

  <!-- good -->
  <ul v-if="shouldShowUsers">
    <li v-for="user in users" :key="user.id">
      {{ user.name }}
    </li>
  </ul>

```