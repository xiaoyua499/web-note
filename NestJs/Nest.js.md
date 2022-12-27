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

## nestjs cli

### 1.通过cli创建nestjs项目

```ts
npm i -g @nestjs/cli

nest new [项目名称]
```

启动项目 我们需要热更新 就启动npm run start:dev就可以了

### 2.目录介绍

1. **main.ts 入口文件主文件 类似于vue 的main.ts**

   1. 通过 NestFactory.create(AppModule) 创建一个app 就是类似于绑定一个根组件App.vue

   2.  app.listen(3000); 监听一个端口

      ```ts
      import { NestFactory } from '@nestjs/core';
      import { AppModule } from './app.module';
       
      async function bootstrap() {
        const app = await NestFactory.create(AppModule);
        await app.listen(3000);
      }
      bootstrap();
      ```

2. **Controller.ts 控制器**

   > 可以理解成vue 的路由
   >
   > private readonly appService: AppService 这一行代码就是依赖注入不需要实例化 appService 它内部会自己实例化的我们主需要放上去就可以了

  ```ts
  import { Controller, Get } from '@nestjs/common';
  import { AppService } from './app.service';

  @Controller()
  export class AppController {
    constructor(private readonly appService: AppService) {}

    @Get()
    getHello(): string {
      return this.appService.getHello();
    }
  }

  //-----------------------------------------------------
  //修改地址之后

  import { Controller, Get } from '@nestjs/common';
  import { AppService } from './app.service';

  @Controller('/get')
  export class AppController {
    constructor(private readonly appService: AppService) {}

    @Get('/hello')
    getHello(): string {
      return this.appService.getHello();
    }
  }
  ```

3. **app.service.ts**

   > 这个文件主要实现业务逻辑的 当然Controller可以实现逻辑，但是就是单一的无法复用，放到app.service有别的模块也需要就可以实现复用

```ts
import { Injectable } from '@nestjs/common';
 
@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

### 3.nestjs cli 常用命令

#### 1.nest --help 可以查看nestjs所有的命令

<img src="https://img-blog.csdnimg.cn/b56338e73ac148c4943f383fbebb9811.png" style="zoom: 80%;" />

#### 2.生成一个用户模块

1. 生成controller.ts

   `nest g co user`

2. 生成 module.ts

   `nest g mo user`

3. 生成service.ts

   `nest g s user`

以上步骤一个一个生成的太慢了我们可以直接使用一个命令生成CURD

` nest g resource user`

<img src="https://img-blog.csdnimg.cn/a2d4ced17e4a44ac9c2a2471307e80e9.png" style="zoom: 67%;" />

生成了一套标准的CURD 模板

##  RESTful 风格设计

> [RESTful](https://so.csdn.net/so/search?q=RESTful&spm=1001.2101.3001.7020) 是一种风格，在RESTful中，一切都被认为是资源，每个资源有对应的URL标识.
>
> 不是标准也不是协议，只是一种风格。当然你也可以不按照他的风格去写。

### 1.接口url

**传统接口**

http://localhost:8080/api/get_list?id=1

http://localhost:8080/api/delete_list?id=1

http://localhost:8080/api/update_list?id=1

**RESTful接口**

http://localhost:8080/api/get_list/1 查询 删除 更新

RESTful 风格一个接口就会完成 增删改差 他是通过不同的请求方式来区分的

查询GET

提交POST

更新 PUT PATCH

删除 DELETE

<img src="https://img-blog.csdnimg.cn/94ffe4f1c441413499126c3cece14f22.png" style="zoom:67%;" />

### 2.RESTful 版本控制 

> 一共有三种我们一般用第一种 更加语义化

| `URI Versioning`        | 版本将在请求的 URI 中传递（默认） |
| ----------------------- | --------------------------------- |
| `Header Versioning`     | 自定义请求标头将指定版本          |
| `Media Type Versioning` | 请求的`Accept`标头将指定版本      |

```ts
import { NestFactory } from '@nestjs/core';
import { VersioningType } from '@nestjs/common';
import { AppModule } from './app.module';
 
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.enableVersioning({
    type: VersioningType.URI,
  })
  await app.listen(3000);
}
bootstrap();
```

然后在user.controller 配置版本

Controller 变成一个对象 通过version 配置版本

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete, Version } from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
 
@Controller({
  path:"user",
  version:'1'
})
export class UserController {
  constructor(private readonly userService: UserService) {}

  @Post()
  create(@Body() createUserDto: CreateUserDto) {
    return this.userService.create(createUserDto);
  }

  @Get()
  // @Version('1')
  findAll() {
    return this.userService.findAll();
  }

  @Get(':id')
  findOne(@Param('id') id: string) {
    return this.userService.findOne(+id);
  }

  @Patch(':id')
  update(@Param('id') id: string, @Body() updateUserDto: UpdateUserDto) {
    return this.userService.update(+id, updateUserDto);
}
```

<img src="https://img-blog.csdnimg.cn/f703fe68dcac4daaa6fd309e0e92419f.png" style="zoom:67%;" />

###  3.Code码规范

​	200 OK

​	304 Not Modified 协商缓存了

​	400 Bad Request 参数错误

​	401 Unauthorized token错误

​	403 Forbidden referer origin 验证失败

​	404 Not Found 接口不存在

​	500 Internal Server Error 服务端错误

​	502 Bad Gateway 上游接口有问题或者服务器问题

## 控制器

### Controller Request （获取前端传过来的参数）

nestjs 提供了方法参数装饰器用来帮助我们快速获取参数 如下：

