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



for-in 语句提供了对对象内容进行操作的快捷方式。在这个遍历的过程中，我们可以干许多事情。比如——给每个属性都重新起一个名字，抛弃原来的：

```javascript
for (let i in person) {
    person["属性-" + i] = person[i];
    delete person[i];
}
```

这时再用之前的方式查看对象内容，就会看到每个属性的名字都被改变了。

```
{
属性-name: Jason
属性-age: 30
属性-sex: male
属性-job: teacher
}
```

我们还可以更进一步：为每个属性都进行编号，毕竟， for-in 语句的本质还是循环，可以做一些适合循环做的事情。

```javascript
let count = 1;
for (let i in person) {
    person[`第${count}个属性-${i}`] = person[i];
    delete person[i];
    count += 1;
}
// {
// 第1个属性-name: Jason
// 第2个属性-age: 30
// 第3个属性-sex: male
// 第4个属性-job: teacher
// }
```

要知道 for-in 语句赋予了我们随意与属性和值打交道的权力——是的，我们甚至可以*交换*属性的名称与值的位置。**当然，如果原本的值就是一个对象，我们还是不要这样做，否则会发生奇怪的事情。**

```javascript
const object = {
    name: "Andy",
    checked: true,
    anotherObj: {
        a: 1,
        b: 2
    }
};

for (let i in object) {
    let newName = object[i]; // 将原本的值存放起来
    object[newName] = i;     // 值的内容来命名一个新的属性，它的值就是原本的属性名
    delete object[i];        // 原来的属性还在，但我们不需要它了
}
```



现在我们与对象更亲近了！:-D

我们可以自由地查看、操作一个对象的情况

---

Note：我们只能遍历一个对象中的*可枚举属性*，这一概念将在后文提及。

---





