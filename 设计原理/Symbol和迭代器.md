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

简单来说，Symbol 相当于一种*唯一标识符*，每个 Symbol 值诞生后就是独一无二的，就像枝头一片叶子长出，世界上就再也不会有另一片与它完全相同的叶子。我们可以给 Symbol 赋予一个标识，但即便是使用相同标识创建的两个 Symbol 值，它们彼此之间也是不相等的。

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

Symbol 的一大用途就是：创建独一无二的对象键名。就像一把指纹锁，当用一个 Symbol 值作为对象的键时，这个键所对应的值只有用同一个 Symbol 值才能访问到。

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





### 迭代协议

Symbol 值本身带来的意义几乎只是为 JavaScript 增加了一种“创建唯一无二的值”的方式，但是，用于构造 Symbol 值的 `Symbol` 函数，其本身的用途却不仅仅是构造 Symbol 值这么简单。事实上，JavaScript 中许多原本保留的内部细节，都通过 `Symbol` 的一批属性暴露给了我们，这使得 `Symbol ` 包含一组非常强大的工具，能帮助我们在探究 JavaScript 的语言构造和内部设计上如虎添翼。

ECMAScript 标准定义了一批用来在语言内部实现某些特性的属性，这些属性以前缀 `@@` 标记，在 ECMAScript 6 以前，它们是无法被我们直接访问到的。一个例子是`@@iterator` 方法，它会使对象成为*可迭代对象*。当需要对一个对象进行迭代时（例如在 `for...of` 语句中），它的 `@@iterator` 方法会在不传参情况下被调用，并返回一个迭代器，这个迭代器提供每次迭代所需要的值。

一些内置类拥有默认的 `@@iterator` 方法，以展现出可供迭代的性质，例如 `Array`、`String` 等，而其他类（如 `Object`）则没有。

`@@iterator` 方法代表 JavaScript 中的*可迭代协议*，凡是实现了正确的 `@@iterator` 方法的对象，就符合可迭代协议，那么这个对象就是*可迭代的*。可迭代协议允许 JavaScript 对象去定义或定制它们的迭代行为，例如在 `for...of` 语句中被遍历时，有什么值会被访问到。可迭代对象就是符合迭代协议、能够展现出正确的迭代行为的对象，它们必然拥有 `@@iterator` 。

来整理一下这些术语的关系：**一些对象拥有定义正确的 `@@iterator` 内部方法，它们符合可迭代协议，是可迭代对象。它们的 `@@iterator` 方法实际上是迭代器函数，它返回一个迭代器，每次迭代时会自动得到一个值。**

为了在每次迭代时提供一个新值, `@@iterator` 方法可以被实现为一个**生成器函数**。我们不能直接访问 `@@iterator` 这样的内部方法，但是可以通过 **`Symbol.iterator`** 访问到。因此，我们可以像这样定义一个最简单的可迭代对象。

```javascript
let it = {
    *[Symbol.iterator]() {
        yield 1;
        yield 2;
        yield 3;
    }
};
```

我们看到， `it` 已经定义了正确的 `@@iterator` 方法，它现在是一个符合迭代协议的可迭代对象了。一些 JavaScript 的语法特性，在语义上只对序列有效，这就要求某个对象必须是符合可迭代协议的，例如序列展开运算符 `...`、`for...of` 语句等。来看看我们的对象能否得到认可：

```javascript
alert([...it]); // 1,2,3
for (let i of it) {
    alert(i);
}
// 1
// 2
// 3
```

成功了！总的来说，这些语法特性依赖可迭代协议。

那么，如果一个对象实现了 `@@iterator` ，却不符合可迭代协议，会怎样呢？

```javascript
let fakeIt = {
    [Symbol.iterator] () {
        return "Hello";
    }
};
[...fakeIt]; // TypeError: Result of the Symbol.iterator method is not an object
```

上文中说 `@@iterator` 方法是一个迭代器函数，又说它必须被实现为一个生成器函数。那么，这些名词究竟有什么关系呢？它们的逻辑关系可以描述如下：

- 生成器函数是函数，它调用后返回一个对象，这个对象是生成器。
- 迭代器函数是函数，它调用后返回一个对象，这个对象是迭代器。
- 生成器是迭代器的一种。

