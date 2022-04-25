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

      