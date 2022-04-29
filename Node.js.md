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
   
5. **Node.js** **中的模块化规范**

   1. Node.js 遵循了 CommonJS 模块化规范，CommonJS 规定了模块的特性和各模块之间如何相互依赖。
   2. CommonJS 规定：
      1. 每个模块内部，module 变量代表当前模块。
      2. module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。
      3. 加载某个模块，其实是加载该模块的 module.exports 属性。require() 方法用于加载模块。

## npm 与包

### 包

1. **什么是包**

   1. Node.js 中的**第三方模块**又叫做包。	
   2. **注意**：Node.js 中的包都是免费且开源的，不需要付费即可免费下载使用。
   3. 包是基于内置模块封装出来的，提供了更高级、更方便的 API，极大的提高了开发效率

2. **从哪里下载包**

   1. 从 https://www.npmjs.com/ 网站上搜索自己所需要的包
   2. 从 https://registry.npmjs.org/ 服务器上下载自己需要的包

3. **如何下载包**

   通过 **Node Package Manager（简称 npm 包管理工具）**，这个包管理工具随着 Node.js 的安装包一起被安装到了用户的电脑上。

4. **安装指定版本的包**

   1. 默认情况下，使用 npm install 命令安装包的时候，会自动安装最新版本的包。如果需要安装指定版本的包，可以在包名之后，通过 @ 符号指定具体的版本

5. **包管理配置文件**

   1. npm 规定，在项目根目录中，**必须**提供一个叫做 package.json 的包管理配置文件。用来记录与项目有关的一些配置信息。例如：
      1. 项目的名称、版本号、描述等
      2. 项目中都用到了哪些包
      3. 哪些包只在开发期间会用到
      4. 那些包在开发和部署时都需要用到
   2. **多人协作的问题**
      1. 遇到的问题：第三方包的体积过大，不方便团队成员之间共享项目源代码。
      2. 解决方案：**共享时剔除node_modules** ( 把 node_modules 文件夹，添加到 .gitignore 忽略文件中)
   3. **如何记录项目中安装了哪些包**
      1. 在项目根目录中，创建一个叫做 package.json 的配置文件，即可用来记录项目中安装了哪些包。从而方便剔除 node_modules 目录之后，在团队成员之间共享项目的源代码。
   4. **快速创建** **package.json**
      1. **npm init -y**
      2. **注意：**
         1. 上述命令只能在英文的目录下成功运行！所以，项目文件夹的名称一定要使用英文命名，不要使用中文，不能出现空格。
         2. 运行 npm install 命令安装包的时候，npm 包管理工具会自动把包的名称和版本号，记录到 package.json 中。
   5. **.** **一次性安装所有需要的包**
      1. **npm install 命令（或 npm i）**
   6. **卸载包**
      1. **npm uninstall 指定的包** 
   7. **devDependencies** **节点**
      1. 如果某些包**只在项目开发阶段**会用到，在**项目上线之后不会用到**，则建议把这些包记录到 devDependencies 节点中.与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到 dependencies 节点中。
      2. **npm i 包名 -D / npm install 包名 --save-dev**

6. **解决下包速度慢的问题**

   1. **淘宝** **NPM** **镜像服务器**

   2. **切换** **npm** **的下包镜像源**

      ```
      查看当前的下包镜像源
      npm config get registry
      将下包的镜像源切换为淘宝镜像源
      npm config set registry=http://registry.npm.taobao.org/
      ```

   3. **nrm**

      1. 为了更方便的切换下包的镜像源，我们可以安装 **nrm** 这个小工具，利用 nrm 提供的终端命令，可以快速查看和切换下包的镜像源。

         ```
         通过npm包管理器，将nrm安装为全局可用的工具
         npm i nrm -g
         查看所有可用的镜像源
         nrm ls
         将下包的镜像源切换为taobao镜像
         nrm use taobao
         ```