这里似乎令人一头雾水，因为我们还没有了解**迭代器**的概念。

简单来说，迭代器定义一个序列，它拥有 `next` 方法，每次调用 `next` 方法，意味着从序列中获取了下一个值。它返回一个对象，包含两个属性。

- `value`，它代表本次迭代所产生的值，这个值来自预定义的序列。
- `done`，如果它为 `true`，代表这个序列已经终结，不再进行迭代。如果它为 `false`，迭代还未技术，这个序列还会继续产生新值。

一个迭代器对象完成迭代过程后，我们说它被*消耗*了。在它产生序列中的最后一个值之后，`done` 方法应当被设为 `true`。

数组是最常见的序列，它本身也包含一个迭代器，即 `@@iterator`方法，这个迭代器可以依次返回数组中的每个成员。显然，因为把 `@@iterator` 定义为迭代器，所以数组本身是可迭代对象。

下面实现了一个简单的迭代器函数，它构造一个可以代表无穷序列的迭代器。

```javascript
const makeIterator = (start = 0, end = Infinity, step = 1) => {
    let nextIndex = start;
    let count = 0;
    
    return {
       next() {
           let result;
           if (nextIndex < end) {
               result = { value: nextIndex, done: false }
               nextIndex += step;
               count += 1;
               return result;
           }
           return { value: count, done: true }
       }
    };
};
```

测试一下：

```javascript
let it = makeIterator(1, 5); // 这个迭代器代表 1 ≤ n < 5 的正整数序列
it.next(); // { value: 1, done: false}
it.next(); // { value: 2, done: false}
it.next(); // { value: 3, done: false}
it.next(); // { value: 4, done: false}
it.next(); // { value: 4, done: true}
```



---

Note：

注意：可迭代协议和迭代器协议是两个容易混淆的不同概念。

- 迭代器协议要求对象拥有 `next` 方法，使一个对象可以预定义一个序列，并且每次迭代时按顺序提供序列的值。这种对象叫**迭代器**。
- 可迭代协议要求对象拥有 `@@iterator` 方法，这个方法应当是一个迭代器，它从外观上呈现为一个序列，实际上是还原了迭代器所定义的序列。**这个对象是可迭代对象。**

迭代器和可迭代对象的关系可以描述为发动机和汽车。可迭代对象像汽车，可以在道路上行使，但真正驱动它的是迭代器这台发动机。

可迭代协议和迭代器协议统称为迭代协议。

---



我们也可以把 `makeIterator` 作为一个另一个对象的 `@@iterator` 方法，构造一个新的可迭代对象：

```javascript
let happyObject = {
    // 不能直接把 makeIterator 作为 @@iterator 的值，因为这样会构造无穷序列
    [Symbol.iterator]: () => makeIterator(1, 10)
};

alert([...happyObject]); // 1,2,3,4,5,6,7,8,9
```

我们看到，只要对象有一个符合迭代器协议的`@@iterator` 方法，它本身就符合可迭代协议，成为可迭代对象。这样就可以回答前面的问题了：生成器函数是 JavaScript 内置的一种默认迭代器函数，它可以便捷地提供可迭代对象所需要的序列。其实一个对象既可以是可迭代对象，又可以是迭代器，要做到这点十分容易。

用一个更进一步的例子来结束有关迭代协议的内容，这个例子会构造一段序列，包含 $ 1 \le n \lt 40 $ 的所有奇数。

```javascript
// 建立一个迭代器函数
const oggIterator = () => {
    let nextIndex = 1;
    let count = 0;
    
    return {
       next() {
           let result = { value: count, done: true };
           if (nextIndex < 40) {
               result = { value: nextIndex, done: false }
               nextIndex += step;
               count += 2;
               return result;
           }
           return result;
       };
    };
};

// 进一步构造成可迭代对象
let oggObject = {
    [Symbol.iterator]: oggIterator
};
alert([...oggIterator]);
// 1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39
```



---

练习 7.4.2

1. 编写一个构造完全平方数序列的迭代器，上限自定。
2. 利用上一个练习中的迭代器，编写一个可迭代对象，将其构造为数组。

---