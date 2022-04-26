[TOC]



# Node.js

## 初识Node.js与内置模块

### 初识 Node.js



1. **Node.js 简介**

   1. **什么是 Node.js**

      Node.js 是一个基于 Chrome V8 引擎的 **JavaScript 运行环境**。

   2. **Node.js 中的 JavaScript运行环境**

      1. 浏览器是 JavaScript 的前端运行环境。
      2. Node.js 是 JavaScript 的后端运行环境。
      3. Node.js 中无法调用 DOM 和 BOM 等浏览器内置 API。

2. **在** **Node.js** **环境中执行** **JavaScript** **代码**

   1. 打开终端
   2. 输入 node 要执行的js文件的路径
   3. **终端中的快捷键**
      1. 使用 ↑ 键，可以快速定位到上一次执行的命令
      2. 使用 tab 键，能够快速补全路径
      3. 使用 esc 键，能够快速清空当前已输入的命令
      4. 输入 cls 命令，可以清空终端

### fs 文件系统模块

1. **什么是** **fs** **文件系统模块**

   1. fs 模块是 Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

      ```javascript
      //fs.readFile() 方法，用来读取指定文件中的内容
      //fs.writeFile() 方法，用来向指定的文件中写入内容
      //如果要在 JavaScript 代码中，使用 fs 模块来操作文件，则需要使用如下的方式先导入它：
      const fs = require('fs')
      ```

   2. **读取指定文件中的内容**

      1. **fs.readFile() 的语法格式**

         `fs.readFile(path[, options], callback)`

         1. 参数1：必选参数，字符串，表示文件的路径。
         2. 参数2：可选参数，表示以什么编码格式来读取文件。
         3. 参数3：必选参数，文件读取完成后，通过回调函数拿到读取的结果。

         ```javascript
         	fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
           // 2.1 打印失败的结果
           // 如果读取成功，则 err 的值为 null
           // 如果读取失败，则 err 的值为 错误对象，dataStr 的值为 undefined
           console.log(err)
           console.log('-------')
           // 2.2 打印成功的结果
           console.log(dataStr)
         })
         ```

      2. **判断文件是否读取成功**

         ```javascript
         const fs = require('fs')
         
         fs.readFile('./files/11.txt', 'utf8', function(err, dataStr) {
           if (err) {
             return console.log('读取文件失败！' + err.message)
           }
           console.log('读取文件成功！' + dataStr)
         })
         ```

   3. **向指定的文件中写入内容**

      1. **fs.writeFile( ) 的语法格式**

         `fs.writeFile(file, data[, options], callback)`

         1. 参数1：必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
         2. 参数2：必选参数，表示要写入的内容。
         3. 参数3：可选参数，表示以什么格式写入文件内容，默认值是 utf8。
         4. 参数4：必选参数，文件写入完成后的回调函数。

      2. **判断文件是否写入成功**

         ```javascript
         fs.writeFile('./files/3.txt', 'ojbk123', function(err) {
           // 2.1 如果文件写入成功，则 err 的值等于 null
           // 2.2 如果文件写入失败，则 err 的值等于一个 错误对象
           // console.log(err)
           if (err) {
             return console.log('文件写入失败！' + err.message)
           }
           console.log('文件写入成功！')
         })
         ```

   4. 

   5. **fs** **模块 -路径动态拼接的问题**

      1. 在使用 fs 模块操作文件时，如果提供的操作路径是以 ./ 或 ../ 开头的相对路径时，很容易出现路径动态拼接错误的问题。

         ```javascript
         //解决方案
         // __dirname 表示当前文件所处的目录
         // console.log(__dirname)
         
         fs.readFile(__dirname + '/files/1.txt', 'utf8', function(err, dataStr) {
           if (err) {
             return console.log('读取文件失败！' + err.message)
           }
           console.log('读取文件成功！' + dataStr)
         })
         ```

### path 路径模块

1. **什么是 path 路径模块**
   1. path 模块是 Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

   2. **path.join()** 方法，用来将多个路径片段拼接成一个完整的路径字符串

   3. **path.basename()** 方法，用来从路径字符串中，将文件名解析出来

      ```javascript
      //如果要在 JavaScript 代码中，使用 path 模块来处理路径，则需要使用如下的方式先导入它：
      const path = require('path')	
      ```

2. **路径拼接**

   1. **path.join()的语法格式**

      `path.join([...paths])`

      1. ...paths <string> 路径片段的序列
      2. 返回值: <string>