7. **包的分类**

   1. **项目包**

      1. 那些被安装到项目的 node_modules 目录中的包，都是项目包。
      2. 项目包又分为两类，分别是：
         1. 开发依赖包(npm i 包名 -D)（被记录到 devDependencies 节点中的包，只在开发期间会用到）
         2. 核心依赖包(npm i 包名)（被记录到 dependencies 节点中的包，在开发期间和项目上线之后都会用到）

   2. **全局包**

      1. 在执行 npm install 命令时，如果提供了 -g 参数，则会把包安装为全局包。全局包会被安装到 C:\Users\用户目录\AppData\Roaming\npm\node_modules 目录下。
      2. 注意：
         1. 只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。
         2. 判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可。

   3. **i5ting_toc**

      i5ting_toc 是一个可以把 md 文档转为 html 页面的小工具，使用步骤如下：

      ```
      将i5 ting toc安装为全局包
      npm install -g i5ting_toc
      调用i5 ting_toc,轻松实现md转html的功能
      i5 ting_toc-f要转换的md文件路径-o
      ```

8. **规范的包结构**

   1. 一个规范的包，它的组成结构，必须符合以下 3 点要求：
      1. 包必须以单独的目录而存在
      2. 包的顶级目录下要必须包含 package.json 这个包管理配置文件
      3. package.json 中必须包含 name，version，main 这三个属性，分别代表包的名字、版本号、包的入口。

9. **开发属于自己的包**

   1. **需要实现的功能**
   2. **初始化包的基本结构**
      1. 新建 itheima-tools 文件夹，作为包的根目录
      2. 在 itheima-tools 文件夹中，新建如下三个文件：
         1. package.json （包管理配置文件）
         2. index.js     （包的入口文件）
         3. README.md （包的说明文档）

   3. **将不同的功能进行模块化拆分**
   4. **编写包的说明文档**

10. **发布包**

   1. **注册** **npm** **账号**
      1. 访问 https://www.npmjs.com/ 网站，点击 sign up 按钮，进入注册用户界面
      2. 填写账号相关的信息：Full Name、Public Email、Username、Password
      3. 点击 Create an Account 按钮，注册账号
      4. 登录邮箱，点击验证链接，进行账号的验证

   2. **登录** **npm** **账号**
      1. npm 账号注册完成后，可以在终端中执行 npm login 命令，依次输入用户名、密码、邮箱后，即可登录成功。
      2. 注意：在运行 npm login 命令之前，必须先把下包的服务器地址切换为 npm 的官方服务器。否则会导致发布包失败！

   3. **把包发布到** **npm** **上**
      1. 将终端切换到包的根目录之后，运行 npm publish 命令，即可将包发布到 npm 上（注意：包名不能雷同）。

   4. **删除已发布的包**
      1. 运行 npm unpublish 包名 --force 命令，即可从 npm 删除已发布的包。
      2. 注意：
         1. npm unpublish 命令只能删除 72 小时以内发布的包
         2. npm unpublish 删除的包，在 24 小时内不允许重复发布
         3. 发布包的时候要慎重，尽量不要往 npm 上发布没有意义的包！


## 模块的加载机制

1. **优先从缓存中加载**
   1. **模块在第一次加载后会被缓存**。 这也意味着多次调用 require() 不会导致模块的代码被执行多次。
   2. 注意：不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。
2. **内置模块的加载机制**
   1. 内置模块是由 Node.js 官方提供的模块，内置模块的加载优先级最高。
3. **自定义模块的加载机制**
   1. 使用 require() 加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，如果没有指定 ./ 或 ../ 这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载。
   2. 同时，在使用 require() 导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件：
      1. 按照确切的文件名进行加载
      2. 补全 .js 扩展名进行加载
      3. 补全 .json 扩展名进行加载
      4. 补全 .node 扩展名进行加载
      5. 加载失败，终端报错
4. **第三方模块的加载机制**
   1. 如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块。
   2. 如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。
5. **目录作为模块**
   1. 当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式：
      1. 在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口
      2. 如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件。
      3. 如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'

## Express

### 初识 Express

1. **Express** **简介**

   1. **什么是** **Express**
      1. Express 是基于 Node.js 平台，快速、开放、极简的 Web 开发框架。
      2. Express 的作用和 Node.js 内置的 http 模块类似，是专门用来创建 Web 服务器的。
      3. **Express** **的本质**：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。
   2. **Express** **能做什么**
      1. 对于前端程序员来说，最常见的两种服务器，分别是：
         1.  Web 网站服务器：专门对外提供 Web 网页资源的服务器。
         2.  API 接口服务器：专门对外提供 API 接口的服务器。

