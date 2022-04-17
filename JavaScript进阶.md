[TOC]



# JavaScript进阶 

## Web API

1. API是为程序员提供的接口,帮助实线某种功能
2. Web API 主要是针对浏览器提供的接口,主要是针对浏览器做交互效果
3. Web API 一般都有输入和输出(函数的传参和返回值),Web API很多都是方法(函数)

## DOM

1. ### **DOM 简介**

   **文档对象模型**(简称**DOM**),是W3C组织推荐的处理可扩展标记语言(HTML或者XML)的标准**编程接口**

2. ### **DOM 树**

   1. 文档:一个页面就是一个文档,DOM中使用document表示

   2. 元素:页面中的所有标签都是元素,DOM中使用element表示

   3. 节点:网页中所有的内容都是节点(标签,属性,文本,注释等),DOM中使用node表示

      **以上内容都可以看做对象**

3. ### **获取元素**

   1. **根据ID获取**

      1. 使用**getElementById( )**方法可以获取带有**ID**的元素对象

         ```javascript
         // 1. 因为我们文档页面从上往下加载，所以先得有标签 所以我们script写到标签的下面
         // 2. get 获得 element 元素 by 通过 驼峰命名法 
         // 3. 参数 id是大小写敏感的字符串
         var time = document.getElementById('time');
         console.log(time);
         // 4. 返回的是一个元素对象
         console.log(typeof time);
         // 5. console.dir 打印我们返回的元素对象 更好的查看里面的属性和方法
         console.dir(time);
         ```

   2. **根据标签名获取**

      1. 使用 **getElementsByTagName( )** 方法可以返回带有指定标签签名的**对象的合集**

      2. 还可以使用 **element.getElementsByTagName('标签名')** 获取某个元素(父元素)内部所有指定标签名的子元素

         ```javascript
         // 1.返回的是 获取过来元素对象的集合 以伪数组的形式存储的
         var lis = document.getElementsByTagName('li');
         console.log(lis);
         console.log(lis[0]);
         // 2. 我们想要依次打印里面的元素对象我们可以采取遍历的方式
         for (var i =0; i < lis.length; i++){
             console.log(lis[i]);
         }
         // 3. 如果页面中只有一个li 返回的还是伪数组的形式 
         // 4. 如果页面中没有这个元素 返回的是空的伪数组的形式
         // 5. element.getElementsByTagName('标签名'); 父元素必须是指定的单个元素
         // var ol = document.getElementsByTagName('ol'); // [ol]
         // console.log(ol[0].getElementsByTagName('li'));
         var ol = document.getElementById('ol');
         console.log(ol.getElementsByTagName('li'));
         //注意:父元素必须是单个对象(必须指明是那个元素对象).获取的时候不包括父元素自己	
         ```

      3. 通过 **HTML5 新增**的获取方法获取

         ```javascript
         // 1. getElementsByClassName 根据类名获得某些元素集合
         var boxs = document.getElementsByClassName('box');
         console.log(boxs);
         // 2. querySelector 返回指定选择器的第一个元素对象  切记 里面的选择器需要加符号 .box  #nav
         var firstBoxs = document.querySelector('.box');
         console.log(firstBoxs);
         var nav = document.querySelector('#nav');
         console.log(nav);
         var li = document.querySelector('li');
         console.log(li);
         // 3. querySelectorAll()返回指定选择器的所有元素对象集合
         var allBox = document.querySelectorAll('.box');
         console.log(allBox);
         var lis = document.querySelectorAll('li');
         console.log(lis);
         ```

   3. **获取特殊元素**

      1. 获取**body元素**

         ```javascript
         var bodyEle = document.body;
         console.log(bodyEle);
         console.dir(bodyEle);
         ```

      2. 获取**HTML元素**

         ```javascript
         var htmlEle = document.documentElement;
         console.log(htmlEle);
         ```

4. ### **事件基础**

   1. **事件三要素**

      - 事件源

      - 事件类型

      - 事件处理程序

         ```javascript
         // 点击一个按钮，弹出对话框
         //(1) 事件源 事件被触发的对象   谁  按钮
         var btn = document.getElementById('btn');
         //(2) 事件类型  如何触发 什么事件 比如鼠标点击(onclick) 还是鼠标经过 还是键盘按下
         //(3) 事件处理程序  通过一个函数赋值的方式 完成
         btn.onclick = function() {
             alert('点秋香');
         }
         ```

   2. **执行事件的步骤**

      1. 获取事件源

      2. 注册事件(绑定事件)

      3. 添加事件处理程序(采取函数赋值形式)

         ```javascript
         // 点击div 控制台输出 我被选中了
         // 1. 获取事件源
         var div = document.querySelector('div');
         // 2.绑定事件 注册事件
         // div.onclick 
         // 3.添加事件处理程序 
         div.onclick = function() {
             console.log('我被选中了');
         }
         ```

   3. **常见的鼠标事件**

      | 鼠标事件    | 触发条件         |
      | ----------- | :--------------- |
      | cnclick     | 鼠标点击左键触发 |
      | onmouseover | 鼠标经过触发     |
      | onmouseout  | 鼠标离开触发     |
      | onfocus     | 获取鼠标焦点触发 |
      | onblur      | 失去鼠标焦点触发 |
      | onmousemove | 鼠标移动触发     |
      | onmmouseup  | 鼠标弹起触发     |
      | onmousedown | 鼠标按下触发     |
      
      ```javascript
      // 1. contextmenu 我们可以禁用右键菜单
      document.addEventListener('contextmenu', function(e) {
          e.preventDefault();
      })
      // 2. 禁止选中文字 selectstart
      document.addEventListener('selectstart', function(e) {
          e.preventDefault();
      
      })
      ```
      
      