3. **获取路径中的文件名**

   1. **path.basename****()** **的语法格式**

      `path.basename(path[, exr])`

      1. path <string> 必选参数，表示一个路径的字符串

      2. ext <string> 可选参数，表示文件扩展名

      3. 返回: <string> 表示路径中的最后一部分

         ```javascript
         const path = require('path')
         
         // 定义文件的存放路径
         const fpath = '/a/b/c/index.html'
         
         const fullName = path.basename(fpath)
         console.log(fullName)
         
         const nameWithoutExt = path.basename(fpath, '.html')
         console.log(nameWithoutExt)
         ```

         

4. **获取路径中的文件扩展名**

   1. **path.extname()的语法格式**

      `path.extname(path)`

      1. path <string>必选参数，表示一个路径的字符串
      2. 返回: <string> 返回得到的扩展名字符串

   2. **path.extname()的代码示例**

      ```javascript
      const path = require('path')
      
      // 这是文件的存放路径
      const fpath = '/a/b/c/index.html'
      
      const fext = path.extname(fpath)
      console.log(fext)  
      ```

### http 模块

1. **什么是** **http** **模块**

   1. http 模块是 Node.js 官方提供的、用来创建 web 服务器的模块。通过 http 模块提供的 http.createServer() 方法，就能方便的把一台普通的电脑，变成一台 Web 服务器，从而对外提供 Web 资源服务。

   2. 如果要希望使用 http 模块创建 Web 服务器，则需要先导入它：

      `const http = require('http')`

   3.  在 Node.js 中，我们不需要使用 IIS、Apache 等这些第三方 web 服务器软件。因为我们可以基于 Node.js 提供的 http 模块，**通过几行简单的代码，就能轻松的手写一个服务器软件**，从而对外提供 web 服务。

2. **服务器相关的概念**

   1. **IP** **地址**

      1. **IP** **地址**就是互联网上每台计算机的唯一地址，因此 IP 地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方 IP 地址的前提下，才能与对应的电脑之间进行数据通信。

         IP 地址的格式：通常用“点分十进制”表示成（a.b.c.d）的形式，其中，a,b,c,d 都是 0~255 之间的十进制整数。例如：用点分十进表示的 IP地址（192.168.1.1）

      2. 注意：

         1. **互联网中每台** **Web** **服务器，都有自己的** **IP** **地址**，例如：大家可以在 Windows 的终端中运行 ping www.baidu.com 命令，即可查看到百度服务器的 IP 地址。
         2. 在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入 127.0.0.1 这个 IP 地址，就能把自己的电脑当做一台服务器进行访问了。

   2. **域名和域名服务器**

      1. 尽管 IP 地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套字符型的地址方案，即所谓的**域名（Domain Name）地址**。
      2. IP地址和域名是一一对应的关系，这份对应关系存放在一种叫做**域名服务器**(DNS，Domain name server)的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，**域名服务器就是提供** **IP** **地址和域名之间的转换服务的服务器**。
      3. 注意：
         1. 单纯使用 IP 地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便。
         2. 在开发测试期间， 127.0.0.1 对应的域名是 localhost，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。

   3. **端口号**

      1. 在一台电脑中，可以运行成百上千个 web 服务。每个 web 服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 web 服务进行处理。
      2. 注意：
         1. 每个端口号不能同时被多个 web 服务占用。
         2. 在实际应用中，URL 中的 80 端口可以被省略。

   4. **创建最基本的** **web** **服务器**

      1. **创建** **web** **服务器的基本步骤**

         1. 导入 http 模块

            `const http = rewuire('http')`

         2. 创建 web 服务器实例

            `const server = http.createSever()`

         3. 为服务器实例绑定 **request** 事件，监听客户端的请求

            ```javascript
            //使用服务器实例的 on() 方法, 为服务器绑定一个 request 事件
            server.on('request', function (req, res) {
                //只要有客户端来请求我们自己的服务器，就会触发 request事件，从而调用这个事件处理函数
              console.log('Someone visit our web server.')
            })
            ```

            

         4. 启动服务器

            ```javascript
            //调用server.listen(端口号，cb回调)方法，即可启动web服务器
            server.listen(8080, function () {  
              console.log('server running at http://127.0.0.1:8080')
            })
            ```

      2. **req** **请求对象**

         ```javascript
         server.on('request', (req, res) => {
           // req.url 是客户端请求的 URL 地址
           const url = req.url
           // req.method 是客户端请求的 method 类型
           const method = req.method
           const str = `Your request url is ${url}, and request method is ${method}`
           console.log(str)
         })
         ```

      3. **res** **响应对象**

         ```javascript
          // 调用 res.end() 方法，向客户端响应一些内容
          res.end(str)
         ```

      4. **解决中文乱码问题**

         ```javascript
         server.on('request', (req, res) => {
           // 定义一个字符串，包含中文的内容
           const str = `您请求的 URL 地址是 ${req.url}，请求的 method 类型为 ${req.method}`
           // 调用 res.setHeader() 方法，设置 Content-Type 响应头，解决中文乱码的问题
           res.setHeader('Content-Type', 'text/html; charset=utf-8')
           // res.end() 将内容响应给客户端
           res.end(str)
         })
         ```

      5. **根据不同的** **url** **响应不同的** **html** **内容**

         ```javascript
         server.on('request', (req, res) => {
           // 1. 获取请求的 url 地址
           const url = req.url
           // 2. 设置默认的响应内容为 404 Not found
           let content = '<h1>404 Not found!</h1>'
           // 3. 判断用户请求的是否为 / 或 /index.html 首页
           // 4. 判断用户请求的是否为 /about.html 关于页面
           if (url === '/' || url === '/index.html') {
             content = '<h1>首页</h1>'
           } else if (url === '/about.html') {
             content = '<h1>关于页面</h1>'
           }
           // 5. 设置 Content-Type 响应头，防止中文乱码
           res.setHeader('Content-Type', 'text/html; charset=utf-8')
           // 6. 使用 res.end() 把内容响应给客户端
           res.end(content)
         })
         ```

