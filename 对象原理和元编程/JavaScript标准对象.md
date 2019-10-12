## JavaScript 标准对象

---

### 内置对象

**1. 内置变量和非构造函数**

我们之前已经介绍了三个内置变量：`Infinity`，`NaN` 和 `undefined`，还有四个内置函数：`parseInt`，`parseFloat`，`isNaN`，`isFinite`。除此之外还有一些函数：

- `encodeURI` 和 `encodeURIComponent` 根据*统一资源标识符*的语法生成一段文本的编码。这些函数将在第九章介绍。
- `decodeURI` 和 `decodeURIComponent` 执行相应编码的逆操作。这些函数将在第九章介绍。
- `eval` 将一段字符串视为 JavaScript 代码并执行。如果代码是一个表达式，那么 `eval` 会求出它的值。由于必须对字符串进行编译和解释，因此 `eval` 执行的速度很慢。

以下是 `eval` 函数的示例。

```javascript
let code = prompt("请输入一个算式");
if (/[^\d()+*/-%\s]/.test(code)) {
    alert("这不是一个算式！");
} else {
    alert(`算式的值是：${eval(code)}`);
}
```

`eval` 函数具有诸多争议，它有时被称为 evil（邪恶的）。当编程语言的某项特性很容易被错误使用，这项特性就被视为邪恶的。使用 `eval` 的唯一原因是动态地执行运行时才产生的代码，但这些代码从何而来呢？如果代码的来源不受信任，就会使应用程序有被注入恶意代码的风险，甚至破坏应用程序。

根据人们的经验，如果我们需要使用 `eval` 来解析一些东西，我们先考虑一下是否有其它替代品可以达成同样目的。一些策略是单纯地解析而不执行，例如 `JSON.parse`。如果我们必须要使用 `eval`，就要保证代码一定是安全的，没有无限循环，没有奇怪的赋值或函数调用等。在上面的示例中，我们使用正则表达式对用户输入的内容进行检查，确保文本仅包含数字、括号和几个运算符，才会调用 `eval` 来求值。我们可以在实践中思考怎样为 `eval` 创建一个安全的执行环境。



**2. Math**



**3. Object**



**4. Array**



**5. Boolean、Number 和 String**



**6. Function**



**7. Date**



**8. 错误对象**

技术上讲，我们可以使用任何东西来作为一个异常对象。甚至可以是基础类型，比如数字或者字符串。但是更好的方式是用对象，尤其是有 `name` 和 `message` 属性的对象（某种程度上和内置的异常有可比性）。
 JavaScript 有很多内置的标准异常构造器，我们也可以用它们来构造标准的异常对象。

| JavaScript 标准异常构造器 | 描述                                                |
| ------------------------- | --------------------------------------------------- |
| `Error`                   | 默认或自定义的错误。                                |
| `EvalError`               | 用错误的方式使用 `eval` 函数。                      |
| `InternalError`           | JavaScript 引擎遇到的内部错误，如：“递归嵌套太多”。 |
| `RangeError`              | 数值变量或参数超出其有效范围。                      |
| `ReferenceError`          | 无效的引用、求值过程。                              |
| `SyntaxError`             | JavaScript 引擎在解析代码时遇到的语法错误。         |
| `TypeError`               | 变量或参数不属于有效类型。                          |
| `URIError`                | 给 `encodeURI` 或 `decodeURI` 传递的参数无效。      |
 使用异常构造器的方式如下：
 ```javascript
let error = new Error(message);
// 或者
let error = new SyntaxError(message);
let error = new ReferenceError(message);
// ...
 ```
 对于内置的异常对象（不是对于其他的对象，而是对于异常对象），`name` 属性刚好是构造器的名字。`message` 则来自于参数所提供的异常信息。例如：
 ```javascript
let error = new Error("不知道发生了什么 (O_o)??");
alert(error.name);    // "Error"
alert(error.message); // "不知道发生了什么 (O_o)??"
 ```
 我们可以使用任何东西来作为一个异常对象。甚至可以是基础类型，比如数字或者字符串。但是更好的方式是用对象，尤其是有 `name` 和 `message` 属性的对象。而内置的异常构造器同时为我们设定好了异常所属的类型，因此尽量使用具体的异常构造器。如果异常不是特定的，那么可以直接用 `Error` 构造器。
 异常构造器可以通过 `new` 运算符建立新的异常对象，包含下列属性：
 - `message` —— 我们能阅读的异常提示信息。
- `name` —— 异常名称（异常对象的构造函数的名称）。
- `stack` —— 异常发生时的调用栈。
0 comments on commit b06a724



**9. JSON**



**10. Map 和 WeakMap **



**11. Set 和 WeakSet**



**12. Proxy**







### 宿主对象





