[TOC]



# Ajax

## 服务器的基本概念

1. **客户端与服务器**

   1. 服务器
   2. 客户端

2. **URL地址**

   1. 概念:

      URL(**统一资源定位符**),用于标识互联网上每个资源的唯一存放位置. 浏览器只有通过URL地址,才能正确的定位资源存放位置,从而成功访问到对应的资源

   2. 组成部分
      1. 客户端与服务器之间的**通信协议**
      2. 存有该资源的**服务器名称**
      3. 资源在服务器上具体的**存放位置**

3. **客户端与服务器的通信过程**

   1. 客户端与服务器之间的通宵过程,分为 **请求-处理-响应**
   2. 网页中的每一个资源,都是通过 **请求-处理-响应** 的方式从服务器获取回来的

4. **服务器在外提供了那些资源**

   1. 在网站中请求服务器的数据资源,则需要用到 **XML HttpRequerst** 对象`

   3. 资源的请求方式

      1. **get 请求** 通常用于获取服务器资源

         例如:根据URL 地址,从服务器获取HTML文件, CSS文件, JS文件, 图片文件, 数据资源等

      2. **post 请求** 通常用于向服务器提交信息

         例如:登录时向服务器提交的登录信息, 注册时向服务器提交的注册信息,添加用户是向服务器提交的用户信息等各种数据提交操作

## 了解Ajax

1. **什么是Ajax**

   Ajax全称 Asynchronous Javascript And XML (异步 JavaScript 和 XML), 在网页中利用 **XML HttpRequest** 对象和服务器进行数据交互的方式就是Ajax

2. **XML 简介**

   **XML(可扩展标记语言)**, 被设计用来传输和存储数据, 与HTML不同的是HTML中都是预定义标签,而XML中没有预定义标签, 全都是自定义标签, 用来表示一些数据
3. **jQuery中的Ajax**

   1. jQuery中发起Ajax请求中常用的三个方法:

      - $.get()
      - $.post()
      - $.ajax()

   2. **$.get() 函数语法**

      `$.get(url, [data], [callback])`

      | 参数名   | 参数类型   | 说明                         |
      | :------- | :--------- | :--------------------------- |
      | **url**  | **string** | 要请求的**资源地址**         |
      | data     | object     | 请求资源期间要**携带的参数** |
      | callback | function   | 请求成功是的**回调函数**     |

   3. **$.post() 函数语法**

      `$post(url, [data], [callback])`

      | 参数名   | 参数类型   | 说明                         |
      | :------- | :--------- | :--------------------------- |
      | **url**  | **string** | **提交数据的地址**           |
      | data     | object     | **要提交的地址**             |
      | callback | function   | 数据提交成功时的**回调函数** |

   4. **$ajax()函数的语法**

      ```javascript
      $.ajax({
         type: '', // 请求的方式，例如 GET 或 POST
         url: '',  // 请求的 URL 地址
         data: { },// 这次请求要携带的数据
         success: function(res) { } // 请求成功之后的回调函数
      })
      ```

## 接口

1. **接口的概念**

   使用 Ajax 请求数据时，**被请求的 URL 地址**，就叫做**数据接口（简称接口）**。同时，每个接口必须有**请求方式。**

2. **接口文档**

   1. **.** **什么是接口文档**

      接口文档，顾名思义就是**接口的说明文档，它是我们调用接口的依据**。好的接口文档包含了对接口URL，参数以及输出内容的说明，我们参照接口文档就能方便的知道接口的作用，以及接口如何进行调用。

   2. **接口文档的组成部分**

      1. **接口名称**：用来标识各个接口的简单说明，如登录接口，获取图书列表接口等。
2. **接口URL**：接口的调用地址。
      3. **调用方式**：接口的调用方式，如 GET 或 POST。
4. **参数格式**：接口需要传递的参数，每个参数必须包含参数名称、参数类型、是否必选、参数说明这4项内容。
      5. **响应格式**：接口的返回值的详细描述，一般包含数据名称、数据类型、说明3项内容。
6. 返回示例（可选）：通过对象的形式，例举服务器返回数据的结构。

## form表单与模板引擎

### form表单的基本使用

1. **表单的组成部分**

   1. 表单标签

   2. 表单域

      包含了文本框、密码框、隐藏域、多行文本框、复选框、单选框、下拉选择框和文件上传框等。

   3. 表单按钮

2. **<form>标签的属性**

   `<form>标签用来采集数据  <form>标签的属性则是用来规定如何把采集到的数据发送到服务器。`

   1. **action**

      1. action 属性用来规定当提交表单时，**向何处发送表单数据**。

         action 属性的值应该是后端提供的一个 URL 地址，这个 URL 地址专门负责接收表单提交过来的数据。

         当 <form> 表单在未指定 action 属性值的情况下，action 的默认值为当前页面的 URL 地址

         **注意**：当提交表单后，页面会立即跳转到 action 属性指定的 URL 地址

   2. **target**

      1. target 属性用来规定**在何处打开** **action URL**

         | 值         | 描述                           |
         | ---------- | ------------------------------ |
         | **_blank** | **在新窗口中打开**。           |
         | **_self**  | 默认。**在相同的框架中打开**。 |
         | _parent    | 在父框架集中打开。（很少用）   |
         | _top       | 在整个窗口中打开。（很少用）   |
         | framename  | 在指定的框架中打开。（很少用） |

   3. **method**

      1. method 属性用来规定**以何种方式**把表单数据提交到 action URL。

         它的可选值有两个，分别是 get 和 post。

         默认情况下，method 的值为 get，表示通过URL地址的形式，把表单数据提交到 action URL。

      2. **注意：**

         get 方式适合用来提交少量的、简单的数据。

         post 方式适合用来提交大量的、复杂的、或包含文件上传的数据。

         在实际开发中，<form> 表单的 post 提交方式用的最多，很少用 get。例如登录、注册、添加数据等表单操作，都需要使用 post 方式来提交表单。

   4. **enctype**

      1. enctype 属性用来规定在**发送表单数据之前如何对数据进行编码**。

         | 值                                | 描述                                                         |
         | --------------------------------- | ------------------------------------------------------------ |
         | application/x-www-form-urlencoded | 在发送前编码所有字符（默认）                                 |
         | multipart/form-data               | 不对字符编码。在使用包含文件上传控件的表单时，必须使用该值。 |
         | text/plain                        | 空格转换为 “+” 加号，但不对特殊字符编码。（很少用）          |

      2. **注意：**

         在涉及到**文件上传**的操作时，**必须**将 enctype 的值设置为 multipart/form-data

         如果表单的提交不涉及到文件上传操作，则直接将 enctype 的值设置为 application/x-www-form-urlencoded 即可！

3. **表单的同步提交及缺点**

   1. **什么是表单的同步提交**

      通过点击 submit 按钮，触发表单提交的操作，从而使页面跳转到 action URL 的行为，叫做表单的同步提交。

   2. **表单同步提交的缺点**

      1. `<form>表单同步提交后，整个页面会发生跳转，跳转到action URL所指向的地址，用户体验很差。`
      2. `<form>表单同步提交后，**页面之前的状态和数据会丢失。`

   3. 解决方案：**表单只负责采集数据，Ajax负责将数据提交到服务器**。

### 通过Ajax提交表单数据

1. **监听表单提交事件**

   ```JavaScript
   // 在 jQuery 中，可以使用如下两种方式，监听到表单的提交事件：
   $('#form1').submit(function(e) {
      alert('监听到了表单的提交事件')
   })
   
   $('#form1').on('submit', function(e) {
      alert('监听到了表单的提交事件')
   })
   ```

2. **阻止表单默认提交行为**

   ```javascript
   //当监听到表单的提交事件以后，可以调用事件对象的 event.preventDefault() 函数，来阻止表单的提交和页面的跳转，示例代码如下：
   $('#form1').submit(function(e) {
      // 阻止表单的提交和页面的跳转
      e.preventDefault()
   })
   
   $('#form1').on('submit', function(e) {
      // 阻止表单的提交和页面的跳转
      e.preventDefault()
   })
   ```

3. **快速获取表单中的数据**

   1. **serialize()函数**

      1. 为了简化表单中数据的获取操作，jQuery 提供了 serialize() 函数，其语法格式如下：

         `$(selector).serialize()`

      2. **注意：**

         1. serialize() 函数 可以一次性获取到表单中的所有的数据。
         2. 在使用 serialize() 函数快速获取表单数据时，**必须为每个表单元素添加** **name** **属性**

### 模板引擎

1. **模板引擎的基本概念**

   1. **什么是模板引擎**

      根据程序员指定的模板结构和数据，自动生成一个完整的HTML页面。

   2. **模板引擎的好处**
      1. 减少了字符串的拼接操作
      2. 使代码结构更清晰
      3. 使代码更易于阅读与维护

2. **art-template模板引擎**

   1. **art-template的安装**

      在浏览器中访问 http://aui.github.io/art-template/zh-cn/docs/installation.html 页面，找到下载链接后，鼠标右键，选择“**链接另存为**”，将 art-template 下载到本地，然后，通过 <script> 标签加载到网页上进行使用。

3. **art-template的使用步骤**

   ```JavaScript
   //1. 导入 art-template
   //2. 定义数据
   //3. 定义模板
   //4. 调用 template 函数
   //5. 渲染HTML结构
   <!-- 1. 导入模板引擎 -->
   <!-- 在 window 全局，多一个函数，叫做 template('模板的Id', 需要渲染的数据对象) -->
   <script src="./lib/template-web.js"></script>
   <body>
     <div id="container"></div>
     <!-- 3. 定义模板 -->
     <!-- 3.1 模板的 HTML 结构，必须定义到 script 中 -->
     <script type="text/html" id="tpl-user">
       <h1>{{name}} ------ {{age}}</h1>
     </script>
   
     <script>
       // 2. 定义需要渲染的数据
       var data = { name: 'zs', age:20 }
       // 4. 调用 template 函数
       var htmlStr = template('tpl-user', data)
       // 5. 渲染HTML结构
       $('#container').html(htmlStr)
     </script>
   
   </body>
   ```

4. **art-template标准语法**

   1. art-template 提供了 **{{ }}** 这种语法格式，在 {{ }} 内可以进行**变量输出**，或**循环数组**等操作，这种 {{ }} 语法在 art-template 中被称为标准语法。

   2. **输出**

      ```javascript
      {{value}}
      {{obj.key}}
      {{obj['key']}}
      {{a ? b : c}}
      {{a || b}}
      {{a + b}}
      //在 {{ }} 语法中，可以进行变量的输出、对象属性的输出、三元表达式输出、逻辑或输出、加减乘除等表达式输出。
      ```

   3. **原文输出**

      ```javascript
      {{@ value }}
      //如果要输出的 value 值中，包含了 HTML 标签结构，则需要使用原文输出语法，才能保证 HTML 标签被正常渲染。 
      ```

   4. **条件输出**

      ```javascript
      {{if value}} 按需输出的内容 {{/if}}
      
      {{if v1}} 按需输出的内容 {{else if v2}} 按需输出的内容 {{/if}}
      ```

   5. **循环输出**

      ```javascript
      //如果要实现循环输出，则可以在 {{ }} 内，通过 each 语法循环数组，当前循环的索引使用 $index 进行访问，当前的循环项使用 $value 进行访问。
      {{each arr}}
          {{$index}} {{$value}}
      {{/each}}
      ```

   6. **过滤器**

      ```javascript
      {{value | filterName}}
      //定义过滤器的基本语法如下：
      template.defaults.imports.filterName = function(value){/*return处理的结果*/}
      ```

5. **模板引擎的实现原理**

   1. **正则与字符串操作**

      1. **基本语法**

         exec() 函数用于检索字符串中的正则表达式的匹配。

         如果字符串中有匹配的值，则返回该匹配值，否则返回 null。

         ```javascript
         RegExpObject.exec(string)
         示例代码如下：
         var str = 'hello'
         var pattern = /o/
         // 输出的结果["o", index: 4, input: "hello", groups: undefined]
         console.log(pattern.exec(str)) 
         ```

      2. **分组**

         ```javascript
         //正则表达式中 ( ) 包起来的内容表示一个分组，可以通过分组来提取自己想要的内容，示例代码如下：
         var str = '<div>我是{{name}}</div>'
         var pattern = /{{([a-zA-Z]+)}}/
         var patternResult = pattern.exec(str)
         console.log(patternResult)
         // 得到 name 相关的分组信息
         // ["{{name}}", "name", index: 7, input: "<div>我是{{name}}</div>", groups: undefined]
         ```

      3. **字符串的replace函数**

         ```javascript
         //replace() 函数用于在字符串中用一些字符替换另一些字符，语法格式如下：
         var result = '123456'.replace('123', 'abc') // 得到的 result 的值为字符串 'abc456'
         //示例代码如下：
         var str = '<div>我是{{name}}</div>'
         var pattern = /{{([a-zA-Z]+)}}/
         var patternResult = pattern.exec(str)
         str = str.replace(patternResult[0], patternResult[1]) // replace 函数返回值为替换后的新字符串
         // 输出的内容是：<div>我是name</div>
         console.log(str)
         
         //使用while循环replace
         var str = '<div>{{name}}今年{{ age }}岁了</div>'
         var pattern = /{{\s*([a-zA-Z]+)\s*}}/
         var patternResult = null
         while (patternResult = pattern.exec(str)) {
             str = str.replace(patternResult[0], patternResult[1])
         }
         console.log(str)
         ```

      4. **replace替换为真值**

         ```javascript
         var data = { name: '张三', age: 20 }
         var str = '<div>{{name}}今年{{ age }}岁了</div>'
         var pattern = /{{\s*([a-zA-Z]+)\s*}}/
         var patternResult = null
         while ((patternResult = pattern.exec(str))) {
            str = str.replace(patternResult[0], data[patternResult[1]])
         }
         console.log(str)
         ```

   2. **实现简易的模板引擎**

      ```html
      <!-- 定义模板结构 -->
      <script type="text/html" id="tpl-user">
         <div>姓名：{{name}}</div>
         <div>年龄：{{ age }}</div>
         <div>性别：{{  gender}}</div>
         <div>住址：{{address  }}</div>
      </script>
      <!--预调用模板引擎-->
      <script>
         // 定义数据
         var data = { name: 'zs', age: 28, gender: '男', address: '北京顺义马坡' }
         // 调用模板函数
         var htmlStr = template('tpl-user', data)
         // 渲染HTML结构
         document.getElementById('user-box').innerHTML = htmlStr
          
          //封装template函数
          function template(id, data) {
            var str = document.getElementById(id).innerHTML
            var pattern = /{{\s*([a-zA-Z]+)\s*}}/
            var pattResult = null
            while ((pattResult = pattern.exec(str))) {
              str = str.replace(pattResult[0], data[pattResult[1]])
            }
            return str
      	}
      </script>
      ```

## Ajax加强

### XMLHttpRequest的基本使用

1. **XML HttpRequerst** (简称 xhr) 是浏览器提供的js成员, 通过他, 可以请求服务器上的数据资源

   `var xhrObj = new XML HttpRequerst()