5. ### **操作元素**

   1. **改变元素内容**

      1. element.innerText

         ```javascript
         //改变从起始位置到终止位置的内容,但他除去html标签,同时空格和换行也会换掉
         // 当我们点击了按钮，  div里面的文字会发生变化
         // 1. 获取元素 
         var btn = document.querySelector('button');
         var div = document.querySelector('div');
         // 2.注册事件
         btn.onclick = function() {
             // div.innerText = '2022-3-20';
             div.innerText = getDate();
         }
         
         function getDate() {
             var date = new Date();
             // 我们写一个 2019年 5月 1日 星期三
             var year = date.getFullYear();
             var month = date.getMonth() + 1;
             var dates = date.getDate();
             var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
             var day = date.getDay();
             return '今天是：' + year + '年' + month + '月' + dates + '日 ' + arr[day];
         }
         // 我们元素可以不用添加事件
         var p = document.querySelector('p');
         p.innerText = getDate()
         ```

      2. element.innerHTML

         ```javascript
         //改变起始位置到终止位置的全部内容,包括html标签,同时保留空格和换行
         // innerText 和 innerHTML的区别 
         // 1. innerText 不识别html标签 非标准  去除空格和换行
         var div = document.querySelector('div');
         // div.innerText = '<strong>今天是：</strong> 2019';
         // 2. innerHTML 识别html标签 W3C标准 保留空格和换行的
         div.innerHTML = '<strong> 今天是: </strong> 2019';
         // 这两个属性是可读写的  可以获取元素里面的内容
         var p = document.querySelector('p');
         console.log(p.innerText);
         console.log(p.innerHTML);
         ```

   2. **常用元素的属性操作**

      1. innerHTML,innerText 改变元素内容
      2. src,href
      3. id,alt,title

   3. **表单元素的属性操作**

      1. type, value, checked, selected, disabled

         ```javascript
         // 1. 获取元素
         var btn = document.querySelector('button');
         var input = document.querySelector('input');
         // 2. 注册事件 处理程序
         btn.onclick = function() {
             // input.innerHTML = '点击了';  这个是 普通盒子 比如 div 标签里面的内容
             // 表单里面的值 文字内容是通过 value 来修改的
             input.value = '被点击了';
             // 如果想要某个表单被禁用 不能再点击 disabled  我们想要这个按钮 button禁用
             // btn.disabled = true;
             this.disabled = true;
             // this 指向的是事件函数的调用者 btn
         }
         ```

   4. **样式属性操作**

      通过JS修改元素的大小,颜色,位置等样式

      1. element.style  行内样式操作
      2. element.className  类名样式操作
      
   5. **排他思想**

      1. 如果有同一组元素,想要某一个元素实现某种样式,需要用到循环的排他算法:

         1. 所有元素全部清除样式

         2. 给当前元素设置样式

         3. **注意:**顺序不能颠倒

            ```javascript
            // 1. 获取所有按钮元素
            var btns = document.getElementsByTagName('button');
            // btns得到的是伪数组  里面的每一个元素 btns[i]
            for (var i = 0; i < btns.length; i++) {
                btns[i].onclick = function() {
                    // (1) 我们先把所有的按钮背景颜色去掉  干掉所有人
                    for (var i = 0; i < btns.length; i++) {
                        btns[i].style.backgroundColor = '';
                    }
                    // (2) 然后才让当前的元素背景颜色为pink 留下我自己
                    this.style.backgroundColor = 'pink'; 
                }
            }
            ```

6. ### **自定义属性的值**

   1. **获取属性值**

      ```javascript
      var div = document.querySelector('div');
      // (1) element.属性
      console.log(div.id);
      //(2) element.getAttribute('属性')  get得到获取 attribute 属性的意思 
      //自己添加的属性我们称为自定义属性 index
      console.log(div.getAttribute('id'));
      console.log(div.getAttribute('index'));
      //区别:
      // element.属性  获取内置属性值(元素本身自带的属性)
      // element.getAttribute('属性')  主要获得自定义的属性(标准)
      ```

   2. **设置属性值**

      ```javascript
      // (1) element.属性= '值'
      div.id = 'test';
      div.className = 'navs';
      // (2) element.setAttribute('属性', '值');  主要针对于自定义属性
      div.setAttribute('index', 2);
      div.setAttribute('class', 'footer'); // class 特殊  这里面写的就是class 不是className
      ```

   3. **移除属性  removeAttribute(属性)** 

      `div.removeAttribute('index');`
      
   4. **H5自定义属性**

      1. **自定义属性的目的:**是为了保存并使用数据,有些数据可以保存到页面中二不用保存到数据库中

      2. **设置H5自定义属性**

         1. H5规定自定义属性data开头做为属性名赋值

            比如: **<div data-index= "1" ></div>**

         2. H5新增 element.dataset.**index** 或者 element.dataset['**index**']

            ```javascript
            // dataset 是一个集合里面存放了所有以data开头的自定义属性
            console.log(div.dataset);
            console.log(div.dataset.index);
            console.log(div.dataset['index']);
            // 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法
            console.log(div.dataset.listName);
            console.log(div.dataset['listName']); 
            ```

