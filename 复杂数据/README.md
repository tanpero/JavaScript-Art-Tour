# 复杂数据

---





## 道生万物·对象

------

### 对象的概念

**构造器与字面量**

*字面量*是一种值的表示法。通过直接写出一个值所包含的内容，来创建这个值，这种**形式**被称为字面量。

如："Hello world" 就是一个字符串字面量，1234.5678 就是一个数字字面量。

字面量与*创建实例*相对。在 JavaScript 中，每种类型的值都有一个对应的*构造器*，原则上你可以使用构造器来构造一个值，构造器写成函数调用的形式，可以接受一些值，作为创建新值的所需信息，这种创建值的形式称为*创建实例*。如：

```javascript
const a = new Number();    // a = 0
const b = new Number(10);  // b = 10
const c = new String();    // c = ""
const d = new String(100); // c = "100"
```

当然，JavaScript 中提供了方便的*字面量*方式来让我们创建值，我们不需要为值一个个创建实例。

除了我们已经了解过的布尔值、数值、字符串之外，有一大类值被称为*对象*。对象是一个包含了一些值的结构。

```javascript
const o = new Object();
o.name = "John";
o.age = 12;
```

现在我们创建了一个对象，并将它赋给常量 `o` 。我们为 `o` 提供了两个信息，分别是名称和年龄。这个信息被称作*属性*，我们可以通过属性来访问对象中所存放的具体的值。

```javascript
const cat = new Object();
cat.name = "Lily";
cat.age  = 3;
alert(cat.age); // 3
```

我们赋予了这个“猫对象”两个属性，一个是它的名字，一个是年龄。每个属性都对应一个值。当我们需要改变或得到某个属性的值时，我们只需要写下 `<对象名>.<属性名>` 即可。你可以把它当做一个对象内部的变量。

如果访问了未设置值的属性，你会得到值 `undefined` ，——因为“未定义”啊！

和基本的值一样，对象也可以用简便的字面量方式创建，这种形式被称为*对象字面量*。

它的特征是一对大括号，标志着这个对象字面量的起始与结束。在大括号中你可以写下一个属性和一个值，二者用冒号分隔，值后面写一个逗号，表示这一项*成员*结束了。

```javascript
const dog = {name: "Peter", age: 4};
alert(dog.name); // "Peter"
```

现在我们拥有了一只小狗，并给它起了名字。我们可以利用合适的换行，让对象字面量看起来舒服一些：

```javascript
const dog = {
    name: "Peter",
    age: 4,
};
alert(dog.name); // "Peter"
```

最后一项成员的逗号是可选的，你可以自由决定是否添加。

我们可以重复定义对象中的一个属性，最后一次定义的值会覆盖掉先前的值。但是我们没必要这样做，如果要改变一个属性的值，随时可以通过访问它的方式来改变。

```javascript
// 不要这样做
const object = {
    a: 1,
    a: 2
};
alert(object.a); // 2

// 你可以像这样
const object2 = {
    a: 1
};
object2.a = 2;
alert(object2.a); // 2
```

对象字面量中所包含的信息构成了这个对象本身，自身也是值，因此你可以在对象字面量中将一个属性的值设置为另一个对象字面量。当一个对象成为属性的值时，你可以通过属性访问这个对象，进一步访问它的属性只需要在它后面接着写 `.<属性名>`即可。这种访问属性的方式被称为*点号访问法。*

```javascript
const person = {
    name: "Venn",
    age: 18,
    foods: {
        apple: 5,
        pear: 3
    }
};
alert(person.name); // Venn
alert(person.foods.apple); // 5
```

当然，你不能直接查看一个对象，否则你会得到一个看起来有些奇怪的字符串值：

```javascript
alert(person);       // "[object Object]"
alert(person.foods); // "[object Object]"
```



**属性名**

如前文所说，对象的属性名可以看做是一个变量名，一个合法的标识符也可以直接用做属性名。但事实上，你可以用**任何字符**作为属性名，包括空格等。你只需要用双引号或单引号将属性名括起：

```javascript
const person = {
    "first name": "John",
    "last name": "Doe",
};
```

然后，可以这样访问属性值：

```javascript
alert(person["first name"]); // John
alert(person["last name"]);  // Doe
```

这种方法被称为*方括号访问法*。如果属性名是合法的标识符，你也可以写成完全等价的点号访问法的形式。

```javascript
const o = {
    "aaa": "bbb"
};
alert(o["aaa"]); // "bbb"
alert(o.aaa);    // "bbb"
```



------

练习 3.4.1

1. 编写一个程序，提示用户输入一些个人信息，并将它存储到一个对象里。
2. 在 3.4.1.1 的基础上，从对象中访问某个信息，并告诉用户某个它的值。

------





### 成员操作

JavaScript 提供了一些方式来操作对象中的属性和值。我们已经讨论了访问和修改成员值的方式，添加一个成员也很简单——就像修改它一样，直接赋值即可。

```javascript
const cat = {
    name: "Kitty",
    age: 4,
    kind: "unknown"
};

// 现在我知道它是波斯猫
cat.kind = "Persian cat";
alert(cat.kind); // "Persian cat"
```

你也可以删除对象中的属性，JavaScript 提供了 `delete` 操作符。

```javascript
const cat = {
    name: "Kitty",
    age: 4,
    kind: "unknown"
};

// 现在我不需要关心它的品种
delete cat.kind;
alert(cat.kind); // undefined
```

