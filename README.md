1. TypeScript 的类型检测其实最主要的针对并不是变量，而是函数。因为在 JavaScript 中的函数时不考虑参数的类型和个数的。

```ts
function sum(a: number, b: number):number {
    return a + b
}

let result = sum(123, 456)
console.log(result)
```

2. TypeScript 中可以直接使用字面量进行类型声明

```ts
let a: 10;
a = 10;
```

这样就规定了其只可以 a 被 10 赋值

3. TypeScript 可以使用 | 来连接多个类型【联合类型】

```ts
let c: boolean | string;
c = true;
c = "hello";
```

4. TypeScript 中的 any 类型声明，这个模式下就和原生 js 没啥区别了

```ts
let d:any;
d = 10;
d = "hello";
d = true;
```

因此，一个变量设置类型为 any 后，相当于对该变量关闭了 TS 的类型检测，TS 压根就不管这个变量了，TypeScript 中不建议使用 any。

5. 显示 any / 隐式 any

```ts
let d;  <=> let d: any;
```

声明变量如果不指定类型，则 TypeScript 解析器会自动判断变量的类型为 any

6. 当 TypeScript 中一个变量的类型不确定的时候，可以使用 unknowm 来类型声明表示未知类型的值。

```ts
let e: unknown;
e = 10;
e = false;
e = "hello";
```

7. any / unknown 的区别

当使用 any 的时候，any 类型的变量不仅可以自己赋任意值，同时也可以将 any 类型变量赋值给任意变量。

当使用 unkonwn 时，就不可以将这个 unknomn 类型变量的值赋给别的类型了。

unknowm 实际上就是一个类型安全的 any。

当一个 unknown 类型的变量想要赋值给其它变量的时候，可以在赋值之前做一个类型判断。

```ts
let e: unknown;
e = 10;
e = false;
e = "hello";

if(typeof e === "string") {
    d = e
}
```


8. 类型断言

可以用来告诉解析器变量的类型

```ts
c = e as string;
c = <string>e;
```

这两种写法等价的。

9.  void 与 never：用以设置函数返回值

void 是指函数没有返回值

```ts
function fn() {

}
```

never 是指函数永远不会返回结果

```ts
function fn1(): never {
    throw new Error("报错了！");
}
```

10. object 类型声明并不实用

```ts
let h: object;
h = {};
h = function() {};
```

11. {} 用来指定对象中可以包含哪些属性

语法：{属性名: 属性值, 属性名: 属性值}

? 语法：可设置对象属性为可选

```ts
let i:{ name: string , age?:number};
i = {name: '书悟空'};
```


12. ? 可选属性写法的加强版

[propName: string]: any 表示可以有任意属性

```ts
let j: {name: string, [propName: string]: any}
j = {name: '猪八戒', age: 18, gender: '男'}
```

这个表示任意类型字符串的属性名。

所以上面的表达式中 name 是必需的属性，其它的可以由用户任意输入。


13. 设置函数结构的类型声明：

语法：(形参: 类型, 形参: 类型 ....) => 返回值

```ts
let k:(o: number, p: number) => number;
k = function (n1: number, n2: number) {
    return n1 + n2
}
```

14. 数组类型声明的两种表达方式

a. 类型[]
b. Array<类型>

```ts
let arr1: string[];
arr1 = ['a', 'b', 'c'];

let arr2: number[];
arr2 = [1, 2, 3];

let arr3: Array<number>
arr3 = [1,2,3,4,5]
```


15. 元组：元组就是固定长度的数组

当数组里面的元素是固定的 用元组就会比较好

```ts
let h1:[string, string];
h1 = ['hello', 'h1']
```

16. enum 枚举

将所有可能的情况列出来

```ts
enum Gender {
    Male,
    Female
}

let i1: {name: string, gender: Gender}
i1 = {
    name: '孙悟空',
    gender: Gender.Male
}

```

17. & 表示同时

```ts
let j1: { name: string } & { age: number };
j1 = { name: '顺悟空', age: 16 }
```

18. 类型别名

解决类型规定过长的问题

```ts
type myType = 1 | 2 | 3 | 4 | 5;
let p1: myType;
let m1: myType;
```

19. 类

19.1 属性

a. 静态属性

不需要生成实例就可以访问的属性就是静态属性，只需要在类中定义的实例属性前使用 static 关键字来定义。

```ts
static age: number = 18;
```

b. 实例属性

直接定义的属性是实例属性，需要通过对象的实例去读写。

```ts
const pre = new Person()
console.log(pre.name)

c. readonly 定义只读属性 不可以修改

static readonly age: number = 18;
readonly name: string = '孙悟空';
```


19.2 方法

a. 实例方法

```ts
class Person {
sayHello() {
	console.log('Hello 大家好！')
}
}

const pre = new Person()
pre.sayHello()
```

b. 类方法

```ts
class Person {
static sayHello() {
	console.log('Hello 大家好！')
}
}

Person.sayHello()
```

19.3 构造函数和 this