2. **Express** **的基本使用**

   1. **安装**

      1. 在项目所处的目录中，运行如下的终端命令，即可将 express 安装到项目中使用：

         `npm i express@14.17.1`

   2. **创建基本的** **Web** **服务器**

      ```javascript
      // 1. 导入 express
      const express = require('express')
      // 2. 创建 web 服务器
      const app = express()
      // 3. 启动 web 服务器
      app.listen(80, () => {
        console.log('express server running at http://127.0.0.1')
      })
      ```

   3. **监听** **GET** **请求**

      1. 通过 app.get() 方法，可以监听客户端的 GET 请求，具体的语法格式如下：

         ```javascript
         //参数1：客户端请求的URL地址
         //参数2：请求对应的处理函数
         //req:请求对像（包，含了与请求相关的属性与方法）
         //res:响应对象（包含了与响应相关的属性与方法）
         app.get('请求URL',function(req,res){/*处理函数*/})
         ```

   4. **监听** **POST** **请求**

      1. 通过 app.post() 方法，可以监听客户端的 POST 请求，具体的语法格式如下：

         ```javascript
         //参数1：客户端请求的URL地址
         //参数2：请求对应的处理函数
         //req:请求对像（包，含了与请求相关的属性与方法）
         //res:响应对象（包含了与响应相关的属性与方法）
         app.post('请求URL',function(req,res){/*处理函数*/})
         ```

   5. **把内容响应给客户端**

      1. 通过 res.send() 方法，可以把处理好的内容，发送给客户端：

         ```javascript
         app.get('/user',(req,res)=>{
         	//向客户端发送JS0N对象
         	res.send({name:'zs',age:20,gender:''}
         })
         app.post('/user',(req,res)=>{
             //向客户端发送文本内容
             res.send('请求成功')
         })
         ```

   6. **获取** **URL** **中携带的查询参数**

      1. 通过 req.query 对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数：

         ```javascript
         //URL地址中，可以通过：参数名的形式，匹配动态参数值
         app.get('/user/:id',(req,res)=>{
             //req.params默认是一个空对象
             //里面存放着通过：动态匹配到的参数值
             console.log(req.params)
         })
         ```

3. **托管静态资源**

   1. **express.static()**

      `app.use(express.static('public'))`

      **注意：**Express 在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在 URL 中。

   2. **托管多个静态资源目录**

      1. 如果要托管多个静态资源目录，请多次调用 express.static() 函数

   3. **挂载路径前缀**

      1. 如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式：

         ``app.use('/public',express.static('public'))``

4. **nodemon**

   1. **为什么要使用** **nodemon**

      1. 在编写调试 Node.js 项目的时候，如果修改了项目的代码，则需要频繁的手动 close 掉，然后再重新启动，非常繁琐,使用 nodemon（https://www.npmjs.com/package/nodemon） 这个工具，它能够监听项目文件的变动，当代码被修改后，nodemon 会自动帮我们重启项目，极大方便了开发和调试。

   2. **安装** **nodemon**

      `npm i -g nodemon`

   3. **使用** **nodemon**

      `nodemon app.js`

### Express 路由

1. **路由的概念**

   1. **什么是路由**

      路由就是映射关系

2. **Express** **中的路由**

   1. 在 Express 中，路由指的是客户端的请求与服务器处理函数之间的映射关系。

   2. Express 中的路由分 3 部分组成，分别是请求的类型、请求的 URL 地址、处理函数，格式如下：

      `app.METHOD(请求的类型)(PATH(请求的URL地址), HANDLER(处理函数))`

3. **路由的匹配过程**

   1. 每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。
   2. 在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的 URL 同时匹配成功，则 Express 会将这次请求，转交给对应的 function 函数进行处理。
   3. 路由匹配的注意点：
      1. 按照定义的**先后顺序**进行匹配
      2. **请求类型**和**请求的URL**同时匹配成功，才会调用对应的处理函数