7. ### **节点操作**

   1. **节点概述**

      1. 一般的,节点至少拥有**nodeTyoe**(节点类型),**nodeName**(节点名称)和**nodeValue**(节点值)三个基本属性
         - 元素节点 nodeType 为 1
         - 属性节点 nodeType 为 2
         - 文本节点 nodeType 为 3 (文本节点包含文字, 空格, 换行等)

   2. **节点层级**

      利用 DOM 树可以吧节点划分为不同的层级关系 ,常用的是父子兄层级关系

      1. **父级节点**

         `node.parentNode`

         - parentNode 属性可以返回某节点的父节点,注意是**最近的一个父节点**
         - 如果指定的节点没有父节点则返回**null**

      2. **子级节点**

         ```javascript
         // 1. 子节点  childNodes 所有的子节点 包含 元素节点 文本节点等等
         console.log(ul.childNodes);
         console.log(ul.childNodes[0].nodeType);
         console.log(ul.childNodes[1].nodeType);
         // 2. children 获取所有的子元素节点 也是我们实际开发常用的
         console.log(ul.children);
         ```

         2. **第一个子元素与最后一个子元素**

            ```javascript
            // 1. firstChild 第一个子节点 不管是文本节点还是元素节点
            console.log(ol.firstChild);
            console.log(ol.lastChild);
            // 2. firstElementChild 返回第一个子元素节点 ie9才支持
            console.log(ol.firstElementChild);
            console.log(ol.lastElementChild);
            // 3. 实际开发的写法  既没有兼容性问题又返回第一个子元素
            console.log(ol.children[0]);
            console.log(ol.children[ol.children.length - 1]);
            ```

      3. **兄弟节点**

         ```javascript
         // 1.nextSibling 下一个兄弟节点 包含元素节点或者 文本节点等等
         console.log(div.nextSibling);
         console.log(div.previousSibling);
         // 2. nextElementSibling 得到下一个兄弟元素节点
         console.log(div.nextElementSibling);
         console.log(div.previousElementSibling);
         	//注意:兼容性问题,IE9以上支持
         //解决兼容性问题
         function getNextElementSibling (element) {
             var el = element;
             while (el = el.nextSibling) {
                 if (el.nodeType === 1) {
                     return el;
                 }
             }
             return null;
         }
         ```

      4. **创建和添加节点**

         1. **创建节点**

         2. **添加节点**

            ```javascript
            // 1. 创建节点元素节点
            var li = document.createElement('li');
            //document.createElement('tagName') 方法创建由tagName 指定的HTML元素.因为这些节点原先不存在,是根据动态生成的,所以也叫动态创建元素节点
            // 2. 添加节点 node.appendChild(child)  node 父级  child 是子级 后面追加元素  类似于数组中的push
            var ul = document.querySelector('ul');
            ul.appendChild(li);
            //node.appendChild( ) 方法将一个节点添加到指定父节点的子节点的末尾
            // 3. 添加节点 node.insertBefore(child, 指定元素);
            var lili = document.createElement('li');
            ul.insertBefore(lili, ul.children[0]);
            //node.insertBefore(child, 指定元素); 方法将一个节点添加到父级节点的指定子节点前面
            // 4. 我们想要页面添加一个新的元素 ： 1. 创建元素 2. 添加元素
            ```

         3. **删除节点**

            `node.removeChild(child)` 从 DOM 中删除一个子节点,返回删除节点

         4. **克隆节点**

            ```javascript
            var ul = document.querySelector('ul');
            // 1. node.cloneNode(); 括号为空或者里面是false 浅拷贝 只复制标签不复制里面的内容
            // 2. node.cloneNode(true); 括号为true 深拷贝 复制标签复制里面的内容
            var lili = ul.children[0].cloneNode(true);
            ul.appendChild(lili);
            ```

8. ### **三种动态创建元素区别**

   1. **document.write** 是直接将内容写入页面的内容流,但是**文档流执行完毕,则他会导致页面全部重绘**

   2. **innerHTML** 是将内容写入某个DOM节点,不会导致页面全部重绘

   3. **innerHTML** 创建多个元素效率更高(不要拼接字符串,采取数组形式拼接),结构稍微复杂

   4. **createElement( )** 创建多个元素效率稍微低一点,但结构更清晰

      **总结: 不同浏览器下, innerHTML 效率要比 creatElement 高**

## 事件高级

### 绑定事件

**注册事件概述**

给页数添加事件,称为**注册事件**或**绑定事件**

注册事件有两种方式:**传统方式和方法监听注册方式**

1. **传统注册方式**

   1. 利用 on 开头的事件 onclick
   2. <button.onclick= "alert('hi~')"  > </button>
   3. btn.onclick = function() {}
   4. 特点:
      - 注册事件**唯一性**
      - 同一个元素同一个事件只能设置一个处理函数,最后注册的处理函数将覆盖前面注册的处理函数

