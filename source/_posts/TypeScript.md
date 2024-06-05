---
title: TypeScript
date: 2024-06-04 22:23:05
tags: 前端
categories: 笔记 
---
# TypeScript简介

## 优势

- 更早发现错误，提高效率
- 任何位置都有代码提示
- 重构代码容易
- 支持最新ECMAScript语法
- 类型推断机制

# 常用类型

## 类型注解

**作用**：为变量{% label 添加类型约束 orange%}

**JS已有类型**

- 原始类型
  - number
  - string
  - boolean
  - null
  - undefined
  - symbol

完全按照JS中类型名称，加上注解即可

```typescript
let age: number = 18
let myName: string = '刘老师'
let isLoading: boolean = false
let a: null = null
let b: undefined = undefined
let s: symbol = Symbol()
```

- 对象类型

  - object(数组，对象，函数)

  - 数组

    - ```ts
      let number: number[] = [1,3,5] 
      let strings: Array<string> = ['a','b','c']
      let arr: (number | string)[] = [1,'a',3,'b']
      // |(竖线)在TS中叫做联合类型（由两个或多个其他类型组成的类型，表示可以是这些中的任意一种，注意不要和js中的或(||)混淆
      ```

**TS新增类型**

- 联合类型

  - ```ts
    let arr: (number | string)[] = [1,'a',3,'b']
    ```

- 自定义类型（类型别名）

  - ```ts
    type CustomArray = (number | string)[]
    let arr1: CustomArray = [1,'a',3,'b']
    let arr2: CustomArray = ['x','y',6,7]
    ```

- 函数类型

  - ```ts
    //单独指定参数,返回值类型
    function add(num1:number,num2:number): number{
        return num1 + num2
    }
    const add = (num1:number, num2:number):number=>{
        return num1 + num2
    }
    //同时指定参数,返回值的类型
    const add: (num1: number, num2:number) => number = (num1,num2)=>{
        return num1 + num2
    }
    // 没有返回值,函数返回类型为void
    function greet(name:string):void {
        console.log('Hello',name)
    }
    // 可选参数
    function mySlice(start?: number, end?:number): void {
        console.log('起始索引:',start,'结束索引:',end)
    }
    //注意:可选参数智能出现在参数列表的最后,即可选参数后面不能再出现必选参数
    
    ```

- 对象类型

  - ```ts
    let person: {
        name: string;
        age: number;
        sayHi(): void
    } = {
        name: 'jack',
        age: 19,
        sayHi(){}
    }
    //可选属性
    function myAxios(config:{url: string; method?:string}):void{
        console.log(config)
    }
    ```

- 接口

  - ```ts
    //1.使用interface关键字来声明接口
    //2.接口名称可以是任意合法的变量名称
    //3.声明接口后,直接使用接口名称作为变量的类型
    //4.因为每一行只有一个属性,因此属性类型后面没有;
    interface IPerson {
        name: string
        age: number
        sayHi(): void
    }
    let person: IPerson = {
        name: 'jack',
        age: 19,
        sayHi(){}
    }
    
    
    //接口和类型别名的区别
    type IPerson = {
        name: string
        age: number
        sayHi(): void
    }
    //相同点: 都可以为对象指定类型
    //不同点:
    //	1. 接口只能为对象指定类型
    //	2. 类型别名,不仅可以为对象指定类型,实际上可以为任意类型指定别名
    
    
    //接口的继承
    interface Point2D {x: number; y:number}
    interface Point3D {x: number; y:number; z:number}
    //更好的方式
    interface Point2D {x: number; y:number}
    interface Point3D extends Point2D {z: number}
    ```

- 元组

  - 场景: 在地图中,使用经纬度来坐标来标记位置信息

  - 可以使用数组来记录坐标,那么该数组中只有两个元素,并且这两个元素都是数值类型

  - ```ts
    let position:number[] = [39,56]
    ```

  - 使用number[]的缺点,不严谨,因为该类型的数组中可以出现任意多个数字

  - 更好的方式: 元组(Tuple)

  - 元组类型是另一种类型的数组,它确切地知道包含多少个元素,以及特定索引对应的类型

  - ```ts
    let position: [number,number] = [39,56]
    ```