## 模块化

### 模块化的基本概念

1. **什么是模块化**
   1. **模块化**是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。
   2. **编程领域中的模块化**
      1. 编程领域中的模块化，就是**遵守固定的规则**，把一个大文件拆成独立并互相依赖的多个小模块。
      2. 把代码进行模块化拆分的好处：
         1. 提高了代码的复用性
         2. 提高了代码的可维护性
         3. 可以实现按需加载
2. **模块化规范**
   1. **模块化规范**就是对代码进行模块化的拆分与组合时，需要遵守的那些规则。
   2. **模块化规范的好处**：大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己。

### **Node.js** 中的模块化

1. **Node.js 中模块的分类**

   1. Node.js 中根据模块来源的不同，将模块分为了 3 大类，分别是：
      - 内置模块（内置模块是由 Node.js 官方提供的，例如 fs、path、http 等）
      - 自定义模块（用户创建的每个 .js 文件，都是自定义模块）
      - 第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载）

2. **加载模块**

   1. 使用强大的 require() 方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用。例如：

      ```javascript
      //1.加载内置的fs模块
      const fs require('fs')
      
      //2.加载用户的自定义模块
      const custom require('./custom.js')
      
      //3.加载第三方模块（关于第三方模块的下载和使用，会在后面的课程中进行专门的讲解）
      const moment require('moment')
      
      //注意：使用 require() 方法加载其它模块时，会执行被加载模块中的代码。
      ```

3. **Node.js** **中的模块作用域**

   1. **什么是模块作用域**

      和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做**模块作用域**。

   2. **模块作用域的好处**

      防止了全局变量污染的问题

4. **向外共享模块作用域中的成员**

   1. **module 对象**

      ```javascript
      //在每个 .js 自定义模块中都有一个 module 对象，它里面存储了和当前模块有关的信息，打印如下：
      Module {
        id: '.',
        path: 'D:\\Desktop\\Web\\Node.js\\day2\\code',
        exports: {},
        filename: 'D:\\Desktop\\Web\\Node.js\\day2\\code\\10.演示module对象.js',
        loaded: false,
        children: [],
        paths: [
          'D:\\Desktop\\Web\\Node.js\\day2\\code\\node_modules',
          'D:\\Desktop\\Web\\Node.js\\day2\\node_modules',
          'D:\\Desktop\\Web\\Node.js\\node_modules',
          'D:\\Desktop\\Web\\node_modules',
          'D:\\Desktop\\node_modules',
          'D:\\node_modules'
        ]
      }
      ```

   2. **module.exports 对象**

      1. 在自定义模块中，可以使用 module.exports 对象，将模块内的成员共享出去，供外界使用。外界用 require() 方法导入自定义模块时，得到的就是 module.exports 所指向的对象。

   3. **共享成员时的注意点**

      使用 require() 方法导入模块时，导入的结果，**永远以** **module.exports** **指向的对象为准**。

   4. **exports** **对象**

      由于 module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了 exports 对象。默认情况下，exports 和 module.exports 指向同一个对象。最终共享的结果，还是以 module.exports 指向的对象为准。

   5. **exports** **和** **module.exports** **的使用误区**

      1. require() 模块时，得到的永远是 module.exports 指向的对象
      2. **注意：**为了防止混乱，建议大家不要在同一个模块中同时使用 exports 和 module.exports