2. **方法监听注册事件方式**

   1. w3c标椎 推荐方式
   2. addEventListener() 方法
   3. IE9 之前的IE 不支持此方法,可以使用attachEvent() 代替
   4. 特点:
      - 同一个元素同一个事件可以注册多个监听器
      - 按注册顺序执行

   5. **addEventListener 事件监听方式**

      `eventTarget.addEventListener (type, listener [, useCapture])`

      eventTarget.addEventListener( ) 方法将指定的监听器注册到eventTarget(目标对象) 上,当该对象触发指定的事件时,就会执行事件处理函数

      **该方法接收三个参数**

      - **type:**事件类型字符串, 比如 click, mouseover, **注意这里不带 on**

      - **listener:** 事件处理函数, 事件发生时,会调用该监听函数

      - **useCapture:** 可选参数,是一个布尔值,默认是 false

        ```javascript
        // 2. 事件侦听注册事件 addEventListener 
        // (1) 里面的事件类型是字符串 必定加引号 而且不带on
        // (2) 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
        btns[1].addEventListener('click', function () {
            alert('22');
        })
        ```

   6. **attachEvent 事件监听方式 (*ie9以前的版本支持*)**

      ```Javas
      // attachEvent ie9以前的版本支持
      btns[2].attachEvent('onclick', function () {
      alert(11);
      })

### 删除事件(解绑事件)

1. **删除事件的方式**

   1. **传统注册方式**

      `eventTarget.onclick = null;`

   2. **方法监听注册事件**

      ```javascript
      // 1. removeEventListener 删除事件
      eventTarget.removeEventListener (type, listener [, useCapture])
      
      divs[1].addEventListener('click', fn) // 里面的fn 不需要调用加小括号
      
      function fn() {
          alert(22);
          divs[1].removeEventListener('click', fn);
      }
      
      // 2. detachEvent 删除事件
      divs[2].attachEvent('onclick', fn1);
      
      function fn1() {
          alert(33);
          divs[2].detachEvent('onclick', fn1);
      }
      ```

### 	DOM 事件流

1. 事件流描述的是从页面中接收事件的顺序

2. 事件发生是会在元素节点之间按照待定的顺序传播,这个过程即 DOM 事件流

3. DOM 事件流:

   - 捕获阶段

   - 当前目标阶段

   - 冒泡阶段

     ```javascript
     // dom 事件流 三个阶段
     // 1. JS 代码中只能执行捕获或者冒泡其中的一个阶段。
     // 2. onclick 和 attachEvent（ie） 只能得到冒泡阶段。
     // 3. 捕获阶段 如果addEventListener 第三个参数是 true 那么则处于捕获阶段  document -> html -> body -> father -> son
     var son = document.querySelector('.son');
     son.addEventListener('click', function() {
         alert('son');
     }, true);
     var father = document.querySelector('.father');
     father.addEventListener('click', function() {
         alert('father');
     }, true);
     // 4. 冒泡阶段 如果addEventListener 第三个参数是 false 或者 省略 那么则处于冒泡阶段  son -> father ->body -> html -> document
     var son = document.querySelector('.son');
     son.addEventListener('click', function() {
         alert('son');
     }, false);
     var father = document.querySelector('.father');
     father.addEventListener('click', function() {
         alert('father');
     }, false);
     document.addEventListener('click', function() {
         alert('document');
     })
     
     //注意:
     //1. JS 代码中只能执行捕获或冒泡其中的一个阶段
     //2. onclick 和 attachEvent 只能得到冒泡阶段
     //3. addEventListener (type, listener [, useCapture]) 第三个参数如果是 ture , 表示在事件捕获阶段调用事件处理程序;如果是 false (默认为 false ), 表示在事件冒泡阶段调用时间处理程序
     ```

### 事件对象

1. **什么是事件对象**

   1. **event** 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看
   2. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数
   3. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊,如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
   4. 这个事件对象我们可以自己命名 比如 **event 、 evt、 e**
   5. 事件对象也有兼容性问题 **ie678** 通过 **window.event** 兼容性的写法  **e = e || window.event;**

   ```javascript
   var div = document.querySelector('div');
   div.onclick = function(event) {
       console.log(event);
   }
   
   div.addEventListener('click', function (event) {
       console.log(event);
   })
   ```

2. **事件对象的常用属性和方法**

   | 事件对象属性方法    | 说明                                             |
   | :------------------ | :----------------------------------------------- |
   | e.target            | 返回**触发**事件的对象  标准                     |
   | e.srcElement        | 返回**触发**事件的对象  非标准 ie6~8使用         |
   | e.type              | 返回事件类型  比如 click mouseover  不带 on      |
   | e.cancelBubble      | 该属性阻止冒泡  非标准 ie6~8使用                 |
   | e.returnValue       | 该属性 阻止默认事件  (默认行为) 非标准 ie6~8使用 |
   | e.preventDefault()  | 该方法 阻止默认事件  (默认行为) 标准             |
   | e.stopPropagation() | 阻止冒泡 标准                                    |

   ```javascript
   // 1. e.target 返回的是触发事件的对象（元素）  this 返回的是绑定事件的对象（元素）
   // 区别 ： e.target 点击了那个元素，就返回那个元素 this 那个元素绑定了这个点击事件，那么就返回谁
   var div = document.querySelector('div');
   div.addEventListener('click', function(e) {
       console.log(e.target); //<div>123</div>
       console.log(this); //<div>123</div>
   })
   
   var ul = document.querySelector('ul');
   ul.addEventListener('click', function(e) {
       // 给ul 绑定了事件 那么 this 就指向ul
       console.log(this); // <ul>...</ul>
       // e.target 指向点击的那个对象 谁触发了这个事件 点击li e.target 指向;de就是li
       console.log(e.target); //<li>...</li>
   })
   
   // 1. 了解兼容性
   div.onclick = function (e) {
       e = e || window.event;
       var target = e.target || e.srcElement;
       console.log(target);
   }
   // 2. 了解 跟 this 有个非常相似的属性 currentTarget  ie678不认识
   
   // 1. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
   var a = document.querySelector('a');
   a.addEventListener('click', function(e) {
       e.preventDefault(); //  dom 标准写法
   })
   // 2. 传统的注册方式
   a.onclick = function(e) {
       // 普通浏览器 e.preventDefault();  方法
       e.preventDefault();
       // 低版本浏览器 ie678  returnValue  属性
       e.returnValue;
       // 我们可以利用return false 也能阻止默认行为 没有兼容性问题
       return false;
       //return 后面的代码不执行了， 而且只限于传统的注册方式
       alert(11);
   }
   
    // 常见事件对象的属性和方法
   // 阻止冒泡  dom 推荐的标准 stopPropagation() 
   var son = document.querySelector('.son');
   son.addEventListener('click', function(e) {
       alert('son');
       e.stopPropagation(); // stop 停止  Propagation 传播
       e.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
   }, false);
   
   var father = document.querySelector('.father');
   father.addEventListener('click', function() {
       alert('father');
   }, false);
   document.addEventListener('click', function() {
       alert('document');
   })
   ```
   
3. **事件委托(代理, 委派)**

   1. **事件委托的原理**

      **不是没个子节点单独设置事件监听,而是事件监听设置在父节点上,然后利用冒泡原理影响设置每一个子节点**

   2. **事件委托的作用**

      只操作一次 DOM , 提高了程序的性能

   ```javascript
   // 事件委托的核心原理：给父节点添加侦听器， 利用事件冒泡影响每一个子节点
   var ul = document.querySelector('ul');
   ul.addEventListener('click', function(e) {
       alert('知否知否，点我应有弹框在手！');
       //e.target 得到点击的对象
       e.target.style.backgroundColor = 'pink';
   }) 
   ```

4. **鼠标事件对象**

   event 对象代表事件的状态,跟事件相关的一系列信息的集合  鼠标事件对象 MouseEvent  键盘事件对象  KeyboardEvent

   | 鼠标事件对象 | 说明                                  |
   | ------------ | ------------------------------------- |
   | e.clientX    | 返回鼠标相对于浏览器窗口可视区的X坐标 |
   | e.clientY    | 返回鼠标相对于浏览器窗口可视区的Y坐标 |
   | e.pageX      | 返回鼠标相对于文档页面可视区的X坐标   |
   | e.pageY      | 返回鼠标相对于文档页面可视区的Y坐标   |
   | e.screenX    | 返回鼠标相对于电脑屏幕的X坐标         |
   | e.screenY    | 返回鼠标相对于电脑屏幕的Y坐标         |

   ```javascript
   //e.mousemove 鼠标移动事件
   
   // 图片跟随鼠标移动案例
   var pic = document.querySelector('img');
   document.addEventListener('mousemove', function(e) {
       // 1. mousemove只要我们鼠标移动1px 就会触发这个事件
       // console.log(1);
       // 2.核心原理： 每次鼠标移动，我们都会获得最新的鼠标坐标， 把这个x和y坐标做为图片的top和left 值就可以移动图片
       var x = e.pageX;
       var y = e.pageY;
       //3 . 千万不要忘记给left 和top 添加px 单位
       pic.style.left = x + 'px';
       pic.style.top = y + 'px';
   })
   ```

5. **常用的键盘事件**

   | 键盘事件   |                           触发条件                           |
   | ---------- | :----------------------------------------------------------: |
   | inkeyup    |                   某个键盘按键被松开时触发                   |
   | onkeydown  |                   某个键盘按键被按下时触发                   |
   | onkeypress | 某个键盘按键被按下时触发 **不能识别功能键 比如 Ctrl shift  箭头 等** |
   |            |      *三个事件的执行顺序  keydown -- keypress -- keyup*      |

   1. **键盘事件对象**

      | 键盘事件对象属性 | 说明              |
      | ---------------- | ----------------- |
      | keyCode          | 返回该键的ASCLL值 |

      ```javascript
      // 键盘事件对象中的keyCode属性可以得到相应键的ASCII码值
      // 1. 我们的keyup 和keydown事件不区分字母大小写  a 和 A 得到的都是65
      // 2. 我们的keypress 事件 区分字母大小写  a  97 和 A 得到的是65
      document.addEventListener('keyup', function(e) {
          // console.log(e);
          console.log('up:' + e.keyCode);
          // 我们可以利用keycode返回的ASCII码值来判断用户按下了那个键
          if (e.keyCode === 65) {
              alert('您按下的a键');
          } else {
              alert('您没有按下a键')
          }
      
      })
      document.addEventListener('keypress', function(e) {
          // console.log(e);
          console.log('press:' + e.keyCode);
      })
      //实际开发中,更多的使用keydown和keyup,它能识别所有的键
      //keypress不能识别功能键,但可以区分大小写
      ```

# BOM 浏览器模型

## BOM 概述 

1. **什么是 BOM**

   BOM 即**浏览器对象模型**, 它提供了独立于内容而与**浏览器窗口进行交互的对象**,其核心对象是**window**

2. **BOM 的构成**

   window 对象是浏览器的顶级对象,它具有双重角色
   1. 它是JS访问浏览器窗口的一个接口
   2. 它是一个全局对象.定义在全局作用域中的变量, 函数都会变成window 对象的属性和方法. 在调用的时候可以省略 window

3. **window 对象的常见事件**

   1. **窗口加载事件**

      ```javascript
      window.onload = function () {};
      window.addEventListener("load", function() {});
      //window.onload 是窗口(页面) 加载事件, 当文档内容完全加载完成会触发该事件(包括图像, 脚本文件, CSS文件等), 就调用的处理函数
      //注意:
      // 1. 有了window.onload 就可以把JS 代码写到页面元素的上方,因为onload 是等页面内容全部加载完毕,再去执行处理函数
      // 2. window.onload 传统注册事件方式只能写一次,如果有多个,会以最后一个window.onload为准
      // 3. 使用addEventListener 没有限制
      
      document.addEventListener('DOMContentLoaded', function() {})
      // DOMContentLoaded 是DOM 加载完毕，不包含图片 falsh css 等就可以执行 加载速度比 load更快一些
      ```

   2. **调整窗口大小事件**

      ```javascript
      window.onresize = function () {}
      window.addEventListener("resize", funnction() {});
      //window.onresize 是调整窗口大小加载事件, 当触发时就调用的处理函数
      //注意:
      // 1. 只要窗口大小发生像素变化, 就会触发这个事件
      // 2. 利用这个时间可以完成响应式布局 window.innerWidth 当前屏幕的宽度
      ```

   3. **定时器**

      ```javascript
       // 一. setTimeout() 也称为 回调函数
      // 语法规范：  window.setTimeout(调用函数, 延时时间);
      // 1. 这个window在调用的时候可以省略
      // 2. 这个延时时间单位是毫秒 但是可以省略，如果省略默认的是0
      // 3. 这个调用函数可以直接写函数 还可以写 函数名 还有一个写法 '函数名()'
      // 4. 页面中可能有很多的定时器，我们经常给定时器加标识符 (名字)
      // setTimeout(function() {
      //     console.log('时间到了');
      // }, 2000)
      
      function callback() {
          console.log('爆炸了');
      }
      
      setTimeout(callback, 3000);
      var time1 = setTimeout(callback, 3000);
      var time1 = setTimeout(callback, 5000);
      // setTimeout('callback()', 3000); // 我们不提倡这个写法
      
      // 二. 停止 setTimeout() 定时器
      //语法规范 window.clearTimeout(timeout ID)
      var btn = document.querySelector('button');
      var timer = setTimeout(function() {
          alert('爆炸了');
      },5000)
      btn.addEventListener('click', function() {
          window.clearTimeout(timer);
          console.log('停止');
      })
      //注意:
      // 1. window 可以省略
      // 2. 里面的参数就是定时器的标识符
      
      // 三. setInterval() 定时器
      //语法规范: window.setInterval(回调函数,[间隔的毫秒数]);
      //setInterval() 方法重复调用一个函数,每隔这个时间,就去调用一次这个回调函数
      //注意:
      // 1. 这个window在调用的时候可以省略
      // 2. 这个延时时间单位是毫秒 但是可以省略，如果省略默认的是0
      // 3. 这个调用函数可以直接写函数 还可以写 函数名 还有一个写法 '函数名()'
      // 4. 页面中可能有很多的定时器，我们经常给定时器加标识符 (名字)
      setInterval(function() {
          console.log('继续输出');
      }, 1000);
      //区别:
      // 1. setTimeout  延时时间到了，就去调用这个回调函数，只调用一次 就结束了这个定时器
      // 2. setInterval  每隔这个延时时间，就去调用这个回调函数，会调用很多次，重复调用这个函数
      
      //停止 setInterval() 定时器
      //语法规范: window.clearInterval (unterval ID);
      var begin = document.querySelector('.begin');
      var stop = document.querySelector('.stop');
      var timer = null; // 全局变量  null是一个空对象
      begin.addEventListener('click', function() {
          timer = setInterval(function() {
              console.log('ni hao ma');
      
          }, 1000);
      })
      stop.addEventListener('click', function() {
          clearInterval(timer);
      })
      //注意:
      // 1. window 可以省略
      // 2. 里面的参数就是定时器的标识符
      ```
      
   4. **JS 执行机制**

      1. **同步和异步**

         1. 同步任务

            同步任务都在主线程上, 形成一个执行线

         2. 异步任务

            JS 的异步任务是通过回调函数实现的.一般而言,异步任务有以下三种类型

            1. 普通事件,如 click, resize 等
            2. 资源加载,如 load, error 等
            3. 定时器, 包括 setlnterval, setTimeout 等

         ​	异步任务相关**回调函数**添加到**任务队列**中(任务队列也称消息队列)

      2. **执行机制**

         1. 先执行执行栈中的同步任务
         2. 异步任务(回调函数)放入任务队列中
         3. 一旦执行栈中的所有同步任务执行完毕,系统就会按次序读取任务队列中的异步任务,于是被读取的异步任务结束等待状态,进入执行栈,开始执行
         4. 由于主线程不断地重复获取二妃山,执行任务, 再获取任务,再执行,所以这种机制被称为**事件循环(rvrnt loop)**

   5. **location 对象**

      1. **什么是 location 对象**

         1. window 对象给我们提供了一个location 属性 用于获取或设置窗体的URL,并且可以用于解析 URL.因为这个属性返回的是一个对象所以将这个属性也称为location 对象

      2. **URL** 

         1. 统一资源定位符(Uniform Resource Locator, URL )是互联网上标准资源的地址

      3. **location 对象**

         | location 对象属性 | 返回值                             |
         | ----------------- | ---------------------------------- |
         | location.href     | 获取或者设置 整个URL               |
         | location.host     | 返回主机(域名) www.itheima.com     |
         | location.port     | 返回端口号 如果返回 空字符串       |
         | location.pathname | 返回路径                           |
         | location.search   | 返回参数                           |
         | location.hash     | 返回片段 #后面内容 常见于链接 锚点 |

         | location 对象方法  | 返回值                                                       |
         | ------------------ | ------------------------------------------------------------ |
         | location.assign()  | 跟 herf 一样, 可以跳转页面(也称为重定向页面)                 |
         | location.reolace() | 替换当前页面, 因为不记录历史, 所以不能后退                   |
         | location.reload()  | 重新加载页面,相当于刷新页面或者 f5 如果参数为true 强制刷新 ctrl+f5 |
      
   6. **navigator 对象**

      1. navigator 对象包含许多含有有关浏览器的信息, 它有很多属性, 常用userAgent属性判断用户在那个终端打开页面,实现跳转

   7. **history 对象**

      window 对象给我们提供了一个history对象, 与浏览器历史记录进行互相交互,该对象包含了用户(在浏览器窗口中)访问过得URL'

      | history 对象方法 | 作用                                                         |
      | ---------------- | ------------------------------------------------------------ |
      | back()           | 可以后退功能                                                 |
      | forward()        | 前进功能                                                     |
      | go(参数)         | 前进后退功能 参数如果是 1 前进一个页面 如果是 -1 后退一个页面 |

# PC 网页特效

## 元素偏移量 offaet 系列

1. **offset 概述**

   1. 使用 offset 系列相关属性可以动态的得到钙元素的位置(偏移), 大小等
      - 获取元素距离带有定位父元素的位置
      - 获取元素自身的大小(宽度 高度)
      - 注意:返回的数值都不带单位

2. **offset 系列常用属性**

   | offset系列属性       | 作用                                                         |
   | -------------------- | ------------------------------------------------------------ |
   | element.offsetParent | 返回作为该元素带有定位的父级元素 如果父级都没有定位则返回body |
   | element.offsetTop    | 返回元素相对带有定位父元素上方的偏移                         |
   | element.offsetLeft   | 返回元素相对带有定位父元素左边框的偏移                       |
   | element.offsetWidth  | 返回自身包括padding, 边框, 内容区的宽度, 返回数值不带单位    |
   | element.offsetHeight | 返回自身包括padding, 边框, 内容区的高度, 返回数值不带单位    |

3. **offset 与 style 区别**

   | offset                                         | style                                        |
   | :--------------------------------------------- | :------------------------------------------- |
   | offset 可以得到任意样式表中的样式值            | style只能得到行内样式表中的样式值            |
   | offset 系列获得的数字是没有单位的              | style.width 获得的是带有单位的字符串         |
   | offsetWidth 包含padding+border+width           | style.width 获得步高寒padding和border的值    |
   | offsetWidth 等属性是只读属性, 只能获取不能赋值 | style.width 是可读写实行, 可以获取也可以赋值 |
   | 所以,想要获取元素大小位置,用offset更合适       | 所以,要给元素更改值,则需要style改变          |


## 元素可视区  client 系列

1. client (客户端), client 系列的相关属性可以获取元素可视区的相关信息  通过client系列的相关属性可以动态的得到该元素的边框大小, 元素大小等

   | client系列属性       | 作用                                                         |
   | -------------------- | ------------------------------------------------------------ |
   | element.clientTop    | 返回元素上边框的大小                                         |
   | element.clientLeft   | 返回元素左边框的大小                                         |
   | element.clientWidth  | 返回自身包括padding, 内容区的宽度, 不含边框, 返回数值不带单位 |
   | element.clientGeight | 返回自身包括padding, 内容区的高度, 不含边框, 返回数值不带单位 |

2. **立即函数**

   ```javascript
   // 1.立即执行函数: 不需要调用，立马能够自己执行的函数
   // 2. 写法 也可以传递参数进来
   // (1.) (function() {})()    或者  (2. (function(){}());
   (function(a, b) {
       console.log(a + b);
       var num = 10;
   })(1, 2); // 第二个小括号可以看做是调用函数
   (function sum(a, b) {
       console.log(a + b);
       var num = 10; // 局部变量
   }(2, 3));
   // 3. 立即执行函数最大的作用就是 独立创建了一个作用域, 里面所有的变量都是局部变量 不会有命名冲突的情况
   ```

## 元素滚动 scroll 系列 

1. **元素 scroll 系列属性**

   scroll (滚动),使用scroll系列的相关属性可以动态的得到该元素的大小, 滚动距离等

   | scroll系列属性       | 作用                                           |
   | -------------------- | ---------------------------------------------- |
   | element.scrollTop    | 返回被卷去的上侧距离, 返回数值 不带单位        |
   | element.scrollLeft   | 返回被卷去的左侧距离, 返回数值 不带单位        |
   | element.scrollWidth  | 返回自身实际的宽度, 不含边框, 返回数值不带单位 |
   | element.scrollHeight | 返回自身实际的高度, 不含边框, 返回数值不带单位 |

##     动画函数封装

1. **简单动画**

```javascript
// 简单动画函数封装obj目标对象 target 目标位置
function animate(obj, target) {
    obj.timer = setInterval(function() {
        if (obj.offsetLeft >= target) {
            // 停止动画 本质是停止定时器
            clearInterval(timer);
        }
        obj.style.left = obj.offsetLeft + 1 + 'px';

    }, 30);
}
var div = document.querySelector('div');
var span = document.querySelector('span');
// 调用函数
animate(div, 300);
animate(span, 200);
```

2. **缓动动画**

   ```JavaScript
   // 缓动动画函数封装obj目标对象 target 目标位置
   // 思路：
   // 1. 让盒子每次移动的距离慢慢变小， 速度就会慢慢落下来。
   // 2. 核心算法：(目标值 - 现在的位置) / 10 做为每次移动的距离 步长
   // 3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器
   obj.style.left = obj.offsetLeft + step + 'px';
   // 匀速动画 就是 盒子是当前的位置 +  固定的值 10 
   // 缓动动画就是  盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）
   
   //动画函数多个目标之间移动
   //当我们点击按钮时, 判断步长是正值还是负值
   // 1. 如果是正值,则步长往大取整
   // 2. 如果是负值,则步长往大取整
   
   // 把我们步长值改为整数 不要出现小数的问题
   // var step = Math.ceil((target - obj.offsetLeft) / 10);
   var step = (target - obj.offsetLeft) / 10;
   step = step > 0 ? Math.ceil(step) : Math.floor(step);