4. **路由的使用**

   1. **最简单的用法**

      ```javascript
      //挂载路由
      app.get('/', (req, res) => {
        res.send('hello world.')
      })
      app.post('/', (req, res) => {
        res.send('post request')
      })
      ```

   2. **模块化路由**

      1. 为了方便对路由进行模块化的管理，Express **不建议**将路由直接挂载到 app 上，而是推荐将路由抽离为单独的模块.将路由抽离为单独模块的步骤如下：

         1. 创建路由模块对应的 .js 文件

            ```JavaScript
            // 1. 导入 express
            const express = require('express')
            // 2. 创建路由对象
            const router = express.Router()
            
            
            ```

            

         2. 调用 express.Router() 函数创建路由对象

            ```JavaScript
            // 1. 导入路由模块
            const router = require('./03.router.js')
            ```

            

         3. 向路由对象上挂载具体的路由

            ```JavaScript
            // 3. 挂载具体的路由
            router.get('/user/list', (req, res) => {
              res.send('Get user list.')
            })
            router.post('/user/add', (req, res) => {
              res.send('Add new urse.')
            })
            ```

            

         4. 使用 module.exports 向外共享路由对象

            ```JavaScript
            // 4. 向外导出路由对象
            module.exports = router
            ```

            

         5. 使用 app.use() 函数注册路由模块

            ```JavaScript
            // 2. 注册路由模块
            app.use(router)
            ```

### Express 中间件

1. **中间件的概念**

   1. **什么是中间件**

      中间件（Middleware ），特指业务流程的中间处理环节。

   2. **Express** **中间件的调用流程**

      当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理

   3. **Express** **中间件的格式**

      1. Express 的中间件，本质上就是一个 **function** **处理函数**，Express 中间件的格式如下：

         `app.get('/', function(req, res, next) { next() })`

      2. 注意：中间件函数的形参列表中，必须包含 next 参数。而路由处理函数中只包含 req 和 res。

   4. **next** **函数的作用**

      **next** **函数**是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

2. **Express** **中间件的初体验**

   1. **定义中间件函数**

      ```javascript
      // // 定义一个最简单的中间件函数
      const mw = function(req, res, next){
        console.log('这是最简单的中间件函数');
        next()
      }
      ```

   2. **全局生效的中间件**

      1. 客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。通过调用 app.use(中间件函数)，即可定义一个全局生效的中间件

         `app.use(mw)`

      2. **定义全局中间件的简化形式**

         ```javascript
         app.use((req, res, next) => {
           console.log('这是最简单的中间件函数')
           next()
         })
         ```

   3. **中间件的作用**

      多个中间件之间，**共享同一份** **req** **和** **res**。基于这样的特性，我们可以在上游的中间件中，**统一**为 req 或 res 对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

   4. **定义多个全局中间件**

      可以使用 app.use() 连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用

   5. **局部生效的中间件**

      1. 不使用 app.use() 定义的中间件，叫做局部生效的中间件，示例代码如下：

      ```javascript
      // 1. 定义中间件函数
      const mw1 = (req, res, next) => {
        console.log('调用了局部生效的中间件')
        next()
      }
      
      // 2. 创建路由
      app.get('/', mw1, (req, res) => {
        res.send('Home page.')
      })
      ```

   6. **定义多个局部中间件**

      ```javascript
      //以下两种写法完全等价
      app.get('/', [mw1, mw2], (req, res) => {
        res.send('Home page.')
      })
      
      app.get('/', mw1, mw2, (req, res) => {
        res.send('Home page.')
      })
      ```

      1. **中间件的5个使用注意事项**
         1. 一定要在路由之前注册中间件
         2. 客户端发送过来的请求，可以连续调用多个中间件进行处理
         3. 执行完中间件的业务代码之后，不要忘记调用 next() 函数
         4. 为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
         5. 连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象