- 类型断言

  - ```ts
    const alink = document.getElementById('link') as HTMLAnchorElement
    // 1. 使用 as 关键字实现类型断言
    // 2. 关键字 as 后面的类型是一个更加具体的类型
    // 3. 通过类型断言,alink的类型变得更加具体,
    // 另一种语法,使用<>语法
    const alink = <HTMLAnchorElement>document.getElementById('link')
    // 技巧:在浏览器控制台,通过console.dir()打印DOM元素,在属性列表的最后面,即可看到该元素的类型
    ```

- 字面量类型

  - ```ts
    let str = 'Hello TS' //str为string类型
    
    const str2 = 'Hello TS' //str为"Hello TS"类型
    ```

  - 使用模式: 字面量类型配合联合类型一起使用

  - 使用场景: 用来表示一组明确的可选值列表

  - 比如,在贪吃蛇游戏中,游戏的方向的可选值只能是上下左右中的任意一个

  - ```ts
    function changeDirection(direction: 'up'|'down'|'left'|'right'){
        console.log(direction)
    }
    ```


- 枚举

  - 类似字面量加联合类型组合

  - 1.使用 enum 关键字定义枚举

  - 2.约定枚举名称,枚举中的值以大写字母开头

  - 3.枚举中的多个值之间用逗号分隔

  - 4.定义好枚举后,直接使用枚举名称作为类型注解

  - ```ts
    enum Direction {Up,Down,Left,Right}
    
    function changeDirection(direction: Direction) {
        console.log(direction)
    }
    
    //类似于js中的对象,使用点(.)语法就可以访问枚举的成员
    console.log(Direction.Up)
    //字符串枚举
    enum Direction {
        Up = 'Up',
        Down = 'Down',
        Left = 'Left',
        Right = 'Right'
    }
    //注意字符串没有自增长欣慰,因此字符串枚举的每个成员必须有初始值
    ```

- void

- any

## 高级类型

- class类

  - ```ts
    // 实例属性初始化
    class Person {
        age: number
        gender: string = 'male'
    }
    
    //构造函数
    class Person {
        age: number
        gender: string
        
        constructor(age:number,gender:string) {
            this.age = age
            this.gender = gender
        }
    }
    
    //实例方法
    class Point {
        x = 10
        y = 10
        
        scale(n:number):void{
            this.x *= n
            this.y *= n
        }
    }
    ```

  - 类的继承

  - ```ts
    //1. extends 继承父类
    //2. implements(实现接口)
    
    //1.继承父类
    class Animal {
        move(){console.log('Moving along!')}
    }
    class Dog extends Animal {
        bark() { console.log('汪!')}
    }
    const dog = new Dog()
    
    //2.实现接口
    interface Singable {
        sing(): void
    }
    class Person implements Singable {
        sing() {
            console.log('你是我的小苹果')
        }
    }
    ```

  - 类成员的可见性

  - ```ts
    // 1. public:公有的,可以在任何地方访问
    // 2. protected:受保护的,在其声明的类和字类中可见,实例对象不可见
    // 3. private:私有的,只在当前类中可见,字类和实例中均不可见
    // 4. readonly:只读属性,只能用构造函数赋值,其他方法不行,接口或者{}表示的对象类型,也可以使用readonly
    class Person {
        readonly age:number = 18
        constructor(age: number) {
            this.age = age
        }
    }
    ```

  - 类型兼容性

  - ```ts
    //1. Structural Type System(结构化类型系统)
    //2. Nominal Type System(标明类型系统)
    // TS采用第一种也叫 duck typing(鸭子类型)
    class Point {
      x: number
      y: number
    }
    class Point2D {
      x: number
      y: number
    }
    
    const p:Point = new Point2D()
    //不会报错
    //因为两个类的属性数目和类型均相同
    //更准确的说,对于对象类型,如果x是y的子集,则x兼容y,y的实例可以赋值给x(成员多的可以赋值给少的)
    class Point {x: number;y: number}
    class Point3D {x: number;y:number;z:number}
    const p:Point = new Point3D()
    
    //接口兼容性
    interface Point {
      x: number
      y: number
    }
    interface Point2D {
      x: number
      y: number
    }
    
    let p1: Point = { x: 1, y: 2 }
    let p2: Point2D = p1
    console.log(p2.x, p2.y)
    
    //函数兼容性
    // 1.参数个数 2.参数类型 3.返回值类型
    
    // 1. 参数个数:参数少的可以赋值给参数多的
    type F1 = (a:number) => void
    type F2 = (a:number, b:number)=>void
    let f1: F1
    let f2: F2 = f1
    
    
    //2.参数类型:相同位置的参数类型要相同(原始类型)或兼容(对象类型)
    
    //3.返回值类型,关注返回值本身就行
    ```

  - 交叉类型

  - ```TS
    //交叉类型(&): 功能类似接口继承(extends),用于组合多个类型为一个类型(常用于对象类型)
    interface Person {name: string}
    interface Contact {phone: string}
    type PersonDetail = Person & Contact
    const obj: PersonDetail = {
        name: 'Tom',
        phone: '123456'
    }
    //交叉类型(&)和接口继承(extends)的对比
    // 相同点: 都可以实现对象类型的组合
    // 不同点: 两种方式实现类型组合时,对于同名属性之间,处理类型冲突的方式不同
    interface A {fn:(value:number)=>string}
    interface B extends A {fn:(value:string)=>string} //报错,参数类型不兼容
    typeC = A & B //不报错
    //相当于
    fn:(value:string | number)=> string
    
    ```