```js
class Dog {
    name: '旺财'
    age = 3
    bark() {
        alert('汪汪汪');
    }
    sayHello() {
        console.log('Hello 大家好！')
    }
}

const dog1 = new Dog()
const dog2 = new Dog()
const dog3 = new Dog()
const dog4 = new Dog()
```

在实例方法中，this就表示当前的实例

在构造函数中，当前对象就是当前新建的那个对象，可以通过this向新建的对象中添加属性


```ts
class Dog {
    name: string;
    age: number;
    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
    bark() {
        alert(this.name);
    }
}
const dog1 = new Dog(name: '小黑', age: 4);
const dog2 = new Dog(name: '小白', age: 6);
```


19.4 继承

```ts
(function() {
    // 抽取公共  -  父类
    class Animal {
        name: string;
        age: number;
        constructor(name: string, age: number) {
            this.name = name;
            this.age = age;
        }
        sayHello( ) {
            alert('动物在叫');
        }
    }
    // 继承 Animal  -  子类
    class Dog extends Animal{
    }
    class Cat extends Animal{
    }
})()
```


在继承父类基础之上可以新增

```ts
class Dog extends Animal{
    // => 子类新增 run 方法
        run() {
            console.log('狗在跑')
    }
        // => 出现了与父类相同的方法，则使用子类
    sayHello() {
            console.log('汪汪汪')
    }
}
```


注意：当子类中拓展的方法与父类同名，子类将会覆盖父类的方法，将这种情况称为方法重写。


20. super 关键字

在子类中 super 就代表当前类的父类

由于在子类中可能是需要额外定义其它类属性的，因此会用到了 constructor 构造函数，因此需要使用到 super 关键字来对父类进行调用。

```ts
(function() {
    // 抽取公共  -  父类
    class Animal {
        name: string;
        constructor(name: string) {
            this.name = name;
        }
        sayHello( ) {
            alert('动物在叫');
        }
    }
    // 继承 Animal  -  子类
    class Dog extends Animal{
        age: number;
        constructor(name:string, age: number) {
            // 如果在子类中写了构造函数，在子类构造函数中必须对父类进行调用
            super(name); // => 调用父类的构造函数
        }
        sayHello() {
            super.sayHello();
        }
    }
})()
```


21. 抽象类

如何禁止一个类被用来创建对象呢？

以 abstructract 开头的类是抽象类，抽象类和其它类的区别不大，只是不能用来创建对象，抽象类其实就是专门用来被继承的类。


```ts
(function() {
    // 抽取公共  -  父类
    abstract class Animal {
        name: string;
        constructor(name: string) {
            this.name = name;
        }
        sayHello() {
            alert('动物在叫');
        }
    }
    // 继承 Animal  -  子类
    class Dog extends Animal{
        sayHello() {
           console.log('汪汪汪');
        }
    }
    const dog = new Dog(name: '旺财');
    dog.sayHello()
})()
```


其中，抽象类里面可以添加抽象方法：

抽象方法使用 abstract 开头，没有方法体，并且抽象方法只能定义在抽象类中，子类必须对抽象方法进行重写。

```ts
(function() {
    // 抽取公共  -  父类
    abstract class Animal {
        name: string;
        constructor(name: string) {
            this.name = name;
        }
       abstract  sayHello():void;
    }
    // 继承 Animal  -  子类
    class Dog extends Animal{
        sayHello() {
           console.log('汪汪汪');
        }
    }
    const dog = new Dog(name: '旺财');
    dog.sayHello()
})()
```


22. 接口

接口可以重复声明，会取一个属性并集，但是 type 不可以


接口可以在定义类的时候去限制类的结构，接口中的所有的属性都不能有实际的值，接口只定义对象的结构，而不考虑实际值，在接口中的所有方法都是抽象方法。


定义类时，可以使类去实现一个接口，实现接口就是使类满足接口的要求。

```ts
interface myInter {
    name: string,
    sayHello():void;
}

class MyClass implements myInter {
    name: string;
    constructor(name: string) {
        this.name = name
    }
    sayHello() {
        console.log('ssss')
    }
}
```

xx.  tsc .\TypeScript的类型声明.ts -w

进行 .ts 文件的自动监视更新 js

xx. tsconfig.json 是 ts 编译器的配置文件，ts 编译器可以根据它的信息来对代码进行编译。

*include 用来指定哪些 .ts 文件需要被编译

```json
  "include": [
    ”./src/**/*“
  ]
```

其中 `"./src/**/*"` 的意思是：src 文件夹下的所有文件夹的所有文件。

** 表示任意目录
  * 表示任意文件

*exclude 被排除编译的文件，其默认值为 ["node_modules", "bower_components", "jspm_packages"]

```json
  "exclude": [
    "./src/hello/**/*"
  ]
```

*extends 引入继承其它配置文件

```json
"extends": "./configs/base"
```

*files 指定被编译文件列表，只有需要编译的文件少时才会用到

```json
  "files":[
    "core.ts"
  ]
```