2. **使用xhr发起GET请求**

   ```javascript
   // 1. 创建 XHR 对象
   var xhr = new XMLHttpRequest()
   // 2. 调用 open 函数，指定 请求方式 与 URL地址
   xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
   // 3. 调用 send 函数，发起 Ajax 请求
   xhr.send()
   // 4. 监听 onreadystatechange 事件
   xhr.onreadystatechange = function() {
       // 4.1 监听 xhr 对象的请求状态 readyState ；与服务器响应的状态 status
       if (xhr.readyState === 4 && xhr.status === 200) {
           // 4.2 打印服务器响应回来的数据
           console.log(xhr.responseText)
       }
   }
   ```

3. **了解xhr对象的readyState属性**

   1. XMLHttpRequest 对象的 readyState 属性，用来表示**当前** **Ajax** **请求所处的状态**。

      | **值** |     **状态**     | **描述**                                                     |
      | :----: | :--------------: | :----------------------------------------------------------- |
      |   0    |      UNSENT      | XMLHttpRequest 对象已被创建，但尚未调用 open方法。           |
      |   1    |      OPENED      | open() 方法已经被调用。                                      |
      |   2    | HEADERS_RECEIVED | send() 方法已经被调用，响应头也已经被接收。                  |
      |   3    |     LOADING      | 数据接收中，此时 response 属性中已经包含部分数据。           |
      | **4**  |     **DONE**     | **Ajax 请求完成**，这意味着数据传输已经彻底**完成**或**失败**。 |