3. **中间件的分类**

   1. **应用级别的中间件**

      通过 app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件，叫做应用级别的中间件

   2. **路由级别的中间件**

      绑定到 express.Router() 实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，应用级别中间件是绑定到 app 实例上，路由级别中间件绑定到 router 实例上

      ```javascript
      const express = require('express')
      const app = express()
      const router = express.Router()
      
      //路由级别中间件
      router.use(function (req, res, next) {
          console.log('Time', Date.now())
          next()
      })
      
      app.use('/', router)
      ```

      

   3. **错误级别的中间件**

      1. 错误级别中间件的**作用**：专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。

      2. **格式**：错误级别中间件的 function 处理函数中，必须有 4 个形参，形参顺序从前到后，分别是 (err, req, res, next)。

         ```javascript
         // 1. 定义路由
         app.get('/', (req, res) => {
           throw new Error('服务器内部发生了错误')
           res.send('Home page.')
         })
         
         // 2. 定义错误级别的中间件，捕获整个项目的异常错误，从而防止程序的崩溃
         app.use((err, req, res, next) => {
           console.log('发生了错误' + err.message);
           res.send('Error:' + err.message)
         })
         ```

      3. **注意：**错误级别的中间件，必须注册在所有路由之后！

   4. **Express 内置的中间件**

      1. 自 Express 4.16.0 版本开始，Express 内置了 3 个常用的中间件，极大的提高了 Express 项目的开发效率和体验：

         1. express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）

         2.  express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

         3. express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）

            ```javascript
            //配置解析 application/json 格式数据的内置中间件
            app.use(express.json())
            //配置解析 application/x-www-form-urllencoded 格式数据的内置中间件
            app.use(express.urlencoded({ extended: false }))
            ```

            

   5. **第三方的中间件**

      1. 非 Express 官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，可以按需下载并配置第三方中间件，从而提高项目的开发效率。
      2. **注意：**Express 内置的 express.urlencoded 中间件，就是基于 body-parser 这个第三方中间件进一步封装出来的。
      
   6. **自定义中间件**
   
      1. **需求描述与实现步骤**
         1. 自己手动模拟一个类似于 express.urlencoded 这样的中间件，来解析 POST 提交到服务器的表单数据。
         2. 实现步骤：
            1. 定义中间件
            2. 监听 req 的 data 事件
            3. 监听 req 的 end 事件
            4. 使用 querystring 模块解析请求体数据
            5. 将解析出来的数据对象挂载为 req.body
            6. 将自定义中间件封装为模块

### 使用 Express 写接口

1. **创建基本的服务器**

   ```javascript
   // 导入 express 模块
   const express = require('express')
   // 创建 express 的服务器实例
   const app = express()
   
   // 调用 app.listen 方法，指定端口号并启动web服务器
   app.listen(80, function () {
     console.log('Express server running at http://127.0.0.1')
   })
   ```

   

2. **创建** **API** **路由模块**

   ```javascript
   // apiRouter.js [路由模块]
   const express = require('express')
   const apiRouter = express.Router()
   
   // bind your rouer here...
   
   module.exports = apiRouter
   
   //..............................
   
   // app.js [导入并注册路由模块]
   const apiRouter = require('./apiRouter.js')
   app.use('/api', apiRouter)
   ```

3. **编写** **GET** **接口**

   ```javascript
   router.get('/get', (req, res) => {
     //通过 req.query 获取客户端通过查询字符串, 发送到服务器的数据
     const query = req.query
     res.send({
       status: 0, //0 表示处理成功 1 表示处理失败
       msg: 'GET 请求成功', //状态的描述
       data: query // 需要响应的数据
     })
   })
   ```

4. **编写** **POST** **接口**

   ```javascript
   router.post('/post', (req, res) => {
     //通过 req.body 获取客户端通过查询字符串, 发送到服务器的数据
     const body = req.body
     res.send({
       status: 0, //0 表示处理成功 1 表示处理失败
       msg: 'post 请求成功', //状态的描述
       data: body // 需要响应的数据
     })
   })
   ```

