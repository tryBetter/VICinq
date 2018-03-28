#### es6新特性概览
1. let 关键字的使用，块级作用域内有效。
2. const 声明静态常量。
3. Object.freeze() 冻结对象属性。
4. import、class 声明变量。
5. 数组解构赋值
```javascript
let [a,b,c] = [1,2,3]; // a = 1 , b = 2 , c = 3
let [x,...y] = [1,2,3,4]; // x = 1 , y = [2,3,4]
let [foo = true] = []; // 设置默认值，解构失败时使用，解构严格匹配 undefined 时属于解构失败。
```    
6. 对象解构赋值    
```javascript
let {a,b} = { a:1 , b:2 }; // a = 1 , b = 2
let { foo:a , bar:b } = { foo:5 , bar : 6}; // a = 5 , b = 6 , foo与bar都等于undefine，它们称为模式，用于匹配变量进行解构
```
`注意：解构赋值可以使用圆括号消除歧义，但要小心使用。可以使用圆括号的情况只有一种：赋值语句的非模式部分，可以使用圆括号。`
7. 解构赋值用途：    
 + 交换变量
 ```javascript
let x = 1;
let y = 2;
[x,y] = [y,x];
 ```    
 + 返回多个值    
 ```javascript
function example(){    
        return [1,2,3];
}
let [a,b,c] = example();
 ```    
 + 函数参数的定义
 + 提取json数据
 + 函数参数的默认值
 + 遍历Map结构
8. unicode使用大括号可以解读超出 FFFF 的码点
```javascript
"\uD842\uDFB7"
// "𠮷"
"\u{20BB7}"
// "𠮷"
let s = '𠮷';
s.codePointAt(0).toString(16) // "20bb7"
String.fromCodePoint(0x20BB7) // "𠮷"
```    
9. for ... of 可以遍历字符串并正确识别32位 UTF-16 字符
10. 确定一个字符串是否包含在另一个字符串中的方法：
```javascript
indexOf();
includes('',0);
startsWith('',0);
endsWith('',10);
```
11. 字符串扩展方法：
```javascript
repeat(); // 返回一个新字符串，由原字符串重复排列组成
padStart(); // 头部补全
padEnd(); // 尾部补全
```
12. 模板字符串，字符串中直接包含变量与标签。使用反引号( **`** )以及美元符号( **$** )和大括号( **{}** )，大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性，甚至调用方法。
```javascript
// 字符串中嵌入变量
let name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```
`注：使用`**trim()**`可以消除模板字符串中的空格与换行符。`
13. String.raw() 方法可以显示原始字符串（显示原始的被转义字符）。
14. 新增指数运算符 `**`
15. 函数参数可以直接设置默认值。
16. 函数参数可以使用 `...变量名` 的形式，用于获取多个参数。`...[a,b,c]`还可以将数组转化为单个参数序列。
17. 箭头函数的使用。
```javascript
let foo = x => x*x;
// 等价于
let foo = function(x){
       return x*x;
}
```
18. 数组合并与克隆可以使用扩展运算符 `...` 。
```javascript    
let a1 = [1,2];
let a2 = [...a1];// 克隆a1        
let a3 = [1,2];
let a4 = [3,4,...a3];// 合并 a3,a4
```   
19. 转化数组使用 `Array.from(任何具有length属性的对象都可以)`。`Array.of(任意数量参数)`也可以完成数组的转化。
20. `Symbol`方法可以生成唯一值。
21. `Set`数据结构，类似于数组，但不存在重复元素。可用于数组的去重。
22. `Map`数据结构，类似于普通对象，也是键值对的存储形式，但键可以是任意类型，普通对象的键只能是字符。
23. `Proxy`代理，可以实现对对象属性的预处理等操作，起到拦截作用。
24. `Reflect`反射，使对象的属性与方法访问都通过函数的方式进行操作。
25. `Promise`对象实现异步编程。
26. `iterator`遍历器可以遍历实现了 **iterator** 接口的对象。该接口主要供 **for...of** 使用。
27. `Generator`生成器，结合 **yield** 可以实现函数的暂停以及返回多个值。函数的执行需要调用 **next()** 方法，否则整个函数体都不会执行。`注：next() 方法如果有参数，那么它的值表示前一个 yield 的产出值。`
