## 人间烟火·Symbol 和迭代器

---

### Symbol 是什么

发布于2015年的 ECMAScript 6 标准为 JavaScript 带来了一种新的原始数据类型——Symbol。就像早已存在的 `Boolean`、`Number` 和 `String` ，JavaScript 提供了一个 `Symbol` 函数来创造新的 Symbol 类型的值。但与其他原始类型不同，`Symbol` 不是类，不能用 `new` 来创建，也没有相应的字面量形式。要想使用 Symbol 值，我们唯一的方法是直接调用 `Symbol` 函数：

```javascript
alert(Symbol());        // Symbol()
alert(typeof Symbol()); // "symbol"
alert(new Symbol());    // TypeError: Symbol is not a constructor
```

Symbol 是什么呢？

简单来说，Symbol 相当于一种*唯一标识符*，它一旦诞生，就成为独一无二的，就像枝头一片叶子长出，世界上就再也不会有另一片与它完全相同的叶子。我们可以给 Symbol 赋予一个标识，但即便是使用相同标识创建的两个 Symbol 值，它们彼此之间也是不相等的。

```javascript
let s1 = Symbol();
let s2 = Symbol();
alert(s1 === s1);       // true
alert(s1 === s2);       // false
alert(s1 === Symbol()); // false

let s3 = Symbol("love");
let s4 = Symbol("love");
alert(s3 === s4);       // false
```

Symbol 的一大用途就是：创建独一无二对象键名。就像一把指纹锁，当用一个 Symbol 值作为对象的键时，这个键所对应的值只有用同一个 Symbol 值才能访问到。

```javascript
const NAME = Symbol();
let person = {
  [NAME]: "Modi"
};

alert(person[NAME]);  // "Modi"

const AnotherNAME = Symbol();
person[AnotherNAME] = () => alert("Hello Modi");
person[AnotherNAME](); // "Hello Modi"
```





### 

