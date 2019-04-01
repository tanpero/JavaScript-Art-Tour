## for-in 和 for-of 语句

---

在 JavaScript 中， for 语句存在两种变体，分别为 *for-in 语句* 和 *for-of 语句*。它们担负的作用是循环访问一个对象中的所有成员，并将得到的值赋给一个变量。这个过程称为**遍历**。



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