这时候我们或许会有疑问：当一个属性被删除之后，再访问它就会得到 `undefined`。那么这跟直接把属性的值设为 `undefined` 有什么区别吗？

当然有！当属性值为 `undefined` 时，它只是一个值为 `undefined` 的属性，依然存在于对象中。但是，当你用 `delete` 删除一个属性的时候，这个对象中就不存在这个属性了，只不过是访问了不存在的属性会得到 `undefined` 而已。

你可以使用 `in` 操作符来查看对象中究竟是否存在某一个属性：

```javascript
const cat = {
    name: "Kitty",
    age: 4,
    kind: "unknown"
};

// 现在我不需要关心它的品种
delete cat.kind;
alert("kind" in cat); // false
alert("name" in cat); // true
```

为什么当我们查看某个属性是否存在时，这个属性名要写成字符串？这是因为在 JavaScript 的语法中，如果直接写成 `kind in cat` 这样，`kind` 会被理解为一个标识符，然而我们并没有定义这个标识符，因此会得到一个错误。

事实上，JavaScript 中的对象的属性名都是以字符串方式存储的，只不过在对象字面量中，如果是合法的标识符，就不需要写成字符串的形式，JavaScript 会理解它。如果是点号标记法，由于它**只能用于访问写成合法标识符的属性名称**，因此属性名也不需要写成字符串的形式。但是在中括号标记法中，就应该写成字符串的形式。因为 JavaScript 会**将中括号中的内容当做表达式进行求值**，如果是一个字符串，那么就是按这个字符串对应的属性名进行访问，而如果认为是一个标识符，就会查找这个标识符本身的值所对应的属性名。

下面用一个示例来说明。

```javascript
let a = "123";
const object = {
    a: 456,
    "123": 123
};
alert(object.a);    // 456
alert(object[a]);   // 123（标识符 a 的值是 "123"，那么访问了名为 "123" 的属性）
alert(object["a"]); // 456（访问名为"a"的属性）
```



------

练习 3.4.2

1. 在 3.4.1.1 的基础上，提示用户输入一个名称，告诉用户这个对象中是否能找到名称对应的值。

   （提示：使用前面学习的逻辑相关知识）

------





### 枚举

上文所提供的访问对象成员的方式，都是通过属性名进行的。假如我们不知道某个属性的名称，或者说想一次性访问到所有的值，JavaScript 也提供了一些方便的函数来进行这类操作。

第一个是 `Object.values` 函数。我们可以从它得到一个列表，列表中会依次存放它所有的值。由于我们可以直接显示数组中的内容，因此它的所有值也就一目了然。

```javascript
const cat = {
    name: "Kitty",
    age: 4,
    kind: "Cheshire Cat"
};

const values = Object.values(cat);
alert(values); // Kitty,4,Cheshire Cat
```

第二个是 `Object.keys` 函数，它得到一个对象中所有属性名称的列表。

```javascript
const cat = {
    name: "Kitty",
    age: 4,
    kind: "Cheshire Cat"
};

const keys = Object.keys(cat);
alert(keys); // name,age,kind
```

此外，我们还可以使用 `Object.entries` 函数，它同样是得到一个列表，列表中交替保存属性名和值。

```javascript
const cat = {
    name: "Kitty",
    age: 4,
    kind: "Cheshire Cat"
};

const entries = Object.entries(cat);
alert(entries); // name,Kitty,age,4,kind,Cheshire Cat
```

我们会在下一节中详细了解如何使用列表中的值。





### 全局对象

我们在这里需要明确一个之前没有提及的概念：

> 在 JavaScript 中，所有变量和常量都是一个*全局对象*的属性。

这个全局对象叫 `window` 。它在语义上指浏览器的窗口对象，同时也是 JavaScript 运行环境的一个“兜底”对象。当我们访问 `window` 对象的属性的时候，我们实际上是在访问这样一个变量/常量。

```javascript
let hello = "Hello world";
alert(window.hello);          // "Hello world"
alert(window.hello === hello); // true
```

由于 `window` 自身也是一个变量，因此它也是它自己的属性。

```javascript
alert(window === window.window);               // true
alert(window.window === window.window.window); // true
```

一般情况下我们不需要直接使用 `window` 对象，不过我们可以使用它来判断一个标识符是否存在于当前环境中——换句话说，只要知道 `window` 对象是否有这个 A 属性，就可以是否声明过一个叫 A 的标识符。

------

练习 3.4.3

1. 编写一个程序，判断当前环境中是否存在一个变量或常量。

2. 编写一个程序，在 3.4.3.1 的基础上判断某个标识符是否为变量或常量。

   （提示：`window` 对象的属性值可改变）

------









## 时空列车·数组

------

### 初探数组

我们已经学习了 JavaScript 中的对象的概念。假如我们想表示教室里一排学生的座次，我们或许可以用对象字面量这样写：

```javascript
let seating = {
    "1": "Mason Mills",
    "2": "Rachel Griffiths",
    "3": "Melissa Duncan",
    "4": "Marley Hughes",
    "5": "Charlie Henderson",
    "6": "Brandon Sharp",
    "7": "Morgan Woods",
    "8": "Maddox Andrews",
    "9": "Lexie Jefferson",
    "10": "Estelle Bolton"    
};

alert(seating["5"]); // "Charlie Henderson"
alert(seating["9"]); // "Estelle Bolton"
```