3. **动画函数添加回调函数**

   ```javascript
   function animate(obj, target, callback) {
       // 回调函数写到定时器结束里面
       if (callback) {
           // 调用函数
           callback();
       }
   }
   // console.log(callback);  callback = function() {}  调用的时候 callback()
   btn800.addEventListener('click', function() {
       // 调用函数
       animate(span, 800, function() {
           // alert('你好吗');
           span.style.backgroundColor = 'red';
       });
   })
   ```

4. **动画函数封装到单独JS文件里面**

5. **常见网页特效**

   ```javascript
   //滚动窗口至文档中的特定位置
   window.scroll(x,y)
   ```

## 移动端网页特效

1. **触屏事件 (touch)**也 称触摸事件

   1. **触屏touch事件**

      | 触屏touch事件 | 说明                            |
      | ------------- | ------------------------------- |
      | touchstart    | 手指触摸到一个 DOM元素是触发    |
      | touchmoce     | 手指在一个 DOM 元素上滑动时触发 |
      | touchhend     | 手指从一个 DOM 元素上移开时触发 |

   2. **触摸事件对象 (TouchEvent)**

      | 触摸列表       | 说明                                           |
      | -------------- | ---------------------------------------------- |
      | touches        | 正在触摸屏幕的所有手指的一个列表               |
      | targetTouches  | 正在触摸当前 DOM 元素上的手指的一个列表        |
      | changedTouches | 手指状态发生了改变的列表,从无到有,从有到无变化 |

   3. **clssList 属性**

      ```javascript
      // classList 返回元素的类名
      var div = document.querySelector('div');
      // console.log(div.classList[1]);
      // 1. 添加类名  是在后面追加类名不会覆盖以前的类名 注意前面不需要加.
      div.classList.add('three');
      // 2. 删除类名
      div.classList.remove('one');
      // 3. 切换类
      var btn = document.querySelector('button');
      btn.addEventListener('click', function() {
          document.body.classList.toggle('bg');
      })
      ```

   4. **click 延时 解决方案**

      1. 禁用缩放  浏览器 禁用默认的双击缩放功能行为并且去掉300ms的点击延迟

         `<meta name="viewport" content="user-scalable=no">`

      2. 利用touch事件自己封装这个事件解决 300ms 延迟问题

         ```javascript
         // 原理
         // 1. 当手指触摸屏幕,记录当前的触摸时间
         // 2. 当手指离开屏幕,用离开地时间减去触摸的时间
         // 3. 如果时间小于 150ms, 并且没有滑动过屏幕,那么就定义为点击事件
         
         // 封装tap 解决 click 300ms 延时
         function tap(obj, callback) {
             var isMove = false;
             var startTime = 0; // 记录触摸时候的时间变量
             obj.addEventListener('touchstart', function (e) {
                 startTime = Date.now(); // 记录触摸时间
             });
             obj.addEventListener('touchmove', function (e) {
                 isMove = true; //看看是否滑动, 有滑动算拖拽, 不算点击
             });
             obj.addEventListener('touchend', function(e) {
                 if (!isMove && (Date.now() - startTime) < 150) { // 如果手指触摸和离开时间小于 150ms 算点击
                     callback && callback(); // 执行回调函数
                 }
                 isMove = false; // 取反 重置
                 startTime = 0;
             });
         }
         
         // 调用
         tap(div,function() { // 执行代码
         });
         ```

      3. **插入 fastclick 插件**
      
   5. **移动端常用开发插件**

      1. click 延时 解决 fastclick 插件
      2. 轮播图 Swiper 插件 
      3. superslide 插件
      4. icroll 插件
      5. 视频插件 zy.media.js

## 本地存储

1. **本地存储特性**

   1. 数据存储在用户浏览器中
   2. 设置, 读取方便, 甚至页面刷新不丢失数据
   3. 容量较大, sessionStorage约5M, localStorage约20M
   4. 只能存储字符串, 可以将对象JSON.stringity() 编码后存储

2. **window.sessionStorage**

   1. 生命周期为关闭浏览器窗口

   2. 在同一个窗口下数据可以共享

   3. 以键值对的形式存储数据

      ```javascript
      // 存储数据
      sessionStorage.setItem(key, value)
      // 获取数据
      sessionStorage.getItem(key)
      // 删除数据
      sessionStorage.removeItem(key)
      // 删除所有
      sessionStorage.clear()
      ```

3. **window.localStorage**

   1. 生命周期为永久生效,除非手动删除, 否则关闭页面也会存在

   2. 可以多个窗口下数据可以共享

   3. 以键值对的形式存储数据

      ```javascript
      // 存储数据
      localStorage.setItem(key, value)
      // 获取数据
      localStorage.getItem(key)
      // 删除数据
      localStorage.removeItem(key)
      // 删除所有
      localStorage.clear()
      ```

      





 