4. **使用xhr发起带参数的GET请求**

   1. 使用 xhr 对象发起带参数的 GET 请求时，只需在调用 xhr.open 期间，为 URL 地址指定参数即可：

      `xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks**?id=1**')`这种在 URL 地址后面拼接的参数，叫做**查询字符串**。

5. **查询字符串**

   1. **什么是查询字符串**

      1. 定义：查询字符串（URL 参数）是指在 URL 的末尾加上用于向服务器发送信息的字符串（变量）。

      2. 格式：将英文的 **?** 放在URL 的末尾，然后再加上 **参数＝值** ，想加上多个参数的话，使用 **&** 符号进行分隔。以这个形式，可以将想要发送给服务器的数据添加到 URL 中。

         ```javascript
         // 不带参数的 URL 地址
         http://www.liulongbin.top:3006/api/getbooks
         // 带一个参数的 URL 地址
         http://www.liulongbin.top:3006/api/getbooks?id=1
         // 带两个参数的 URL 地址
         http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记
         ```

   2. **GET请求携带参数的本质**

      无论使用 $.ajax()，还是使用 $.get()，又或者直接使用 xhr 对象发起 GET 请求，当需要携带参数的时候，本质上，都是直接将参数以查询字符串的形式，追加到 URL 地址的后面，发送到服务器的。