| @Request()              | req                               |
| ----------------------- | --------------------------------- |
| @Response()             | res                               |
| @Next()                 | next                              |
| @Session()              | req.session                       |
| @Param(key?: string)    | `req.params`/`req.params[key]`    |
| @Body(key?: string)     | `req.body`/`req.body[key]`        |
| @Query(key?: string)    | `req.query`/`req.query[key]`      |
| @Headers(name?: string) | `req.headers`/`req.headers[name]` |
| @HttpCode               |                                   |

调试工具可以使用postMan ApiFox 等

<img src="https://img-blog.csdnimg.cn/74fbf871d5004e58abe3fba981b2fbb2.png" style="zoom:80%;" />

### 1.获取get请求传参

> 可以使用Request装饰器 或者 Query 装饰器 跟express完全一样

<img src="https://img-blog.csdnimg.cn/9f673fd619b643ebad0d0d02cadb02e8.png" style="zoom:80%;" />

也可以使用Query 直接获取 不需要在通过req.query 了

![](https://img-blog.csdnimg.cn/3957dc61a1cc4719b92ae236a59d7c89.png)

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete, Version, Request, Query } from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
 
@Controller('user')
export class UserController {
  constructor(private readonly userService: UserService) { }
 
  @Get()
  find(@Query() query) {
    console.log(query)
    return { code: 200 }
  }
}
```

### 2.post 获取参数

>  可以使用Request装饰器 或者 Body 装饰器 跟express 完全一样

![](https://img-blog.csdnimg.cn/210ac37854714438a5f2c2b5385967b4.png)

或者直接使用Body 装饰器

![](https://img-blog.csdnimg.cn/d54ed57d83b24ae38377e1c0d0e17372.png)

也可以直接读取key

![](https://img-blog.csdnimg.cn/33454cfde24b46b6b0ede32eb89bbf82.png)

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete, Version, Request, Query } from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
 
@Controller('user')
export class UserController {
  constructor(private readonly userService: UserService) { }
 
  @Get()
  find(@Query() query) {
    console.log(query)
    return { code: 200 }
  }
 
  @Post()
  create (@Body() body) {
     
    console.log(body)
 
    return {
       code:200
    }
  }
}
```

### 3.动态路由

> 可以使用Request装饰器 或者 Param 装饰器 跟express 完全一样