然后，我们可以使用中括号访问法访问某个具体的序号上的学生姓名。但是这样显然非常不方便：

- 每增加一个学生，就要手动安排一个序号；
- 如果我们要将一个学生移到别的位置，将会非常糟糕：我们要把从这里到那里所有的学生重新排一遍序号。
- 我们不能方便地获取到已经加入到这个列表中的学生数量。

所幸，JavaScript 为我们提供了另外一种结构可以避免上面说的问题，它就是**数组**。

我们只需在数组中写下学生姓名，而无需被序号和获取学生数量等问题所困扰，数组为我们搞定了这一切。你可以这样构造一个数组：

```javascript
let seating = ["Mason Mills", "Rachel Griffiths", "Melissa Duncan", "Marley Hughes", "Charlie Henderson", "Brandon Sharp", "Morgan Woods", "Maddox Andrews", "Lexie Jefferson", "Estelle Bolton"]；
```

你猜对了！这种构造形式被称为*数组字面量*。一对中括号 `[]` 标志着数组字面量的开始与结束，中括号之间的每一项都是数组的一个*成员*，或者叫*元素*。这两种称呼是等价的，本书中会交替出现这两个名词。

我们依然可以通过中括号访问法访问数组元素，不同的是，这里不用写成字符串的形式，我们只需要使用数字来访问进行访问，这种访问方式称为*下标访问法*，每个元素的唯一序号称为*下标*。下标是从 `0` 开始的，换句话说，第一个元素下标为 `0`，第二个为 `1` ，第三个为 `2`……以此类推，第 n 个元素下标为 `n-1` 。如果数组中找不到指定下标的元素，就会得到一个 `undefined`。

```javascript
// 不要写成这样;
let student = seating["3"];
alert(student); // "Melissa Duncan"

// 只需要这样：
let student = seating[2];
alert(student); // "Melissa Duncan"

// 找不到指定下标的元素的例子：
alert(seating[100]); // undefined
```

如果要移动某个元素的位置，你只需要在构造时将它写在你需要的位置即可。你还可以使用 `length ` 属性来获取数组的长度（即所包含元素的数量）。由于第 `n` 个元素的下标是 `n-1`，因此数组中最后一个元素的下标是 `length` 值减一。

```javascript
// const seating = ["Mason Mills", "Rachel Griffiths", "Melissa Duncan", "Marley Hughes", "Charlie Henderson", "Brandon Sharp", "Morgan Woods", "Maddox Andrews", "Lexie Jefferson", "Estelle Bolton"]；
// Morgan Woods 上课会跟 Maddox Andrews 说话，把他挪到第二排吧！
let seating = ["Mason Mills", "Morgan Woods", "Rachel Griffiths", "Melissa Duncan", "Marley Hughes", "Charlie Henderson", "Brandon Sharp", "Maddox Andrews", "Lexie Jefferson", "Estelle Bolton"]；

alert(seating.length);              // 10
alert(seating[0]);                  // "Mason Mills"
alert(seating[1]);                  // "Morgan Woods"
alert(seating[seating.length - 1]); // "Estelle Bolton"
alert(seating[seating.length]);     // undefined （超出了数组边界）
```

就像我们更改一个对象的属性一样，我们也可以用类似的方式更改数组的元素值，只要知道它的下标即可：

```javascript
alert(seating[0]); // Mason Mills 被点名了
seating[0] = "Anchimolios"; // 这个位置坐了一个古希腊人！
alert(seating[0]); // 现在报上名字的是 Anchimolios
```

可怜的 Mason Mills！他的位置被一个我们都不认识的古希腊人给占了。不过我们不需要为他感到难过，我们会在下文学到如何在不剥夺任何一个学生座位的情况下安排新的学生进入这里。

现在，我们知道这一列有十个学生，但是今天很巧，坐在第四、第五位的 "Melissa Duncan、Marley Hughes 都没来上课，我们可以给他们留两个空位：

```javascript
let seating = ["Anchimolios", "Morgan Woods", "Rachel Griffiths", , , "Charlie Henderson", "Brandon Sharp", "Maddox Andrews", "Lexie Jefferson", "Estelle Bolton"]；
```

老师开始点人数了！坐在第一个的是 Anchimolios……咦，是谁坐在第四、第五个来着？老师没看到人，就想不起来他们的名字，只能用 `undefined` 来表示自己的无奈。

```javascript
alert(seating[2]); // "Rachel Griffiths"
alert(seating[3]); // undefined
alert(seating[4]); // undefined
```

几分钟后，Melissa Duncan 和 Marley Hughes 气喘吁吁地赶回了他们的座位上，老师终于想起了他们的名字。

```javascript
seating[3] = "Marley Hughes";
seating[4] = "Melissa Duncan";
```

等等……好像有点不对！这两人的位置是不是坐反了？我们记得 Melissa Duncan 明明坐在 Marley Hughes 的前面！老师发现了这个问题，现在要求他们互换座位。于是 Marley Hughes 先腾出了座位，等 Melissa Duncan 从原本属于他的位置上起来，好坐回去。

```javascript
let temp = seating[3];
seating[3] = seating[4];
seating[4] = temp;
```

Marley Hughes 站起来，站到了一个临时（temp）位置，于是 Melissa Duncan 一步到位，坐到了第四桌，Marley Hughes 终于也回到了他的位置上。但是，这两个小伙子不仅迟到，还搞出了这么些名堂，于是，**他们被老师记住了！**（默哀一秒钟）