6. **URL编码与解码**

   1. **什么是URL编码**
      1. URL 地址中，只允许出现英文相关的字母、标点符号、数字，因此，在 URL 地址中不允许出现中文字符。
      2. **URL编码的原则**：使用安全的字符（没有特殊用途或者特殊意义的可打印字符(英文字符)）去表示那些不安全的字符(非英文字符)。
   2. **如何对URL进行编码与解码**
      1. encodeURI() 编码的函数
      2. ldecodeURI() 解码的函数

7. **使用xh发起POST请求**

   ```javascript
   // 1. 创建 xhr 对象
   var xhr = new XMLHttpRequest()
   // 2. 调用 open()
   xhr.open('POST', 'http://www.liulongbin.top:3006/api/addbook')
   // 3. 设置 Content-Type 属性（固定写法）
   xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
   // 4. 调用 send()，同时将数据以查询字符串的形式，提交给服务器
   xhr.send('bookname=水浒传&author=施耐庵&publisher=天津图书出版社')
   // 5. 监听 onreadystatechange 事件
   xhr.onreadystatechange = function() {
       if (xhr.readyState === 4 && xhr.status === 200) {
           console.log(xhr.responseText)
       }
   }
   ```

### 数据交换格式

1. **什么是数据交换格式**

   1. 数据交换格式，就是**服务器端**与**客户端**之间进行**数据传输与交换的格式**
   2. 前端领域，经常提及的两种数据交换格式分别是 XML 和 **JSON**。其中 XML 用的非常少，所以，我们重点要学习的数据交换格式就是 **JSON**。

