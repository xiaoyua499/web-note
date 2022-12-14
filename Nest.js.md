# Nest.js

## 介绍nestjs

> Nestjs 是一个用于构建高效可扩展的一个基于[Node](https://so.csdn.net/so/search?q=Node&spm=1001.2101.3001.7020) js 服务端 应用程序开发框架并且完全支持[typeScript](https://so.csdn.net/so/search?q=typeScript&spm=1001.2101.3001.7020) 结合了 AOP 面向切面的编程方式
>
> nestjs 还是一个spring [MVC](https://so.csdn.net/so/search?q=MVC&spm=1001.2101.3001.7020) 的风格 其中有依赖注入 IOC 控制反转 都是借鉴了Angualr
>
> nestjs 的底层代码运用了 [express](https://so.csdn.net/so/search?q=express&spm=1001.2101.3001.7020) 和 Fastify 在他们的基础上提供了一定程度的抽象，同时也将其 API 直接暴露给开发人员。这样可以轻松使用每个平台的无数第三方模块


nest js 英文官网 [NestJS - A progressive Node.js framework](https://nestjs.com/)

nestjs 中文网 [NestJS 简介 | NestJS 中文文档 | NestJS 中文网](https://nestjs.bootcss.com/)

nestjs 中文网2 [Nest.js 中文文档](https://docs.nestjs.cn/)

### nestjs内置[框架](https://so.csdn.net/so/search?q=框架&spm=1001.2101.3001.7020)express 默认express

能够快速构建服务端应用程序，且学习成本非常低，容易上手

<img src="https://img-blog.csdnimg.cn/1d1b6d8f608f47d5b712c10b7befa9f4.png" style="zoom: 67%;" />

 express 文档[Express - 基于 Node.js 平台的 web 应用开发框架 - Express 中文文档 | Express 中文网](https://www.expressjs.com.cn/)

### nestjs唯二内置框架 Fastify

- **高性能：** 据我们所知，Fastify 是这一领域中最快的 web 框架之一，另外，取决于代码的复杂性，Fastify 最多可以处理每秒 3 万次的请求。
- **可扩展：** Fastify 通过其提供的钩子（hook）、插件和装饰器（decorator）提供完整的可扩展性。
- **基于 Schema：** 即使这不是强制性的，我们仍建议使用 [JSON Schema](http://json-schema.org/) 来做路由（route）验证及输出内容的序列化，Fastify 在内部将 schema 编译为高效的函数并执行。
- **日志：** 日志是非常重要且代价高昂的。我们选择了最好的日志记录程序来尽量消除这一成本，这就是 [Pino](https://github.com/pinojs/pino)!
- **对开发人员友好：** 框架的使用很友好，帮助开发人员处理日常工作，并且不牺牲性能和安全性。
- **支持 TypeScript：** 我们努力维护一个 [TypeScript](https://www.typescriptlang.org/) 类型声明文件，以便支持不断成长的 TypeScript 社区。

![](https://img-blog.csdnimg.cn/c3e25f041333448d90dee6f3cf8ae645.png)

## 前置知识

### IOC控制反转 DI依赖注入

在学习nestjs 之前需要先了解其设计模式

**IOC**

> Inversion of Control字面意思是[控制反转](https://so.csdn.net/so/search?q=控制反转&spm=1001.2101.3001.7020)，具体定义是高层模块不应该依赖低层模块，二者都应该依赖其抽象；抽象不应该依赖细节；细节应该依赖抽象。

DI

> [依赖注入](https://so.csdn.net/so/search?q=依赖注入&spm=1001.2101.3001.7020)（Dependency Injection）其实和IoC是同根生，这两个原本就是一个东西，只不过由于控制反转概念比较含糊（可能只是理解为容器控制对象这一个层面，很难让人想到谁来维护对象关系），所以2004年大师级人物Martin Fowler又给出了一个新的名字：“依赖注入”。 类A依赖类B的常规表现是在A中使用B的instance。

案例未使用控制反转和依赖注入之前的代码

```ts
class A {
    name: string
    constructor(name: string) {
        this.name = name
    }
}
 
 
class B {
    age:number
    entity:A
    constructor (age:number) {
        this.age = age;
        this.entity = new A('小满')
    }
}
 
const c = new B(18)
 
c.entity.name
```

我们可以看到，**B** 中代码的实现是需要依赖 **A** 的，**两者的代码耦合度非常高。当两者之间的业务逻辑复杂程度增加的情况下，维护成本与代码可读性都会随着增加，并且很难再多引入额外的模块进行功能拓展**。

为了解决这个问题可以使用IOC容器

```ts
class A {
    name: string
    constructor(name: string) {
        this.name = name
    }
}
 
 
class C {
    name: string
    constructor(name: string) {
        this.name = name
    }
}
//中间件用于解耦
class Container {
    modeuls: any
    constructor() {
        this.modeuls = {}
    }
    provide(key: string, modeuls: any) {
        this.modeuls[key] = modeuls
    }
    get(key) {
        return this.modeuls[key]
    }
}
 
const mo = new Container()
mo.provide('a', new A('小满1'))
mo.provide('c', new C('小满2'))
 
class B {
    a: any
    c: any
    constructor(container: Container) {
        this.a = container.get('a')
        this.c = container.get('c')
    }
}
 
new B(mo)
```

其实就是写了一个中间件，来收集依赖，主要是为了解耦，减少维护成本

### 装饰器

#### 1.什么是[装饰器](https://so.csdn.net/so/search?q=装饰器&spm=1001.2101.3001.7020)

> 装饰器是一种特殊的类型声明，他可以附加在类，方法，属性，参数上面

装饰器写法 **tips（需要开启一项配置）**

<img src="https://img-blog.csdnimg.cn/95a018ec2abe4c20adeea449534d0ded.png" style="zoom: 50%;" />

#### 2.类装饰器 主要是通过@符号添加装饰器

> 它会自动把class的[构造函数](https://so.csdn.net/so/search?q=构造函数&spm=1001.2101.3001.7020)传入到装饰器的第一个参数 target ,然后通过prototype可以自定义添加属性和方法

```ts
function decotators (target:any) {
    target.prototype.name = '小满'
}
 
@decotators
 
class Xiaoman {
 
    constructor () {
 
    }
 
}
 
const xiaoman:any = new Xiaoman()
 
console.log(xiaoman.name)
```

#### 3.属性装饰器

> 它会返回两个参数:1.原形对象2.属性的名称,同样使用@符号给属性添加装饰器

```ts
const currency: PropertyDecorator = (target: any, key: string | symbol) => {
    console.log(target, key)
}
 
 
class Xiaoman {
    @currency
    public name: string
    constructor() {
        this.name = ''
    }
    getName() {
        return this.name
    }
}
```

#### 4.参数装饰器

> 它会返回两个参数:1.原形对象 2.方法的名称 3.参数的位置从0开始,同样使用@符号给属性添加装饰器

```ts
const currency: ParameterDecorator = (target: any, key: string | symbol,index:number) => {
    console.log(target, key,index)
}
 
 
class Xiaoman {
    public name: string
    constructor() {
        this.name = ''
    }
    getName(name:string,@currency age:number) {
        return this.name
    }
}
```

#### 5.方法装饰器 

> 它会返回两个参数: 1.原形对象 2.方法的名称 3.属性描述符 可写对应writable，可枚举对应enumerable，可配置对应configurable,同样使用@符号给属性添加装饰器

```ts
const currency: MethodDecorator = (target: any, key: string | symbol,descriptor:any) => {
    console.log(target, key,descriptor)
}
 
 
class Xiaoman {
    public name: string
    constructor() {
        this.name = ''
    }
    @currency
    getName(name:string,age:number) {
        return this.name
    }
}
```

<img src="https://img-blog.csdnimg.cn/fa38175eb8974aa090c099c535c101d0.png" style="zoom:50%;" />