现在终于开始正式上课了，同学们开始聚精会神地听讲，只见老师在黑板上写下了 “`Array` 构造器“几个大字，同学们似乎想起了什么……



------

note：还记得在上一节中提到的 `Object.values`、 `Object.keys` 和 `Object.entries` 吗？它们都会得到数组。如果不记得的话，可以回去看一看。

------





### Array 构造器

在 JavaScript 中，每种类型的值都具有一个*构造器*，数组也不例外。它是一类称为 `array`  的值。我们已经见到了 `number` 类型（数字）的构造器 `Number`，`string` 类型（字符串）的构造器 `String`，还有 `object` 类型（对象）的构造器 `Object`。那么数组——这类称为 `array` 类型的值，它的构造器自然叫 `Array`。虽然我们总是用字面量方式创建这些值，但是了解它们的构造器也是很有必要的。

我们可以创建一个构造器的**实例**，在前文中这种形式就叫做创建实例，但是现在我们要冠以一个更准确的术语：实例化。例如，当我们写下 `const o = new Object();` 的时候，我们实例化了 `Object` 构造器，得到了一个对象。我们也可以如法炮制，实例化 `Array` 构造器：

```javascript
let a = new Array();
```

它创建了一个*空数组*，与这种字面量形式是等价的：

```javascript
let a = [];
```

如果我们知道数组应该有多少元素（例如：我们知道有多少学生坐在同一列），可以在实例化 `Array` 构造器时附加一个数据，以表示创建一个包含这么多元素的数组：

```javascript
let a = new Array(10);
alert(a.length); // 10

// 相当于
let a = [ , , , , , , , , , ]; // 嘿，怎么搞的，今天一个人都没回来？
```

趁着老师发出怒吼之前，我们赶紧往下看！

我们也可以把需要包含的元素写在 `Array` 构造器的括号里，括号内的东西有个正式名称，叫*实参*。

```javascript
let a = new Array("Anchimolios", "Morgan Woods", "Rachel Griffiths", "Charlie Henderson");
alert(a.length); // 4

// 相当于
let a = ["Anchimolios", "Morgan Woods", "Rachel Griffiths", "Charlie Henderson" ]; // 好吧，至少回来了四个
```

这时有同学提问：

> 假如我们要用这种方式创建一个只包含一个数字成员的数组，不就会与创建“包含这个数量的数组”混淆了吗？

这是 JavaScript 设计时一个没考虑周到的地方，我们在使用时应当加以注意。当然，我们完全可以直接使用方便的数组字面量来创建数组，也可以使用另一种方式——利用字符串的 `split` 方法，将一段字符串按照特定分隔符，分解成数组。当我们需要构造比较长的字符串数组时，可以使用这种方式，它比完整的数组字面量更为简便。`split` 方法更多情况下适用于直接根据用户输入建立列表。

```javascript
const source = "Dark night gave me black eyes, but I use it to look for light";
const array = source.split(" ");  // 根据空格进行拆分
alert(array);                     // "Dark,night,gave,me,black,eyes,,but,I,use,it,to,look,for,light"
const source2 = "黑夜给了我黑色的眼睛，我却用它来寻找光明";
const array2 = source2.split(""); // 直接将每个字符都作为数组元素
alert(array2);                    // "黑,夜,给,了,我,黑,色,的,眼,睛,，,我,却,用,它,来,寻,找,光,明"

// 数组的 join 方法可以将数组元素以特定文本相连，组合成字符串
alert(array2.join("。"));         // "黑。夜。给。了。我。黑。色。的。眼。睛。，。我。却。用。它。来。寻。找。光。明"
```





### 插入与移除

我们的数组不会是一成不变的。如果我们有一列学生，我们有可能会在前面、后面或中间安插新学生的座位，如果有学生要离开这一列，我们也需要将他的座位移走。JavaScript 中提供了一些方便的操作，来在数组中实施以上现实中的需求。

JavaScript 提供了三个*数组方法*。方法是一些函数，它以属性的形式被访问，并按规定的方式使用。“方法”一词反映了它们的本质：通过一些固定方式来完成指定的需求。

`push` 方法用于在数组末尾加入一个元素，并得到数组的新长度。

```javascript
let list = ["red", "orange", "yellow", "green"];
alert(list.length); // 4
list.push("blue");  // 加入 "blue" 这个字符串
alert(list.length); // 5
alert(list);        // red,orange,yellow,green,blue
```

我们可以直接查看数组内部所包含的元素，如运行结果所显示的那样，`list` 数组末尾添加了 `"blue"` 这个字符串。我们也可以一次多添加几个元素：

```javascript
alert(list.push("purple", "pink")); // 添加两个元素并显示数组的新长度 7
alert(list.length);                 // 7
alert(list);                        // red,orange,yellow,green,blue,purple,pink
```

`unshift` 方法将一个或多个元素添加到数组的开头，并得到数组的新长度。

```javascript
let flowers = ["Calendula", "Chrysanthemum", "Cosmos", "Dianthus"];
alert(flowers.length);            // 4
alert(flowers.unshift("Dahlia")); // 把大丽花加进来，现在长度是 5
alert(flowers.length);            // 是的！就是5！

```

和 `push` 类似，它也可以一次添加多个元素。

此外还有一个 `concat` 方法，它用于将两个数组拼在一起，并得到合并后的新数组。