![](https://img-blog.csdnimg.cn/b790aeebe8f444488f721491cb2581a9.png)

![](https://img-blog.csdnimg.cn/96a5bc5570df4d24a976347017d1517e.png)

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete, Version, Request, Query } from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
 
@Controller('user')
export class UserController {
  constructor(private readonly userService: UserService) { }
 
  @Get()
  find(@Query() query) {
    console.log(query)
    return { code: 200 }
  }
 
  @Post()
  create (@Body('name') body) {
     
    console.log(body)
 
    return {
       code:200
    }
  }
 
  @Get(':id')
  findId (@Param() param) {
     
    console.log(param)
 
    return {
       code:200
    }
  }
}
```

### 4.读取header信息

> 我在调试工具随便加了一个cookie

![](https://img-blog.csdnimg.cn/1618ecf69b214bd49fffeab19abb897c.png)

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete, Version, Request, Query, Ip, Header, Headers } from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
 
@Controller('user')
export class UserController {
  constructor(private readonly userService: UserService) { }
 
  @Get()
  find(@Query() query) {
    console.log(query)
    return { code: 200 }
  }
 
  @Post()
  create (@Body('name') body) {
     
    console.log(body)
 
    return {
       code:200
    }
  }
 
  @Get(':id')
  findId (@Headers() header) {
     
    console.log(header)
 
    return {
       code:200
    }
  }
}
```

### 5.状态码

> 使用 HttpCode 装饰器 控制接口返回的状态码 

![](https://img-blog.csdnimg.cn/d3fc2406b79f40c296f9bba4223b80c8.png)

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete, Version, Request, Query, Ip, Header, Headers, HttpCode } from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
 
@Controller('user')
export class UserController {
  constructor(private readonly userService: UserService) { }
 
  @Get()
  find(@Query() query) {
    console.log(query)
    return { code: 200 }
  }
 
  @Post()
  create (@Body('name') body) {
     
    console.log(body)
 
    return {
       code:200
    }
  }
 
  @Get(':id')
  @HttpCode(500)
  findId (@Headers() header) {
    return {
       code:500
    }
  }
}
```

## Session

> session 是服务器 为每个用户的浏览器创建的一个会话对象 这个session 会记录到 浏览器的 cookie 用来区分用户
>
> 我们使用的是nestjs 默认框架express 它也支持express 的插件 所以我们就可以安装express的session

1. 安装

​	`npm i express-session --save`

2. 需要智能提示可以装一个声明依赖

​	`npm i @types/express-session -D`

3. 在main.ts 引入 通过app.use 注册session

   ```ts
   import * as session from 'express-session'
    
    
   app.use(session())
   ```

**参数配置详解**

| secret  | 生成服务端session 签名 可以理解为加盐                        |
| ------- | ------------------------------------------------------------ |
| name    | 生成客户端cookie 的名字 默认 connect.sid                     |
| cookie  | 设置返回到前端 key 的属性，默认值为{ path: ‘/’, httpOnly: true, secure: false, maxAge: null }。 |
| rolling | 在每次请求时强行设置 cookie，这将重置 cookie 过期时间(默认:false) |

4. nestjs 配置

   ```ts
   import { NestFactory } from '@nestjs/core';
   import { VersioningType } from '@nestjs/common';
   import { AppModule } from './app.module';
   import * as session from 'express-session'
   async function bootstrap() {
     const app = await NestFactory.create(AppModule);
     app.enableVersioning({
       type: VersioningType.URI
     })
     app.use(session({ secret: "XiaoMan", name: "xm.session", rolling: true, cookie: { maxAge: null } }))
     await app.listen(3000);
   }
   bootstrap();
   ```

### 验证码案例 

前端技术栈： vue3+ts+element-plus+fetch

简单的绘制页面

```vue
<template>
     <div class="wraps">
          <el-form :label-position="labelPosition" label-width="100px" :model="formLabelAlign" style="max-width: 460px">
               <el-form-item label="账号">
                    <el-input v-model="formLabelAlign.name" />
               </el-form-item>
               <el-form-item label="密码">
                    <el-input type="password" v-model="formLabelAlign.password" />
               </el-form-item>
               <el-form-item label="验证码">
                    <div style="display:flex">
                         <el-input  v-model="formLabelAlign.code" />
                         <img @click="resetCode" :src="codeUrl" alt="">
                    </div>
               </el-form-item>
               <el-form-item>
                    <el-button @click="submit">登录</el-button>
               </el-form-item>
          </el-form>
     </div>
</template>
     
<script setup lang='ts'>
import { onMounted, reactive, ref } from 'vue';
 
const codeUrl = ref<string>('/api/user/code')
 
const resetCode = () => codeUrl.value = codeUrl.value + '?' + Math.random()
 
const labelPosition = ref<string>('right')
 
const formLabelAlign = reactive({
     name: "",
     password: "",
     code: ""
})
 
const submit = async () => {
     await fetch('/api/user/create', {
          method: "POST",
          body: JSON.stringify(formLabelAlign),
          headers: {
               'content-type': 'application/json'
          }
     }).then(res => res.json())
}
 
 
 
</script>
     
<style>
* {
     padding: 0;
     margin: 0;
}
 
.wraps {
     display: flex;
     justify-content: center;
     align-items: center;
     height: inherit;
}
 
html,
body,
#app {
     height: 100%;
}
</style>
```

<img src="https://img-blog.csdnimg.cn/c2d33a16861e41a8831fe77bb2e629e0.png" style="zoom:80%;" />

我们可以看到 session 已经存到了浏览器

![](https://img-blog.csdnimg.cn/18edc3438b4a401b9aa85091c64fa786.png)

跨域用了本地dev 解决

```ts
proxy:{
  '/api':{
    target:'http://localhost:3000/',
    changeOrigin:true,
    rewrite: path => path.replace(/^\/api/, ''),
  }
}
```

后端nestjs 验证码插件 svgCaptcha

`npm install svg-captcha -S`

```ts
import { Controller, Get, Post, Body, Param, Request, Query, Headers, HttpCode, Res, Req } from '@nestjs/common';
import { UserService } from './user.service';
import { CreateUserDto } from './dto/create-user.dto';
import { UpdateUserDto } from './dto/update-user.dto';
import * as svgCaptcha from 'svg-captcha';
@Controller('user')
export class UserController {
  constructor(private readonly userService: UserService) { }
  @Get('code')
  createCaptcha(@Req() req, @Res() res) {
    const captcha = svgCaptcha.create({
      size: 4,//生成几个验证码
      fontSize: 50, //文字大小
      width: 100,  //宽度
      height: 34,  //高度
      background: '#cc9966',  //背景颜色
    })
    req.session.code = captcha.text //存储验证码记录到session
    res.type('image/svg+xml')
    res.send(captcha.data)
  }
 
  @Post('create')
  createUser(@Req() req, @Body() body) {
    console.log(req.session.code, body)
    if (req.session.code.toLocaleLowerCase() === body?.code?.toLocaleLowerCase()) {
      return {
        message: "验证码正确"
      }
    } else {
      return {
        message: "验证码错误"
      }
    }
 
  }
}
```

![](https://img-blog.csdnimg.cn/f86ac9e613644378a63cec674e09a4d9.png)

## Providers(提供者)

**Providers**

> Providers 是 `Nest` 的一个基本概念。许多基本的 `Nest` 类可能被视为 `provider - service`,` repository`, `factory`, `helper` 等等。 他们都可以通过 `constructor` **注入**依赖关系。 这意味着对象可以彼此创建各种关系，并且“连接”对象实例的功能在很大程度上可以委托给 `Nest`运行时系统。 Provider 只是一个用 `@Injectable()` 装饰器注释的类。

### 1.基本用法

module 引入 service 在 providers 注入 

<img src="https://img-blog.csdnimg.cn/bb29915e1e9b4b14a8547cd41022e260.png" style="zoom:67%;" />

在Controller 就可以使用注入好的service 了 

<img src="https://img-blog.csdnimg.cn/7882400e265e48dcad985b9a63e85ef6.png" style="zoom:67%;" />

### 2.service 第二种用法(自定义名称)

第一种用法就是一个语法糖 其实他的全称是这样的

```ts
import { Module } from '@nestjs/common';
import { UserService } from './user.service';
import { UserController } from './user.controller';
 
@Module({
  controllers: [UserController],
  providers: [{
    provide: "Xiaoman",
    useClass: UserService
  }]
})
export class UserModule { }
```

![](https://img-blog.csdnimg.cn/2ec413ea8a1f4ae6a90f0a20ded1407c.png)

 自定义名称之后 需要用对应的Inject 取 不然会找不到的

![](https://img-blog.csdnimg.cn/2a731c48c2b445cdb3821a782a2222ca.png)

###  3.自定义注入值

> 通过 useValue

```ts
import { Module } from '@nestjs/common';
import { UserService } from './user.service';
import { UserController } from './user.controller';
 