2. **XML**

   1. XML 的英文全称是 E**X**tensible **M**arkup **L**anguage，即**可扩展标记语言**。因此，XML 和 HTML 类似，也是一种标记语言。
   2. **. XML和HTML的区别**
      1. HTML 被设计用来描述网页上的**内容**，是网页内容的载体
      2. XML 被设计用来**传输和存储数据**，是数据的载体 

3. **JSON**

   1. **.** **什么是****JSON**

      1. 概念：JSON 的英文全称是 JavaScript Object Notation，即“JavaScript 对象表示法”。简单来讲，JSON 就是 Javascript 对象和数组的字符串表示法，它使用文本表示一个 JS 对象或数组的信息，因此，**JSON** **的本质是字符串**。
      2. 作用：JSON 是一种轻量级的文本数据交换格式，在作用上类似于 XML，专门用于存储和传输数据，但是 JSON 比 XML 更小、更快、更易解析。

   2. **JSON的两种结构**

      1. JSON 就是用字符串来表示 Javascript 的对象和数组。所以，JSON 中包含**对象**和**数组**两种结构，通过这两种结构的相互嵌套，可以表示各种复杂的数据结构。

      2. **对象结构**：对象结构在 JSON 中表示为 { } 括起来的内容。数据结构为 { key: value, key: value, … } 的键值对结构。其中，key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是数字、字符串、布尔值、null、数组、对象6种类型。

         ```javascript
         {
             "name": "zs",
             "age": 20,
             "gender": "男",
             "address": null,
             "hobby": ["吃饭", "睡觉", "打豆豆"]
         }
         ```

      3. **数组结构**：数组结构在 JSON 中表示为 [ ] 括起来的内容。数据结构为 [ "java", "javascript", 30, true … ] 。数组中数据的类型可以是数字、字符串、布尔值、null、数组、对象6种类型。

         ```javascript
         [ "java", "python", "php" ]
         [ 100, 200, 300.5 ]
         [ true, false, null ]
         [ { "name": "zs", "age": 20}, { "name": "ls", "age": 30} ]
         [ [ "苹果", "榴莲", "椰子" ], [ 4, 50, 5 ] ]
         ```

      4. **JSON语法注意事项**

         1. 属性名必须使用双引号包裹
         2. 字符串类型的值必须使用双引号包裹
         3. JSON 中不允许使用单引号表示字符串
         4. JSON 中不能写注释
         5. JSON 的最外层必须是对象或数组格式
         6. 不能使用 undefined 或函数作为 JSON 的值

      5. **JSON和JS对象的关系**

         ```javascript
         //JSON 是 JS 对象的字符串表示法，它使用文本表示一个 JS 对象的信息，本质是一个字符串。例如：
         
         //这是一个对象
         var obj = {a: 'Hello', b: 'World'}
         
         //这是一个 JSON 字符串，本质是一个字符串
         var json = '{"a": "Hello", "b": "World"}' 
         ```

      6. **JSON和JS对象的互转**

         ```javascript
         //从 JSON 字符串转换为 JS 对象，使用 JSON.parse() 方法：
         var obj = JSON.parse('{"a": "Hello", "b": "World"}')
         //结果是 {a: 'Hello', b: 'World'}
         
         //从 JS 对象转换为 JSON 字符串，使用 JSON.stringify() 方法：
         var json = JSON.stringify({a: 'Hello', b: 'World'})
         //结果是 '{"a": "Hello", "b": "World"}'
         ```

      7. **序列化和反序列化**

         1. 把数据对象转换为字符串的过程，叫做**序列化**，例如：调用 JSON.stringify() 函数的操作，叫做 JSON 序列化。
         2. 把字符串转换为数据对象的过程，叫做**反序列化**，例如：调用 JSON.parse() 函数的操作，叫做 JSON 反序列化。