```javascript
// 现在有两支来自日本的观光团，他们要进行合并以统一行程。
let visitors_1 = ["Jissoji Goro", "Kagawa Nui", "Okamura Nariakira",
                  "Ehara Kiyumi", "Okita Miu", "Tanji Chigusa"];
let visitors_2 = ["Abo Akasuki", "Kirishima Kayoko", "Kuwahara Toichi",
                  "Amachi Hisato, Nakayama Norihisa"];
alert(visitors_1.length);                     // 现在第一支观光团有 6 人。
alert(visitors_2.length);                     // 第二支观光团有 4 人。
let visitors = visitors_1.concat(visitors_2); // 合并！
alert(visitors.length);                       // 现在新的观光团有十个人。
alert(visitors);                              // Jissoji Goro,Kagawa Nui,
                                              // Okamura Nariakira,Ehara Kiyumi,
                                              // Okita Miu,Tanji Chigusa,...

```

提供了加入元素的方法，自然也提供了移除元素的途径。

`pop` 方法与 `push` 相对，用于移除数组的最后一个元素，并得到这个移除的元素值。

```javascript
let list = [1, 2, 3, 4, 5];
alert(list.pop()); // 5
alert(list);       // 1,2,3,4

```

`shift` 方法与 `unshift` 方法相对，用于移除数组的第一个元素，并得到移除的元素值。

```javascript
let list = [1, 2, 3, 4, 5];
alert(list.shift()); // 1
alert(list);         // 2,3,4,5

```

如果操作的数组是什么元素也没有的空数组，那么执行方法时只能得到一个 `undefined` 值。

```javascript
let empty = [];
alert(empty.pop()); // undefined

```

我们可以利用刚刚了解到的几个数组方法来模拟一个排队的场景。

```javascript
let queue = []; // 现在还没人开始排队。
queue.push("Delphium  Vitulus");
queue.push("Palinurus  Catullus");
queue.push("Amatia  Laevinus");          // 到现在为止，队伍里有三个人。
alert("现在队伍情况：" + queue);
queue.push(prompt("请输入新来者的名字：")); // 新来者的名字由你决定
alert(queue.shift() + "离开了，大家向前一位。");
alert("又离开了一位：" + queue.shift());
queue.push("Talmudia  Zosimus");
queue.push(queue.shift()));                // 队伍第一位又重新开始排队
alert(queue.pop() + "等不住了，走了");
alert("现在队伍里共有" + queue.length + “人。"");

```

上述数组方法都是在起始或结束位置添加元素，约束性太强。我们经常需要从数组的任意位置删除元素。由于数组也是一类对象，也可以使用 `delete` 操作符，那么它会产生怎样的效果呢？

```javascript
const language = ["C++", "Java", "Python", "Ruby", "Swift"];
delete language[2];
// 咦，长度怎么没有改变？
alert(language.length); // 5
alert(language);        // "C++,Java,undefined,Ruby,Swift"

```

显然，这种删除数组元素的方法是无效的，它只是清除了某一位置上元素的值，但依然保留了元素所占的位置。数组仍然有五个元素，我们还要删除 `undefined`。

类似地，如果要在数组任意位置插入元素，应该怎么做呢？JavaScript 的所有数组都拥有 `splice` 方法。给出一个索引，`splice` 方法可以完成删除和插入元素的操作。

```javascript
const language = ["C++", "Java", "Python", "Ruby", "Swift"];
let removedItem = language.splice(2, 1); // 从第二个索引，也就是第三个元素开始，删除一个元素
                                         // splice 方法返回被删除的元素组成的数组
alert(removedItem);                      // "Python"
alert(removedItem.length);               // 1
// language 中不再有 "Python"，后面的元素自动向前移动
alert(language.length);                  // 现在只剩四个元素了

removedItem = language.splice(1, 2, "Haskell", "Erlang", "Perl");
                                         // 在 splice 方法中添加参数，可以实现在指定位置插入新元素
alert(removedItem.length);               // 3
alert(language.length);                  // 5
alert(language);                         // "C++,Haskell,Erlang,Perl,Swift"

```

在这个例子中，`splice` 至少需要两个参数，分别是起始索引和需要移除的元素个数。如果没有指定元素个数也可以工作，`splice` 会删除从起始索引开始直到末尾的所有元素。然后，`splice` 将所有删除掉的元素组合成一个新数组并返回。如果 `splice` 接收到了三个或更多参数，那么移除元素后，会将剩余的参数都作为数组元素，从起始索引开始插入数组。这里，`splice` 删除了 `"Java"` 和 `"Ruby"` 两个元素，然后从 `"Java"` 原来的位置开始插入 `"Haskell"`，接下来是 `"Erlang"` 和 `"Perl"`。插入完毕后，再调整被移除元素后面原来元素的位置。





### 排序与查找

在计算机科学中，对数据进行排序是一个常见需求。生活中也常有这样的例子，比如教科书的扉页上按照笔画顺序排列的编者姓名、按照分数排列的成绩单等。JavaScript 的数组作为存储数据的载体，提供了一个叫 `sort` 的方法用于数组排序。它会将数组中的元素按照字典顺序排列，如果遇到的元素不是字符串，就会将它转换为字符串来看待。

`sort` 方法直接对数组进行操作，同时返回修改后的数组，与下文中的 `reverse` 方法一致。

