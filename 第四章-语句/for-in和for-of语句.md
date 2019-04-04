## for-in 和 for-of 语句

---

JavaScript 提供了 for 语句的两种变体用于更加灵活地实现遍历，不但能遍历数组的索引和值，也能遍历对象的成员，并将得到的值赋给一个变量。

### 属性遍历

我们可以使用 *for-in 语句*来遍历一个对象中的所有属性名称。for-in 语句的形式如下：

```javascript
for (let 变量 in 对象) {
    处理语句
}
```

for-in 语句会依次访问对象中的每个属性的名称，并将得到的字符串存放在指定的变量中，这个过程会对每一个*可遍历*的属性都执行一次。

```javascript
const person = {
    name: "Jason",
    age:  30,
    sex: "male",
    job: "teacher"
};

for (let i in person) {
    alert(i);
}
// "name"
// "age"
// "sex"
// "job"
```

有了属性名，我们也就能同时得到它的值：

```javascript
for (let i in person) {
    alert(person[i]);
}
// "Jason"
// 30
// "male"
// "teacher"
```

于是，我们可以简单地打印出一个对象的内容：

```javascript
let s = "{\n";
for (let i in person) {
    s += `${i}: ${person[i]}\n`;
}
s += "}";
alert(s);
```

结果如图所示：

![1554378154501](assets/1554378154501.png)



现在我们与对象更亲近了！

---

Note：我们只能遍历一个对象中的*可枚举属性*，这一概念将在后文提及。

---





