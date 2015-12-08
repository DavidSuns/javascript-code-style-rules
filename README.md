#javascript 代码规范

### 1.代码书写风格
>* 使用严格模式。

```javascript
"use strict";
```

>* 使用soft-tab（两个空格），保证代码在各种环境下显示一致。
>* 有层级结构需使用缩紧。
>* 二元运算符两侧必须有一个空格，一元运算符与操作对象之间不允许有空格。

``` javascript
var a = !arr.length;
a++;
a = b + c;
```

>* 在对象创建时，属性中的 : 之后必须有空格，: 之前不允许有空格。

``` javascript
// good
var obj = {
    a: 1,
    b: 2,
    c: 3
};

// bad
var obj = {
    a : 1,
    b:2,
    c :3
};
```

>* , 和 ; 前不允许有空格。

``` javascript
// good
callFunc(a, b);

// bad
callFunc(a , b) ;
```

>* 非特殊情况，每行不得超过 120 个字符。
>* 运算符处换行时，运算符必须在新行的行首。

``` javascript
// good
if (user.isAuthenticated()
    && user.isInRole('admin')
    && user.hasAuthority('add-admin')
    || user.hasAuthority('delete-admin')
) {
    // Code
}
```

>* 不同行为或逻辑的语句集，使用空行隔开，更易阅读。

``` javascript
function setStyle(element, property, value) {
    if (element == null) {
        return;
    }

    element.style[property] = value;
}
```

>* 不得省略语句结束的分号。
>* 函数定义结束不允许添加分号。

``` javascript
// good
function funcName() {
}

// bad
function funcName() {
};

// 如果是函数表达式，分号是不允许省略的。
var funcName = function () {
};
```

>* 适量注释。

### 2.变量声明

>* 使用var来声明变量。
>* 使用单var模式来声明变量。

``` javascript
//good
var a, b, c;

a = 1;
if(a) {
  b = 2;
  c = b + 2;
}

//bad
var a = 1;
if(a) {
  var b = 2;
  var c = b + 2;
}

```
> 使用单var模式的原因在于这样的声明方式符合js变量声明优先于语句执行的顺序，避免当在变量声明之前使用这个变量时产生的逻辑错误。
也可以提醒你不要忘记声明变量，顺便减少潜在的全局变量。书写的代码量更少。

>* 使用驼峰原则声明命名空间，变量，参数，函数。
>* 常量 使用 全部字母大写，单词间下划线分隔 的命名方式。
>* 类 使用 Pascal命名法
例:

```javascript
function HelloWorld() {}
```

>* 私有函数命名需使用 _ 开头
例：

```javascript
//private
function _calculate() {}
```

>* boolean 类型的变量使用 is 或 has 开头。
>* 函数名 使用 动宾短语
>* 类名 使用 名词。

### 3.语言特性
>* 使用严格等于和严格不等于。

```javascript
// good
if (age === 30) {
    // ......
}

// bad
if (age == 30) {
    // ......
}
```

>* 按执行频率排列分支的顺序。
>* 不要在循环体中包含函数表达式，事先将函数提取到循环体外。
>* 对循环内多次使用的不变值，在循环外用变量缓存。
>* 禁止使用for in 对数组进行遍历。
>* 禁止使用eval。
>* 禁止使用with。
>* 在使用for in 进行属性遍历的时候，需要使用hasOwnProperty做检测。

```javascript
var newInfo = {};
for (var key in info) {
    if (info.hasOwnProperty(key)) {
        newInfo[key] = info[key];
    }
}
```

>* 字符串开头和结束使用单引号 '。
解释：
输入单引号不需要按住 shift，方便输入。
实际使用中，字符串经常用来拼接 HTML。为方便 HTML 中包含双引号而不需要转义写法。

```javascript
var str = '我是一个字符串';
var html = '<div class="cls">拼接HTML可以省去双引号转义</div>';
```

>* 不允许修改和扩展任何原生对象和宿主对象的原型。

### 3.函数
>* 函数尽量保持简短。  
>* 函数参数尽量保持简短，函数参数大于3个时，应以对象形式作为参数集传递。

### 4.类
>* 属性在构造函数中声明，方法在原型中声明。

```javascript
function TextNode(value, engine) {
    this.value = value;
    this.engine = engine;
}

TextNode.prototype.clone = function () {
    return this;
};
```

>* 使用原型定义类的方法。

```javascript
function TextNode() {

}

TextNode.prototype.clone = function () {
    return this;
}

TextNode.prototype.init = function () {
    //code
}
```

## 5.jsHint

使用jsHint进行代码管理，jsHint配置文件统一为：

```javascript
{
    "jquery": true,//检查预定义的全局变量，防止出现$未定义，该项根据实际代码修改
    "bitwise": false,//不检查位运算
    "browser": true,//通过浏览器内置的全局变量检测
    "devel":true,//允许对调试用的alert和console.log的调用
    "camelcase": false,//不强制验证驼峰式命名
    "curly": true,//强制使用花括号
    "eqeqeq": false,//不强制使用===比较运算符
    "es3":true,//兼容es3规范，针对旧版浏览器编写的代码
    "esnext": false, //不使用最新的es6规范
    "expr": true,//允许未赋值的函数名表达式，例如console && console.log(1)
    "forin":false,//不强制过滤遍历对象继承的属性    
    "freeze":false,//不限制对内置对象的扩展
    "immed": true,//禁止未用括号包含立即执行函数
    "indent": false,//不强制缩进
    "latedef": true,//禁止先调用后定义
    "maxdepth":false,//不限制代码块嵌套层数
    "maxparams":false,//不限制函数参数个数
    "newcap": false,//不对首字母大写的函数强制使用new
    "noarg": false,//不禁止对arguments.caller和arguments.callee的调用
    "noempty":false,//不禁止空代码块
    "nonew":false,//允许直接new实例化而不赋值给变量
    "plusplus":false,//允许++和--运算符使用
    "quotmark": "single",//字符串使用单引号
    "scripturl": true,//允许javascript伪协议的url
    "smarttabs": true,//允许混合tab和空格缩进
    "strict": false,//不强制使用es5严格模式
    "sub": true,//允许用[]形式访问对象属性
    "undef": true,//禁止明确未定义的变量调用，如果你的变量（myvar）是在其他文件中定义的，可以使用/*global myvar */绕过检测
    "unused": false,//允许定义没用的变量，在某些函数回调中，经常出现多个参数，但不一定会用
    "multistr": false,//禁止多行字符串，改用加号连接
    "globals": {
      "jQuery": true
    }
}
```