5. **CORS** **跨域资源共享**

   1. **接口的跨域问题**

      1. 解决接口跨域问题的方案主要有两种：
         1. CORS（主流的解决方案，推荐使用）
         2.  JSONP（有缺陷的解决方案：只支持 GET 请求）

   2. **使用 cors 中间件解决跨域问题**

      1. cors 是 Express 的一个第三方中间件。通过安装和配置 cors 中间件，可以很方便地解决跨域问题。
      2. 使用步骤分为如下 3 步：
         1. 运行 npm install cors 安装中间件
         2. 使用 const cors = require('cors') 导入中间件
         3. 在路由之前调用 app.use(cors()) 配置中间件

   3. **什么是** **CORS**

      1. CORS （Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，**这些** **HTTP** **响应头决定浏览器是否阻止前端** **JS** **代码跨域获取资源**。
      2. 浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了 CORS 相关的 HTTP 响应头，就可以解除浏览器端的跨域访问限制。

   4. **CORS** **的注意事项**

      1. CORS 主要在服务器端进行配置。客户端浏览器**无须做任何额外的配置**，即可请求开启了 CORS 的接口。
      2. CORS 在浏览器中有兼容性。只有支持 XMLHttpRequest Level2 的浏览器，才能正常访问开启了 CORS 的服务端接口（例如：IE10+、Chrome4+、FireFox3.5+）。

   5. **CORS** **响应头部** **- Access-Control-Allow-Origin** 

      1. 响应头部中可以携带一个 **Access-Control-Allow-Origin** 字段，其语法如下:

         `Access-Control-Allow-Origin: <origin> | *`

         其中，origin 参数的值指定了允许访问该资源的外域 URL,如果指定了 Access-Control-Allow-Origin 字段的值为通配符 *****，表示允许来自任何域的请求

   6. **CORS** **响应头部** **- Access-Control-Allow-Headers**

      1. 默认情况下，CORS **仅**支持客户端向服务器发送如下的 9 个请求头：
         1. Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type （值仅限于 text/plain、multipart/form-data、application/x-www-form-urlencoded 三者之一）
         2. 如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过 Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败！

   7. **CORS** **响应头部** **- Access-Control-Allow-Methods**

      1. 默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。
      2. 如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP 方法。

   8. **CORS请求的分类**

      1. 客户端在请求 CORS 接口时，根据请求方式和请求头的不同，可以将 CORS 的请求分为两大类，分别是：
         1. 简单请求
            1. 同时满足以下两大条件的请求，就属于简单请求：
               1. 请求方式：GET、POST、HEAD 三者之一
               2. HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值application/x-www-form-urlencoded、multipart/form-data、text/plain）
         2. 预检请求
            1. 只要符合以下任何一个条件的请求，都需要进行预检请求：
               1. 请求方式为 GET、POST、HEAD 之外的请求 Method 类型
               2. 请求头中包含自定义头部字段
               3. 向服务器发送了 application/json 格式的数据
               4. 在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。
         3. **.** **简单请求和预检请求的区别**
            1. **简单请求的特点**：客户端与服务器之间只会发生一次请求。
            2. **预检请求的特点**：客户端与服务器之间会发生两次请求，OPTION 预检请求成功之后，才会发起真正的请求。

   9. **JSONP** **接口**

      1. **创建** **JSONP** **接口的注意事项**

         1. 如果项目中已经配置了 CORS 跨域资源共享，为了**防止冲突**，必须在配置 CORS 中间件之前声明 JSONP 的接口。否则 JSONP 接口会被处理成开启了 CORS 的接口

      2. **实现** **JSONP** **接口的步骤**

         1. 获取客户端发送过来的回调函数的名字
         2. 得到要通过 JSONP 形式发送给客户端的数据
         3. 根据前两步得到的数据，拼接出一个函数调用的字符串
         4. 把上一步拼接得到的字符串，响应给客户端的 <script> 标签进行解析执行

      3. **实现** **JSONP** **接口的具体代码**

         ```javascript
         app.get('/api/jsonp',(req,res)=>{
             //1。获取客户端发送过来的回调函数的名字
             const funcName req.query.callback
             //2.得到腰通过JSONP形式发送给客户端的数据
             const data =name:'zs',age:22
             //3.根据前两步得到的数据，拼接出一个函数调用的字符串
             const scriptstr =${funcName)(${JSON.stringify(data)})'
             //4.把上步拼接得到的字符串，响应给客户端的<script>标签进行解析执行
             res.send(scriptstr)
         )}
         ```

      4. **在网页中使用** **jQuery** **发起** **JSONP** **请求**

         1. 调用 $.ajax() 函数，提供 JSONP 的配置选项，从而发起 JSONP 请求，示例代码如下：

            ```javascript
            $('#btnJSONP').on('click',function (
                $.ajax({
                    method:'GET',
                    url:'http://127.0.0.1/api/jsonp',
                    dataType:'jsonp',//表示要发起JSONP的请求
                    success:function (res){
                    console.log(res)
            		}
                })
            })
            ```

            