```javascript
let array = ["Since", "then", "no", "torch", "such", "as", "fire", "I", "will", "be", "the", "only", "light"]; // 鲁迅先生名言：此后如竟没有炬火，我便是那唯一的光
alert(array.sort()); // "I,Since,as,be,fire,light,no,only,such,the,then,torch,will"

// 大写字母总会被排列在小写字母前面，数字也是按照字典顺序排列
array = [1, 11, 21, 2, 0, "Apple", "apollo", "Beta"]; 
alert(array.sort()); // "0,1,11,2,21,Apple,Beta,apollo"

```

这样的排序规则比较简单，我们将会在第五章接触到更为高级和灵活的排序技巧。



------

Note：

数组的 `sort` 方法实际上是根据每项元素转换为字符串后的 Unicode 码点进行排列的。·

------



另一种可能遇到的排序需求是，将数组中所有元素的顺序反过来，也就是*数组倒序*（reverse），这时不会关心数组的具体内容，一把梭，敢教日月换新天！

```javascript
let array = ["Since", "then", "no", "torch", "such", "as", "fire", "I", "will", "be", "the", "only", "light"];
alert(array.reverse()); // "light,only,the,be,will,I,fire,as,such,torch,no,then,Since"

```

`reverse` 方法可以配合 `sort` 方法来使用：`sort` 将数组元素按照字典顺序排列，`reverse` 再进行倒序，也就是按照倒字典序（Z-A）进行排列。如果需要将字符串中每个字符的顺序翻转，也可以结合字符串的 `split` 方法。

```javascript
let array = ["Since", "then", "no", "torch", "such", "as", "fire", "I", "will", "be", "the", "only", "light"];
alert(array.sort().reverse()); // "will,torch,then,the,such,only,no,light,fire,be,as,Since,I"
let array2 = "鸿雁长飞光不度，鱼龙潜跃水成文".split(""); // 将每个字拆分成数组元素
alert(array2.reverse().join(""));                     // "文成水跃潜龙鱼，度不光飞长雁鸿"

```

计算机科学界的高峰、高德纳先生的著作《计算机程序设计艺术》中有一整卷书专门讲排序与查找两大数据处理方式，可见查找操作在数据处理领域占据着与排序相当的重要地位。我们在使用文本处理软件时，查找功能为我们带来了莫大方便。JavaScript 中的数组提供了 `indexOf` 和 `lastIndexOf` 两个方法，用于查找指定元素。

```javascript
const weather = ["sunshine", "rain", "snow", "dew", "rainbow", "wind"];
alert(weather.indexOf("rain"));     // 1
alert(weather.lastIndexOf("rain")); // 5

```

`indexOf` 方法接受要查找的元素作为参数，在数组中找到第一个匹配的元素，并返回索引。如果找不到，那么返回 `-1`。

```javascript
weather.indexOf("snow");    // 2
weather.indexOf("snowman"); // -1

```

而查找某个元素最后一次出现时的索引，可以用 `lastIndexOf`方法。

```javascript
weather.lastIndexOf("snow");    // 4
weather.lastIndexOf("snowman"); // -1

```

此外，还有一个简单的 `includes` 方法，用于确定一个元素是否在数组中存在，返回 `true` 或 `false`。

```javascript
weather.includes("snow");    // true
weather.includes("snowman"); // false

```

数组的查找方法可以应用在实际生活中。例如下面这个小程序模拟了文本处理软件的查找功能。

```javascript
// 查找小程序
const source = prompt("请输入一段英文文本，用空格分隔").split(" ");
const target = prompt("请输入要查找的词：");
let index = source.indexOf(target);
let lastIndex = source.lastIndexOf(target);
alert(`在给定文本中搜索“${target}”，结果如下：
    第一次出现的位置：${index}
    最后一次出现的位置：${lastIndex}`);

```

假设第一次输入“ Eating grapes spit grapes skins while not spit grapes skins while not eating grapes”，第二次输入“grapes”，那么会得到这样的搜索结果。

![1565929449193](assets/1565929449193.png)

我们刚才已经了解了用于删除和替换元素的 `splice` 方法，那么也可以考虑将它应用到这里来，升级成替换功能：

```javascript
// 替换小程序
// 目前只能替换第一个（和最后一个）匹配的词
// 在后面我们将学到更高级的内容来完善这个程序
const source = prompt("请输入一段英文文本，用空格分隔").split(" ");
const target = prompt("要替换的词：");
const destination = prompt("替换成：");
let index = source.indexOf(target);
source.splice(index, 1, destination);
alert(`在给定文本中替换“${target}为“${destination}”，结果如下：
    ${source.join(" ")}`);

```

这次我们试试把“grape”替换成“banana”（有点奇怪），得到了这样的结果：

![1565930786117](assets/1565930786117.png)

咦？我们不是要替换掉第一个出现的“grape”吗？怎么会这样？

关键的地方在于这里：

```javascript
let index = source.indexOf(target);
source.splice(index, 1, destination);

```

`indexOf` 方法只有在找到与 `target` 的内容完全一致的元素时才会返回索引，否则得到 `-1`。因为 `-1`不是一个合法的数组索引，它表示“未找到”。这里，我们用“grape”进行查找，但是数组中只有单独的`"grapes"`，而没有`"grape"`，因此`index` 会等于 `-1`。

但是 `splice` 并不知道这一点。根据 `splice` 的规则，如果第一个表示索引的参数是一个负数（$$-x$$），那么 `splice` 会理解为移除倒数第 $$x$$ 个元素，并在其位置上插入新元素（如果指定了的话）。因此，这里 `splice` 得到了 `index`，由于它是 `-1`，所以将 `source` 的倒数第一个匹配元素替换为 `destination`（也就是 `"banana"`），最终呈现为我们看到的结果。

