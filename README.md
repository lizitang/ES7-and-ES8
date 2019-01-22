# ES7-and-ES8
ES7 and ES8特性
### ES7新特性
ES7在ES6的基础上添加了三项内容：<strong>求幂运算符(**)</strong>、<strong>Array.prototype.includes()</strong>方法、函数作用域中严格模式的变更。
#### Array.prototype.includes()
includes()的作用，是查找一个值在不在数组中，若在，则返回true，反之返回false。用法如下：
```js
    let arr = ['a','b','c','d'];

    arr.includes('a'); //true
    arr.includes('f'); //false
```
接收参数：
includes()接收两个参数：<strong>要搜索的值和搜索的开始索引</strong>。当第二个参数传入时，该方法会从索引处开始往后搜索(默认索引值为0)。
```js
    let arr = ['a','b','c'];
    arr.includes('b',1); //true
    arr.includes('b',2); //false
```
includes()还有一个怪异的点需要指出，在判断 +0 与 -0 时，被认为是相同的。
<strong style="color:red;">注意：</strong>includes()只能判断简单类型的数据，对于复杂类型的数据，比如对象类型的数组，二维数组，这些，是无法判断的。
### 求幂运算符(**)
### Object.entries()
`Object.entries()`方法返回一个给定对象自身可枚举属性的键值对数组，其排列与使用`for...in`循环遍历该对象时返回的顺序一致(区别在于for-in循环也枚举原型链中的属性)
#### 语法
```js
Object.entries(obj)
```
#### 参数
obj:可以返回其可枚举属性的键值对的对象
#### 返回值
给定对象自身可枚举属性的键值对数组
#### 描述
`Object.entries()`返回一个数组，其元素是与直接在object上找到的可枚举属性键值对相对应的数组。属性的顺序与通过手动循环对象的属性值所给出的顺序相同。
#### 示例
```js
const obj = {foo:'bar',baz:42};
console.log(Object.entries(obj); //[['foo','bar'],['baz',42]]

// array like object
const obj = {0:'a',1:'b',2:'c'};
console.logZ(Object.enries(obj)); //[['0','a'],['1','b'],['2','c']]

// array like object with random key ordering
const anObj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.entries(anObj)); // [ ['2', 'b'], ['7', 'c'], ['100', 'a'] ]

// getFoo is property which isn't enumerable
const myObj = Object.create({}, { getFoo: { value() { return this.foo; } } });
myObj.foo = 'bar';
console.log(Object.entries(myObj)); // [ ['foo', 'bar'] ]

// non-object argument will be coerced to an object
console.log(Object.entries('foo')); // [ ['0', 'f'], ['1', 'o'], ['2', 'o'] ]

// iterate through key-value gracefully
const obj = { a: 5, b: 7, c: 9 };
for (const [key, value] of Object.entries(obj)) {
  console.log(`${key} ${value}`);
   // "a 5", "b 7", "c 9"
}

// Or, using array extras
Object.entries(obj).forEach(([key, value]) => {
console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
});
```
### 将`Object`转换为`Map`
`new Map()` 构造函数接受一个可迭代的`entries`。借助`Object.entries`方法你可以很容易的将`Object`转换为`Map`:
```js
var obj = { foo: "bar", baz: 42 }; 
var map = new Map(Object.entries(obj));
console.log(map); // Map { foo: "bar", baz: 42 }
```
### polyfill
你可以使用下面列出的简易 polyfill。
```js
if (!Object.entries)
  Object.entries = function( obj ){
    var ownProps = Object.keys( obj ),
        i = ownProps.length,
        resArray = new Array(i); // preallocate the Array
    while (i--)
      resArray[i] = [ownProps[i], obj[ownProps[i]]];
    
    return resArray;
  };
```