@Module({
  controllers: [UserController],
  providers: [{
    provide: "Xiaoman",
    useClass: UserService
  }, {
    provide: "JD",
    useValue: ['TB', 'PDD', 'JD']
  }]
})
export class UserModule { }
```

![](https://img-blog.csdnimg.cn/a5803c28b336479b9b973e6655facca1.png)

![](https://img-blog.csdnimg.cn/c29fcb2806ab498a804762300e07f823.png)

###  3.工厂模式

> 如果服务 之间有相互的依赖 或者逻辑处理 可以使用 useFactory

```ts
import { Module } from '@nestjs/common';
import { UserService } from './user.service';
import { UserService2 } from './user.service2';
import { UserService3 } from './user.service3';
import { UserController } from './user.controller';
 
@Module({
  controllers: [UserController],
  providers: [{
    provide: "Xiaoman",
    useClass: UserService
  }, {
    provide: "JD",
    useValue: ['TB', 'PDD', 'JD']
  },
    UserService2,
  {
    provide: "Test",
    inject: [UserService2],
    useFactory(UserService2: UserService2) {
      return new UserService3(UserService2)
    }
  }
  ]
})
export class UserModule { }
```

![](https://img-blog.csdnimg.cn/c7e4901a7b6a4f1abf74984b457f7ba9.png)

![](https://img-blog.csdnimg.cn/7f1888320de249208a3e0e324bbe7903.png)

###  4.异步模式

> useFactory 返回一个promise 或者其他异步操作

```ts
import { Module } from '@nestjs/common';
import { UserService } from './user.service';
import { UserService2 } from './user.service2';
import { UserService3 } from './user.service3';
import { UserController } from './user.controller';
 
@Module({
  controllers: [UserController],
  providers: [{
    provide: "Xiaoman",
    useClass: UserService
  }, {
    provide: "JD",
    useValue: ['TB', 'PDD', 'JD']
  },
    UserService2,
  {
    provide: "Test",
    inject: [UserService2],
    useFactory(UserService2: UserService2) {
      return new UserService3(UserService2)
    }
  },
  {
    provide: "sync",
    async useFactory() {
      return await  new Promise((r) => {
        setTimeout(() => {
          r('sync')
        }, 3000)
      })
    }
  }
  ]
})
export class UserModule { }
```

![](https://img-blog.csdnimg.cn/90fb36c676484b698c83b7e62e4b4328.png)

## 模块@Module

> 每个 Nest 应用程序至少有一个模块，即根模块。根模块是 Nest 开始安排应用程序树的地方。事实上，根模块可能是应用程序中唯一的模块，特别是当应用程序很小时，但是对于大型程序来说这是没有意义的。在大多数情况下，您将拥有多个模块，每个模块都有一组紧密相关的**功能**

### 1.基本用法

当我们使用nest g res user 创建一个 CURD 模板的时候 nestjs 会自动帮我们引入模块

![](https://img-blog.csdnimg.cn/eeac62e95cd64df783f3f8ccfdc3c38f.png)

### 2.共享模块

例如 user 的 Service 想暴露给 其他模块使用就可以使用exports 导出该服务

![](https://img-blog.csdnimg.cn/41420a4be6c4497abec0871be0944af0.png)

由于App.modules 已经引入过该模块 就可以直接使用user 模块的 Service 

![](https://img-blog.csdnimg.cn/c275f874c27e4229ad2588e7aad0ad33.png)

![](https://img-blog.csdnimg.cn/36f88161516b4354ba735bd0185583c2.png)

###  3.全局模块 @Global()

> 我们给 user 模块添加 @Global() 他便注册为全局模块

![](https://img-blog.csdnimg.cn/87c46590a3b046f991b1241d932a8e99.png)

 在list 模块使用无须在module import 导入

![](https://img-blog.csdnimg.cn/06fa5e368a4e4c8283cd33704f0e8a19.png)

###  4.动态模块

> 动态模块主要就是为了给模块传递参数 可以给该模块添加一个静态方法 用来接受参数

![](https://img-blog.csdnimg.cn/e414eb0507d9419aa8098ddf5463d459.png)

```ts
import { Module, DynamicModule, Global } from '@nestjs/common'
 
 
 
interface Options {
    path: string
}
 
@Global()
@Module({
})
export class ConfigModule {
    static forRoot(options: Options): DynamicModule {
        return {
            module: ConfigModule,
            providers: [
                {
                    provide: "Config",
                    useValue: { baseApi: "/api" + options.path }
                }
            ],
            exports: [
                {
                    provide: "Config",
                    useValue: { baseApi: "/api" + options.path }
                }
            ]
        }
    }
} 
```

![](https://img-blog.csdnimg.cn/e269dc8dd1d14bb8a0345321b567921e.png)

![](https://img-blog.csdnimg.cn/c980f29751274936ba081a2384bffe93.png)

## 中间件

> 中间件是在路由处理程序 **之前** 调用的函数。 中间件函数可以访问请求和响应对象

中间件函数可以执行以下任务:

- 执行任何代码。
- 对请求和响应对象进行更改。
- 结束请求-响应周期。
- 调用堆栈中的下一个中间件函数。
- 如果当前的中间件函数没有结束请求-响应周期, 它必须调用 `next()` 将控制传递给下一个中间件函数。否则, 请求将被挂起。

### 1.创建一个依赖注入中间件

要求我们实现use 函数 返回 req res next 参数 如果不调用next 程序将被挂起

```ts
import {Injectable,NestMiddleware } from '@nestjs/common'
 