为了解决这个问题，我们可以用 `includes` 方法判断一下 `source` 中是否包含指定的 `target`。当然，`includes` 方法需要重新查看整个数组，可能会造成效率问题，因此可以直接用 `index` 做简单判断，再决定是否进行替换。

```javascript
// 替换小程序
// 目前只能替换第一个（和最后一个）匹配的词
// 在后面我们将学到更高级的内容来完善这个程序
const source = prompt("请输入一段英文文本，用空格分隔").split(" ");
const target = prompt("要替换的词：");
const destination = prompt("替换成：");
let index = source.indexOf(target);
index !== -1 ? source.splice(index, 1, destination) : null;
alert(`在给定文本中替换“${target}”为“${destination}”，结果如下：
    ${source.join(" ")}`);

```

第八行代码使用了一个三目表达式来做选择，表达式的值会被丢弃，其作用体现在 `source` 上。现在再来测试一波代码，可以看到我们实现了预期结果。

![1565932209076](assets/1565932209076.png)

![1565932212738](assets/1565932212738.png)









## 物以类聚·数据类型

------

### JavaScript 中的数据类型

JavaScript 所有的值（数据）都有着自己的**数据类型**。目前 JavaScript 中共有以下的数据类型：

- `number`（数值）
- `BigInt` （任意精度整数，2019年发布）
- `string`（字符串）
- `object`（对象）
- `function`（函数）
- `undefined`
- `regexp`（正则表达式）
- `symbol`（符号）

我们已经接触了 `number` 用于数值计算，`string` 用于处理文本内容，`object` 作为存放其他数据的结构，还有 `undefined`，它自身也是一种独立的数据类型。你可能会为看不见 `array` 而感到奇怪，事实上，数组是一种特殊的对象，它被精心设计以用于处理数据，但是我们仍需将它归类为 `object`。至于另外三种数据类型，我们会在后面逐渐接触到。

JavaScript 提供了 `typeof` 操作符来确定一个值的数据类型，它得到类型的字符串名称，即以上七种之一。

```javascript
alert(typeof 123);           // "number"
alert(typeof NaN);           // "number
alert(typeof Infinity);      // "number"
alert(typeof "Hello world"); // "string"
alert(typeof {});            // "object"
alert(typeof [1, 2, 3]);     // "object"
alert(typeof null);          // "object"
alert(typeof alert);         // "function"
alert(typeof undefined);     // "undefined"
```



------

Note: 为什么 `typeof null === "object"` ？

在 JavaScript 第一个版本的实现中，每个值在内部存储时都会用一个标记来记录它的数据类型。由于 `object` 是 JavaScript 中的“第一等类型”，它的类型标记为 `0`，而 `null` 表示为 *`NULL` 指针*，在大多数平台上， `NULL` 指针的实际值是 `0x00`，那么 `null` 的数据类型标记实际上与 `object` 相同。因此 `typeof` 运算符在获取 `null` 的类型标记的时候，得到的是 `0` ，便会将它判断为 `"object"`。

------





### 判断数据类型的技巧

`typeof` 的首要作用自然是判断数据类型，以便了解到的数据类型做出可能的操作。它具有明显的局限性：它对数据类型的判断仅限于以上七种；无法区分 `array` 和一般的 `object`；当我们明确地需要一个**对象**时它却会将 `null` 混为一谈。我们需要在 `typeof` 的判断的基础上使用一些辅助方法，以便在各类数据类型之间游刃有余。

**区分数组与对象**

`typeof` 会将数组判定为 `"object"`，没关系，JavaScript 提供了 `Array.isArray` 函数来判断一个值是不是数组。那么我们只需要：

```javascript
alert(Array.isArray([1, 2, 3]));   // true
alert(Array.isArray([]));          // true
alert(Array.isArray(new Array())); // true
alert(Array.isArray({}));          // false
```



**精确地判断对象**

我们在第一节（逻辑）中了解过，`null` 会被当做一个假值，因此对它进行非运算会得到 `true`。

我们可以采取这样的策略：

- 使用`typeof` 进行判断，如果它不是 `"object"`，得到 `false`。
- 如果它是 `"object"`，判断它是否为数组，若是，得到 `false`。
- 如果它是 `null`，得到 `false`，否则为 `true`。可以对它进行 `!!`操作，若为 `null` ，我们就会得到 `false`，否则我们就会得到 `true`。

示例：

```javascript
let value = "Hello world";
alert( // 对 "Hello" 进行判断
    typeof value !== "object" ? false :
        Array.isArray(value) ? false :
        !!value
); // false
// value = true -> false
// value = 123  -> false
// value = null -> false
// value = [1, 2, 3] -> false
// value = {a: 1, b: 2} -> true
// value = window -> true
```

**精确判断数值**

`NaN` 和 `±Infinity` 都属于 `number` 类型，但是我们在进行数学运算的时候并不希望将它们参与到运算中。我们只需要进行一些附加判断即可将它们与真正的数字区分开来。

```javascript
let n = 100;
alert(
    typeof n !== "number" ? false :
        isNaN(n) ? false : isFinite(n)
); // true
// n = "123" -> false
// n = NaN   -> false
// n = Infinity -> false
// n = Number.MAX_VALUE      -> true
// n = Number.MAX_VALUE * 10 -> false
```