### XMLHttpRequest Level2的新特性

1. **XMLHttpRequest Level2的新功能**

   1. 可以设置 HTTP 请求的时限

      ```javascript
      //有时，Ajax 操作很耗时，而且无法预知要花多少时间。如果网速很慢，用户可能要等很久。新版本的 XMLHttpRequest 对象，增加了 timeout 属性，可以设置 HTTP 请求的时限：
      xhr.timeout = 3000
      //上面的语句，将最长等待时间设为 3000 毫秒。过了这个时限，就自动停止HTTP请求。与之配套的还有一个 timeout 事件，用来指定回调函数：
      xhr.ontimeout = function(event){
           alert('请求超时！')
       }
      ```

      

   2. 可以使用 FormData 对象管理表单数据

      ```JavaScript
      //Ajax 操作往往用来提交表单数据。为了方便表单处理，HTML5 新增了一个 FormData 对象，可以模拟表单操作：
      
      // 1. 新建 FormData 对象
      var fd = new FormData()
      // 2. 为 FormData 添加表单项
      fd.append('uname', 'zs')
      fd.append('upwd', '123456')
      // 3. 创建 XHR 对象
      var xhr = new XMLHttpRequest()
      // 4. 指定请求类型与URL地址
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata')
      // 5. 直接提交 FormData 对象，这与提交网页表单的效果，完全一样
      xhr.send(fd)
      ```

      

   3. 可以上传文件

   4. 可以获得数据传输的进度信息