import {Request,Response,NextFunction} from 'express'
 
 
@Injectable()
export class Logger implements NestMiddleware{
  use (req:Request,res:Response,next:NextFunction) {
    console.log(req)
    next()
  }
}
```

使用方法 在模块里面 实现 configure 返回一个消费者 consumer 通过 apply 注册中间件 通过forRoutes 指定 Controller 路由

```ts
import { Module,NestModule,MiddlewareConsumer } from '@nestjs/common';
import { UserService } from './user.service';
import { UserController } from './user.controller';
import { Logger } from 'src/middleware';
@Module({
  controllers: [UserController],
  providers: [UserService],
  exports:[UserService]
})
export class UserModule implements NestModule{
  configure (consumer:MiddlewareConsumer) {
    consumer.apply(Logger).forRoutes('user')
  }
}
```

也可以指定 拦截的方法 比如拦截GET POST 等 forRoutes 使用对象配置

```ts
import { Module,NestModule,MiddlewareConsumer,RequestMethod } from '@nestjs/common';
import { UserService } from './user.service';
import { UserController } from './user.controller';
import { Logger } from 'src/middleware';
@Module({
  controllers: [UserController],
  providers: [UserService],
  exports:[UserService]
})
export class UserModule implements NestModule{
  configure (consumer:MiddlewareConsumer) {
    consumer.apply(Logger).forRoutes({path:'user',method:RequestMethod.GET})
  }
}
```

你甚至可以直接吧 UserController 塞进去

```ts
import { Module,NestModule,MiddlewareConsumer,RequestMethod } from '@nestjs/common';
import { UserService } from './user.service';
import { UserController } from './user.controller';
import { Logger } from 'src/middleware';
@Module({
  controllers: [UserController],
  providers: [UserService],
  exports:[UserService]
})
export class UserModule implements NestModule{
  configure (consumer:MiddlewareConsumer) {
    consumer.apply(Logger).forRoutes(UserController)
  }
}
```

### 2.全局中间件

注意全局中间件只能使用函数模式 案例可以做白名单拦截之类的

```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
 
 
const whiteList = ['/list']
 
function middleWareAll  (req,res,next) {
   
     console.log(req.originalUrl,'我收全局的')
 
     if(whiteList.includes(req.originalUrl)){
         next()
     }else{
         res.send('小黑子露出鸡脚了吧')
     }
 
     
}
 
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.use(middleWareAll)
  await app.listen(3000);
}
bootstrap();
```

### 3.接入第三方中间件 例如 cors 处理跨域

```ts
npm install cors

npm install @types/cors -D
```

```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as cors from 'cors'
 
const whiteList = ['/list']
 
function middleWareAll  (req,res,next) {
   
     console.log(req.originalUrl,'我收全局的')
 
     if(whiteList.includes(req.originalUrl)){
         next()
     }else{
         res.send({code:200})
     }
 
     
}
 
async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.use(cors())
  app.use(middleWareAll)
  await app.listen(3000);
}
bootstrap();
```

![](https://img-blog.csdnimg.cn/2047466ba6b540d986899fe1bcf190f0.png)

## 上传图片

### 静态目录

#### 1.主要会用到两个包

multer与@nestjs/platform-express (**nestJs自带了**)

multer  @types/multer 这两个需要安装

在upload Module 使用MulterModule register注册存放图片的目录

需要用到 multer 的 diskStorage 设置存放目录 extname 用来读取文件后缀 filename给文件重新命名

![](https://img-blog.csdnimg.cn/573e80de52e24ea1b2552fc72f97472c.png)

```ts
import { Module } from '@nestjs/common';
import { UploadService } from './upload.service';
import { UploadController } from './upload.controller';
import { MulterModule } from '@nestjs/platform-express'
import {diskStorage} from 'multer'
import { extname,join } from 'path';
@Module({
  imports: [MulterModule.register({
     storage:diskStorage({
        destination:join(__dirname,"../images"),
        filename:(_,file,callback) => {
           const fileName = `${new Date().getTime() + extname(file.originalname)}`
           return callback(null,fileName)
        }
     })
  })],
  controllers: [UploadController],
  providers: [UploadService]
})
export class UploadModule { }
```

#### 2.controller 使用

> 使用 UseInterceptors装饰器FileInterceptor是单个 读取字段名称 FilesInterceptor是多个参数 使用 UploadedFile 装饰器接受file 文件

![](https://img-blog.csdnimg.cn/875e7b3177814355ae0bc9386e9f422c.png)

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete,UseInterceptors,UploadedFile } from '@nestjs/common';
import { UploadService } from './upload.service';
import {FileInterceptor} from '@nestjs/platform-express'
@Controller('upload')
export class UploadController {
  constructor(private readonly uploadService: UploadService) {}
  @Post('album')
  @UseInterceptors(FileInterceptor('file'))
  upload (@UploadedFile() file) {
    console.log(file)
    return true
  }
}
```

#### 3.生成静态目录访问上传之后的图片

> useStaticAssets prefix 是虚拟前缀

```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import {NestExpressApplication} from '@nestjs/platform-express'
import { join } from 'path'
async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(AppModule);
  app.useStaticAssets(join(__dirname,'images'),{
     prefix:"/xiaoman"
  })
  await app.listen(3000);
}
bootstrap();
```