## 人以群分·解构赋值

------

JavaScript 提供了一类语法以简化赋值操作，可以根据一组数据，一次定义一组变量，像这样：

```javascript
let [a, b] = [1, 2];
alert(a); // 1
alert(b); // 2
```

等号右边是一个通常的对象/数组字面量，而等号左边就写成与右边相匹配的格式，即一个*模式*，以满足我们的需要。

它实际上是如下方式的替代：

```javascript
let arr = [1, 2];
let a = arr[0];
let b = arr[1];
```

这类语法被称为*解构赋值*，按字面意义上来理解，就是“解析一个结构，并进行赋值”。





### 数组解构

你可以将一组变量在声明时同时进行赋值操作。

```js
let arr = ["one", "two", "three"];
let [one, two, three] = arr;
alert(one); // "one"
alert(two); // "two"
alert(three); // "three"
```

也可以将声明与赋值分离。

```javascript
let a, b;
[a, b] = [1, 2];
alert(a); // 1
alert(b); // 2
```

如果一个模式没有找到相匹配的值，相应的变量就会得到 `undefined`，因为不知道到该给它赋什么值，只能说明它是“未定义”的。

```javascript
let [a, b, c] = [1, 2];
alert(a); // 1
alert(b); // 2
alert(c); // undefined
```

为了避免发生这种情况，可以在模式中为变量设置一个默认值。如果找不到匹配值，就使用变量的默认值。

```javascript
let [a = 3, b = 4, c = 5] = [1, 2];
alert(a); // 1
alert(b); // 2
alert(c); // 5
```

在一个解构赋值的表达式中我们还可以交换两个已有变量的值，以避免使用*临时变量*。

```javascript
let a = 3, b = 5;
[a, b] = [b, a];
alert(a); // 5
alert(b); // 3

// 不使用解构赋值
let temp = a;
a = b;
b = temp;
alert(a); // 5
alert(b); // 3
```

你也可以忽略你不感兴趣的值：

```js
let [a, , b] = [1, 2, 3];
alert(a); // 1
alert(b); // 3

// 甚至忽略所有值，但是没必要这样
[, ,] = [1, 2, 3];
```

当解构一个数组时，可以使用*剩余模式*，将数组的“剩余部分”交给一个变量。

```js
let [a, ...b] = [1, 2, 3];
alert(a); // 1
alert(b); // [2, 3]
```

注意：如果剩余模式右侧有逗号，会得到一个语法错误，因为剩余元素必须是数组的最后一个元素。

```js
let [a, ...b,] = [1, 2, 3]; // SyntaxError: rest element may not have a trailing comma
```

同时，使用剩余模式赋值的变量不能被设置默认值。

```javascript
let [a, ...b = 2] = [3, 4] // SyntaxError: Invalid destructuring assignment target
alert("a = " + a);         // 不会执行
alert("b = " + b);         // 不会执行
```

用于实现剩余模式的三个点号称为*Spread 操作符*。





### 对象解构

除了数组以外，你还可以对一个对象进行解构赋值。在数组解构中，变量被赋予的值取决于它的排列顺序，而在对象解构中，变量根据对象中对应的属性名被赋予值。

```js
let o = {p: 42, q: true};
let {p, q} = o;
alert(p); // 42
alert(q); // true
```

通过解构，无需声明即可赋值一个变量。

```js
let a, b;
({a, b} = {a: 1, b: 2});
alert(a); // 1
alert(b); // 2
```

赋值语句周围的 `( ... )` 是使用对象字面解构赋值时不需要声明的语法。`{a, b} = {a: 1, b: 2}` 不是有效的独立语法，因为左边的 `{a, b}` 被认为是一个**块语句**而不是对象字面量。然而，`({a, b} = {a: 1, b: 2})` 是有效的，相当于`let {a, b} = {a: 1, b: 2}`



------

Note：

你的`( ... )` 表达式需要一个分号在它前面，否则它也许会被当成上一行中的函数来执行。

------



我们也可以根据属性，将值赋给我们需要的变量名，而不一定与属性名重名。

```js
let obj = {p: 42, q: true};
let {p: a, q: b} = obj; 
// 相当于
// a = obj.p;
// b = obj.q 
alert(a); // 42 
alert(b); // true
```

变量也可以先赋予默认值。当要提取的对象没有对应的属性，变量的值就是它的默认值。

```js
let {a = 10, b = 5} = {a: 3};
alert(a); // 3
alert(b); // 5
```

可以将上述方法结合起来。

```js
let {a: first = 10, b: second = 5} = {a: 3};
alert(first); // 3
alert(second); // 5
```

模式中可以像普通对象字面量那样使用计算属性名，来确定要从对象中匹配的属性值。

```js
let key = "name";
let { [key]: theName } = { name: "Pluto" };
alert(theName); // "Pluto"
```

事实上，我们还可以像数组解构那样，对对象解构应用剩余模式：

```js
let {a, b, ...others} = {a: 10, b: 20, c: 30, d: 40}
alert(a);        // 10 
alert(b);        // 20
// others = { c: 30, d: 40 }
alert(others.c); // 30
alert(others.d); // 40
```

显然，如果一个属性不能作为合法的标识符名称，就需要用一个等价的方式来代替。

```js
const obj = { "hello-world": "Oh!" };
const { "hello-world": helloWorld } = obj;

alert(helloWorld) // "Oh!"
```