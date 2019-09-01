## JavaScript 标准对象

---

### 内置对象

### **1. 内置变量和非构造函数**

我们之前已经介绍了三个内置变量：`Infinity`，`NaN` 和 `undefined`，还有四个内置函数：`parseInt`，`parseFloat`，`isNaN`，`isFinite`。除此之外还有一些函数：

- `encodeURI` 和 `encodeURIComponent` 根据*统一资源标识符*的语法生成一段文本的编码。这些函数将在第九章介绍。
- `decodeURI` 和 `decodeURIComponent` 执行相应编码的逆操作。这些函数将在第九章介绍。
- `eval` 将一段字符串视为 JavaScript 代码并执行。如果代码是一个表达式，那么 `eval` 会求出它的值。由于必须对字符串进行编译和解释，因此 `eval` 执行的速度很慢。
- `Symbol` 得到一个 `symbol` 类型的唯一值。

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



**9. JSON**



**10. Map 和 WeakMap **



**11. Set 和 WeakSet**



**12. Proxy**







### 宿主对象