![](https://img-blog.csdnimg.cn/5c777aabd1144d6c94916b54450eaff9.png)

## 下载图片

### 1.download 直接下载

```ts
import { Controller, Post, UseInterceptors, UploadedFile, Get, Res } from '@nestjs/common';
import { UploadService } from './upload.service';
import { FileInterceptor, FilesInterceptor } from '@nestjs/platform-express'
import type { Response } from 'express'
import {join} from 'path'
@Controller('upload')
export class UploadController {
  constructor(private readonly uploadService: UploadService) { }
  @Post('album')
  @UseInterceptors(FileInterceptor('file'))
  upload(@UploadedFile() file) {
    console.log(file, 'file')
    return '峰峰35岁憋不住了'
  }
  @Get('export')
  downLoad(@Res() res: Response) {
    const url = join(__dirname,'../images/1662894316133.png')
    // res
    // console.log(url)
    res.download(url)
    // return  true
  }
}
```

![](https://img-blog.csdnimg.cn/6cbc40ebf6a548d8add5ce70a6fb567c.png)

### 2.使用文件流的方式下载

> 可以使用compressing把他压缩成一个zip

```ts
import {zip} from 'compressing' 
  


@Get('stream')
  async down (@Res() res:Response) {
    const url = join(__dirname,'../images/1662894316133.png')
    const tarStream  = new zip.Stream()
    await tarStream.addEntry(url)
    
    res.setHeader('Content-Type', 'application/octet-stream');
   
    res.setHeader(
      'Content-Disposition',  
      `attachment; filename=xiaoman`,
    );
 
    tarStream.pipe(res)
 
  }
```

前端接受流

```ts
const useFetch = async (url: string) => {
  const res = await fetch(url).then(res => res.arrayBuffer())
  console.log(res)
  const a = document.createElement('a')
  a.href = URL.createObjectURL(new Blob([res],{
    // type:"image/png"
  }))
  a.download = 'xiaman.zip'
  a.click()
}
 
const download = () => {
  useFetch('http://localhost:3000/upload/stream')
}
```

## RxJs

> **为什么要介绍RxJs 应为 在 Nestjs 已经内置了 RxJs 无需安装 并且Nestjs 也会有一些基于Rxjs提供的API**

![](https://img-blog.csdnimg.cn/0494e29cbd49435b9cb160f9bae1bb19.png)

> Rxjs 中文文档[Observable | RxJS 中文文档](https://cn.rx.js.org/class/es6/Observable.js~Observable.html)

### 概念

RxJs 使用的是观察者模式，用来编写异步队列和事件处理。

Observable 可观察的物件

Subscription 监听Observable

Operators 纯函数可以处理管道的数据 如 map filter concat reduce 等

### 案例

类似于迭代器 next 发出通知  complete通知完成

subscribe 订阅 observable 发出的通知 也就是一个观察者

```ts
import { Observable } from "rxjs";
 
//类似于迭代器 next 发出通知  complete通知完成
const observable = new Observable(subscriber=>{
    subscriber.next(1)
    subscriber.next(2)
    subscriber.next(3)
 
    setTimeout(()=>{
        subscriber.next(4)
        subscriber.complete()
    },1000)
})
 
observable.subscribe({
    next:(value)=>{
       console.log(value)
    }
})
```

### 案例2

interval 五百毫秒执行一次 pipe 就是管道的意思 管道里面也是可以去掉接口的支持处理异步数据 去处理数据 这儿展示 了 map 和 filter 跟数组的方法是一样的 最后 通过观察者 subscribe 接受回调

```ts
import { Observable, interval, take } from "rxjs";
import { map, filter,reduce,find,findIndex } from 'rxjs/operators'
 
 
const subs = interval(500).pipe(map(v => ({ num: v })), filter(v => (v.num % 2 == 0))).subscribe((e) => {
    console.log(e)
    if (e.num == 10) {
        subs.unsubscribe()
    }
})
```

![](https://img-blog.csdnimg.cn/f10b3ab637944c9eb60f2eeed2e6edd9.png)

### 案例3 

Rxjs 也可以处理事件 不过我们在[Nestjs](https://so.csdn.net/so/search?q=Nestjs&spm=1001.2101.3001.7020) 里面就不用操作DOM 了 你如果Angular 或则 Vue 框架看可以使用 fromEvent

```ts
import { Observable, interval, take,of,retry,fromEvent } from "rxjs";
import { map, filter,reduce,find,findIndex } from 'rxjs/operators'
 
const dom = fromEvent(document,'click').pipe(map(e=>e.target))
dom.subscribe((e)=>{
 
})
```

## 拦截器

### 响应拦截器

拦截器具有一系列有用的功能，这些功能受面向切面编程（AOP）技术的启发。它们可以：

- 在函数执行之前/之后绑定**额外的逻辑**
- 转换从函数返回的结果
- **转换**从函数抛出的异常
- 扩展基本函数行为
- 根据所选条件完全重写函数 (例如, 缓存目的)

我们现在没有给我们的[Nestjs](https://so.csdn.net/so/search?q=Nestjs&spm=1001.2101.3001.7020) 规范返回给前端的格式现在比较乱

![](https://img-blog.csdnimg.cn/99c5d7c52b0f49ae9d7055bc18050845.png)

 我们想给他返回一个标准的json 格式 就要给我们的数据做一个全局format

```ts
{
  data, //数据
  status:0,
  message:"成功",
  success:true
}
```

新建common 文件夹 创建 response.ts

Nest Js 配合 Rxjs 格式化数据

```ts
import { Injectable, NestInterceptor, CallHandler } from '@nestjs/common'
import { map } from 'rxjs/operators'
import {Observable} from 'rxjs'

interface data<T>{
    data:T
}
 
@Injectable()
export class Response<T = any> implements NestInterceptor {
    intercept(context, next: CallHandler):Observable<data<T>> {
        return next.handle().pipe(map(data => {
            return {
               data,
               status:0,
               success:true,
               message:"牛逼"
            }
        }))
    }
}
```

在main.ts 注册

`app.useGlobalInterceptors(new Response())`

![](https://img-blog.csdnimg.cn/1ff2a779632b4533afec8e947e43a7b7.png)

### 全局异常拦截器

common下面新建filter.ts

让我们创建一个异常过滤器，它负责捕获作为`HttpException`类实例的异常，并为它们设置自定义响应逻辑。为此，我们需要访问底层平台 `Request`和 `Response`。我们将访问`Request`对象，以便提取原始 `url`并将其包含在日志信息中。我们将使用 `Response.json()`方法，使用 `Response`对象直接控制发送的响应。

```ts 
 import { ExceptionFilter, Catch, ArgumentsHost,HttpException } from '@nestjs/common'
 
import {Request,Response} from 'express'
 
@Catch(HttpException)
export class HttpFilter implements ExceptionFilter {
    catch(exception:HttpException, host: ArgumentsHost) {
        const ctx = host.switchToHttp()
        const request = ctx.getRequest<Request>()
        const response = ctx.getResponse<Response>()
 
        const status = exception.getStatus()
 
        response.status(status).json({
           data:exception.message,
           time:new Date().getTime(),
           success:false,
           path:request.url,
           status
        })
    }
}
```

注册全局异常过滤器

`app.useGlobalFilters(new HttpFilter())`

![](https://img-blog.csdnimg.cn/093f7ce30d0f46af8d41bb7b59a58a0e.png)

![](https://img-blog.csdnimg.cn/63040ff529bd413695828930c6e82b80.png)

## 管道转换

![](https://img-blog.csdnimg.cn/img_convert/266c9dbe43307e152e42c5ca2ba8ede1.png)

### 管道

> 1.转换，可以将前端传入的数据转成成我们需要的数据
>
> 2.验证 类似于前端的rules 配置验证规则

我们先来讲一下转换 [Nestjs](https://so.csdn.net/so/search?q=Nestjs&spm=1001.2101.3001.7020) 提供了八个内置转换API

- `ValidationPipe`
- `ParseIntPipe`
- `ParseFloatPipe`
- `ParseBoolPipe`
- `ParseArrayPipe`
- `ParseUUIDPipe`
- `ParseEnumPipe`
- `DefaultValuePipe`

### 案例1 

接受的动态参数希望是一个number 类型 现在是string 

![](https://img-blog.csdnimg.cn/4140f756d639462d89315d8c4e15dbe3.png)

![](https://img-blog.csdnimg.cn/816ec2a26b944159ad79b3ea71f8553b.png)

这时候就可以通过内置的管道 去做转换

![](https://img-blog.csdnimg.cn/21d9cfb8ea104d989722aadf6c9721f3.png)

## 管道验证DTO

### 1.先创建一个pipe 验证管道

`nest g pi 文件名字`

### 2.安装验证器

`npm i --save class-validator class-transformer`

```ts
import {IsNotEmpty,IsString} from 'class-validator'
export class CreatePDto {
    @IsNotEmpty()//验证是否为空
    @IsString() //是否为字符串
    name:string;
 
    @IsNotEmpty()
    age:number
}
```

![](https://img-blog.csdnimg.cn/db5188291c334678a63ab6f005f2b0e3.png)

###  3.controller 使用管道 和定义类型

![](https://img-blog.csdnimg.cn/a6f44266fc7d4ec496e551f289afbc47.png)

### 4.实现验证transform

value 就是 前端传过来的数据 metaData 就是元数据 通过 metatype 可以去实例化这个类

![](https://img-blog.csdnimg.cn/c92a04bd2d8c424f856b2e01d173a6a0.png)

实例化DTO

![](https://img-blog.csdnimg.cn/e0a779cc334c4a008ccfb557f0c2e667.png)

通过 validate 验证 DTO 返回一个promise 的错误信息 如果有错误抛出

![](https://img-blog.csdnimg.cn/5b1d10b655054b1daee060c38ec5a7a2.png)

### 5.注册全局DTO验证管道 

跟自己写的效果基本类似

![](https://img-blog.csdnimg.cn/3fcb663b2b3c4f86a1fc754c67deda57.png)

![](https://img-blog.csdnimg.cn/9261c089d82143e3b5b2a9ea9890daff.png)

## 守卫（guard）

> 守卫有一个单独的责任。它们根据运行时出现的某些条件（例如权限，角色，[访问控制列表](https://so.csdn.net/so/search?q=访问控制列表&spm=1001.2101.3001.7020)等）来确定给定的请求是否由路由处理程序处理。这通常称为授权。在传统的 `Express` 应用程序中，通常由中间件处理授权(以及认证)。中间件是身份验证的良好选择，因为诸如 `token` 验证或添加属性到 `request` 对象上与特定路由(及其元数据)没有强关联。
>
> **tips 守卫在每个中间件之后执行，但在任何拦截器或管道之前执行。**

### 创建一个守卫 

`nest g gu [name]`

守卫要求实现函数 给定参数context**执行上下文** 要求返回布尔值

![](https://img-blog.csdnimg.cn/a49d71961d394ae585d4b49adccc9428.png)

### Controller 使用守卫

使用UseGuards 控制守卫

![](https://img-blog.csdnimg.cn/1e9b509cef964854bc577bbdd7382aef.png)

```ts
import { Controller, Get, Post, Body, Patch, Param, Delete ,UseGuards} from '@nestjs/common'; 
 
@Controller('guard')
@UseGuards(RoleGuard)
xxxxx
```

### 全局守卫

`app.useGlobalGuards(new RoleGuard())`

![](https://img-blog.csdnimg.cn/9c95a0eb42af4b2995e64ea85942c8f0.png)

###  针对角色控制守卫

SetMetadata 装饰器

第一个参数为key，第二个参数自定义我们的例子是数组存放的权限

![](https://img-blog.csdnimg.cn/566d426f4b7445beb1c12d1ec3dd4292.png)

guard 使用 Reflector 反射读取 setMetaData的值 去做判断这边例子是从url 判断有没有admin权限

```ts
import { CanActivate, ExecutionContext, Injectable } from '@nestjs/common';
import { Observable } from 'rxjs';
import { Reflector } from '@nestjs/core'
import type { Request } from 'express'
@Injectable()
export class RoleGuard implements CanActivate {
  constructor(private Reflector: Reflector) { }
  canActivate(
    context: ExecutionContext,
  ): boolean | Promise<boolean> | Observable<boolean> {
    const admin = this.Reflector.get<string[]>('role', context.getHandler())
    const request = context.switchToHttp().getRequest<Request>()
    if (admin.includes(request.query.role as string)) {
      return true;
    }else{
      return false
    }
   
  }
}
```

成功的 

![](https://img-blog.csdnimg.cn/c70c667130ab42a38c04de4739a92ce1.png)

失败的

![](https://img-blog.csdnimg.cn/bb6d9e8061e244ab966bdc7c4d248c71.png)

## 自定义装饰器

> 在[Nestjs](https://so.csdn.net/so/search?q=Nestjs&spm=1001.2101.3001.7020) 中我们使用了大量装饰器 decorator ，所以Nestjs 也允许我们去自定义装饰器。

### 案例1 自定义权限装饰器

生成装饰器 

`nest g d [name]`

```ts
import { SetMetadata } from '@nestjs/common';
 
export const Role = (role: string[]) => {
    console.log(role,1)
    return SetMetadata('role', role);
}
```

![](https://img-blog.csdnimg.cn/52e259dee68a42e7ac3e70b4b24c81e7.png)

###  案例2 自定义参数装饰器返回一个url

```ts
import { SetMetadata,createParamDecorator,ExecutionContext ,applyDecorators } from '@nestjs/common';
import type {Request} from 'express'
 
 
export const ReqUrl = createParamDecorator((data:string,ctx:ExecutionContext)=>{
    const req = ctx.switchToHttp().getRequest<Request>()
    return req.url
})
```

![](https://img-blog.csdnimg.cn/4e8b67be7037456a80af3fd5617f37a7.png)

## swagger接口文档

> swagger 用于提供给前端接口文档

安装命令如下

`npm install  @nestjs/swagger swagger-ui-express`

### 在main.ts 注册swagger

```ts
async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(AppModule);
  const options = new DocumentBuilder().setTitle('小满接口文档').setDescription('描述，。。。').setVersion('1').build()
  const document = SwaggerModule.createDocument(app,options)
  SwaggerModule.setup('/api-docs',app,document)
  await app.listen(3000);
}
bootstrap();
```

![](https://img-blog.csdnimg.cn/9a1be201b57242c6a44f1e3674c7e02f.png)

 打开对应的路径即可

![](https://img-blog.csdnimg.cn/236cfafcd81a4312a87bc859ddadd85e.png)

现在发现并没有分组很乱

### 可以使用ApiTags 添加分组

![](https://img-blog.csdnimg.cn/4ce8da2366364493878a9e79b665b898.png)

![](https://img-blog.csdnimg.cn/7bb7434d04ff49459170b280556c7847.png)

###  ApiOperation 接口描述

```ts
  @Get()
  @Role('admin')
  @ApiOperation({summary:"测试admin",description:"请求该接口需要amdin权限"})
  findAll(@ReqUrl('123') url:string) {
    console.log(url,'url')
    return this.guardService.findAll();
  }
```

![](https://img-blog.csdnimg.cn/4845cb968a7c453da9d705032199a596.png)

### ApiParam 动态参数描述

`@ApiParam({name:"id",description:"用户id",required:true})`

![](https://img-blog.csdnimg.cn/5f95ccb6c9e741d7ae1af44dc02bd7e7.png)

### ApiQuery 修饰get

` @ApiQuery({name:"xxxx",description:"bbb"})`

![](https://img-blog.csdnimg.cn/cf8a5e9a586e4eaa8641bb78b629729a.png)

### ApiProperty 定义Post

```ts
import { ApiProperty } from "@nestjs/swagger"
 
export class CreateGuardDto {
    @ApiProperty({ description: "姓名", example: "小满" })
    name: string
    @ApiProperty({ description:"年龄"})
    age: number
}
```

![](https://img-blog.csdnimg.cn/c4ef21446c05482d97adba5948163a0c.png)

###  ApiResponse 自定义返回信息

`@ApiResponse({status:403,description:"自定义返回信息"})`

![](https://img-blog.csdnimg.cn/7f6ee1894378478bbaf0c5013c4a25e5.png)

### ApiBearerAuth **jwt token**

 main.ts 增加 addBearerAuth()

![](https://img-blog.csdnimg.cn/3fdef8f1147e473ba12541556c13dc3f.png)

![](https://img-blog.csdnimg.cn/d888762b030344b480070d2a3235f2a9.png)

 添加token

![](https://img-blog.csdnimg.cn/5642cc7a3667402fbac54fdbca539d1c.png)

![](https://img-blog.csdnimg.cn/06048bfdd0414154b53c4f67ccb0312a.png)

请求头携带了 

### 其他装饰器 

![](https://img-blog.csdnimg.cn/999e492e1d7a45d0b5b51069477a936f.png)