- 泛型

  - 泛型就是在保证类型安全的前提下,让函数等多种类型一起工作,从而实现复用,常用于函数,接口,class中

  - 需求: 创建一个id函数,传入什么数据就返回该数据本身(也就是说,返回值类型和参数相同)

  - ```ts
    function id(value: number):number {return value}
    //上例只能接收数值类型,无法用于其他类型
    //下例将参数类型修改为any,不安全
    function id(value: any):any {return value}
    
    //创建泛型函数
    function id<Type>(value:Type):Type {return value}
    //1.语法: 在函数名称的后面添加<>(尖括号),尖括号中添加类型变量,比如此处的Type
    //2.类型变量Type,是一种特殊类型的变量,他处理类型而不是值
    //3.该类型变量相当于一个类型容器,能够捕获用户提供的类型(具体是什么类型由用户调用该函数时指定)
    //4.类型变量Type,可以是任意合法的变量名称
    const num:number = id<number>(10)
    ```

  - 简化调用泛型函数

  - ```ts
    function id<Type>(value: Type): Type {return value}
    
    //原来调用
    let num: number
    let num = id<number>(10)
    
    //简化调用
    let num:number
    let num = id(10)
    ```

  - 泛型约束

  - ```ts
    //默认情况下,Type可以代表多个类型,这导致无法访问任何属性
    //比如,id('a')调用函数时获取参数的长度
    function id<Type>(value:Type): Type {
        console.log(value.length)//报错,找不到length属性
        return value
    }
    //1.指定更加具体的类型
    function id<Type>(value: Type[]): Type[] {
        console.log(value.length)
        return value
    }
    
    //2.添加约束
    
    //解释:
    //1.创建描述约束的接口ILength,该接口要求提供length属性
    //2.通过extends关键字使用该接口,为泛型(类型变量)添加约束
    //3. 该约束表示:传入的类型必须具有length属性
    interface ILength {length:number}
    function id<Type extends ILength}(value: Type):Type {
        consoloe.log(value.length)
        return value
    }
    ```

  - 多个泛型变量

  - ```ts
    function getProp<Type, Key extends keyof Type>(obj:Type, key: Key){
        return obj[key]
    }
    let person = {name: 'jack', age: 18}
    getProp(person,'name')
    
    //解释
    //1.添加了第二个类型变量 Key,两个类型变量之间用(,)逗号分隔
    //2.keyof关键字接收一个对象类型,生成其键名称(可能是字符串或数字)的联合类型
    //3.本示例中keyof Type实际上获取的是person对象所有键的联合类型,也就是:'name|age'
    //4.类型变量Key受Type约束,可以理解为: Key只能是Type所有键中的任意一个,或者说之恶能访问对象中存在的属性
    ```

  - 泛型接口

  - ```ts
    interface IdFunc<Type> {
        id: (value:Type) => Type
        ids: () => Type[]
    }
    let obj: IdFunc<number> = {
        id(value) {return value}
        ids() {return [1,2,3]}
    }
    //解释
    //1.在接口名称的后面添加<类型变量>,那么这个接口就变成了泛型接口
    //2.接口的类型变量,对接口中多有其他成员可见
    //3.使用泛型接口时,需要显示指定具体的类型,比如此处的IdFun<number>
    //4.此时,id方法的参数和返回值类型都是number,ids方法的返回值类型是number[]
    ```

  - 泛型类

  - ```react
    interface IState {count: number}
    interface IProps {maxLength: number}
    class InputCount extends React.Component<IProps,Istate>{
        state: IState = {count: 0}
        render(){
            return <div>{this.props.maxLength}</div>
        }
    }
    ```

  - 泛型工具类型

    - Partial<Type>

    - ```ts
      //用来构造一个类型,将Type所有属性设置为可选
      interface Props {
          id: string
          children: number[]
      }
      type PartialProps = Partial<Props>
      //构造出来的新类型PartialProps结构和Props相同,但所有属性都变为可选的
      ```

    - Readonly<Type>

    - ```ts
      //将Type的所有属性都设置为readonly
      interface Props {
          id: string
          children: number[]
      }
      type ReadonlyProps = Readonly<Props>
      ```

    - Pick<Type,Keys>

    - ```ts
      //从Type中选择一组属性来构造新类型
      interface Props {
          id: string
          title: string
          children: number[]
      }
      type PickProps = Pick<Props, 'id'|'title'>
      //1. Pick工具类型有两个类型变量:1表示选择谁的属性,2表示选择哪几个属性
      //2. 其中第二个类型变量,如果只选择一个则只传入该属性名即可
      //3. 第二个类型变量传入的属性只能是第一个类型变量中存在的属性
      ```

    - Record<Keys,Type>

    - ```ts
      //构造一个对象类型,属性键位Keys,属性类型为Type
      type RecordObj = Record<'a' | 'b' | 'c',string[]>
      let obj:RecordObj = {
          a: ['1'],
          b: ['2'],
          c: ['3']
      }
      ```

- 索引签名类型

  - 使用场景:当无法确定对象中有哪些属性

  - ```ts
    interface AnyObject {
        [key: string]: number
    }
    let obj: AnyObject = {
        a: 1,
        b: 2
    }
    
    //解释
    //1.使用[key:string]来约束该接口中允许出现的属性名称.表示只要是string类型的属性名称,都可以出现在对象中
    //2.这样,对象obj中就可以出现任意多个属性
    //3.key只是一个占位符,可以换成任意合法的变量名称
    //4. 隐藏的前置知识:JS对象({})的键是string类型的
    ```

# 类型声明文件

## 两种文件类型

- .ts文件
  - 既包含类型信息,又包含可执行代码
  - 可以被编译为.js文件,然后,执行代码
  - 用途:编写程序代码的地方
- .d.ts文件
  - 只包含类型信息的类型声明文件
  - 不会生成.js文件,仅用于提供类型信息
  - 用途: 为JS提供类型信息

## 类型声明文件来源

- 包自带
- DefinitelyTyped提供
  - DefinitelyTyped是一个github仓库,用来提供高质量的TypeScript类型声明
  - 可以通过npm来下载,包的名称格式为: @types/*
  - 比如, @types/react , @types/lodash

## 创建自己的类型声明文件

