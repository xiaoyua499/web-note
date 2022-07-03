



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

# ES6~ES11

## **ES6**

### let变量声明以及声明特性

1.**声明变量**

```js
let a;
let b,c,d;
let e = 100;
let f = 521, g = 'iloveyou', h = [];
```

2.**声明特性**

1. 变量不能重复声明
2. 块级作用域  全局、函数、eval
3. 不存在变量提升
4. 不影响作用域链

### const 定义常量

1.**声明变量**

```js
const SCHOOL = '尚硅谷'
```

1. 一定要赋初始值

2. 一般常量使用大写（潜规则）

   `const A = 100`

3. 常量的值不能修改

4. 块级作用域

5. 对于数组和对象的元素修改，不算做对常量的修改，不会报错

   ```js
   const TEAM = ['UZI','MLXG','Ming','Letme','xiaohu']
   TEAM.push('Zz1tai')
   ```

###变量的解构赋值

> ​	ES6 允许按照一定模式从数组中和对象中提取值，对变量进行赋值，这被称为解构赋值。
>

 1. **数组的解构**

    ```js
    const F4 = ['小沈阳','刘能','赵四','宋小宝']
    let [xiao,liu,zhao,song] = F4
    console.log(xiao);//小沈阳
    console.log(liu);// 刘能
    console.log(zhao);// 赵四
    console.log(song);// 宋小宝
    ```

2. **对象的解构**

   ```js
   const zhao = {
     name:'赵本山',
     age:'不详',
     xiaopin:function(){
       console.log('我可以演小品');
     }
   }
   let {name,age,xiaopin} = zhao
   console.log(name);//赵本山
   console.log(age);//不详
   console.log(xiaopin);
   /*
     ƒ (){
         console.log('我可以演小品');
       }
   */
   ```

### 模板字符串

> ​	ES6 引入新的声明字符串的方式

1. **声明**

2. **内容中可以直接出现换行符**

   ```js
   let str = `<ul>
   						<li></li>
   						<li></li>
   						<li></li>
   					</ul>`
   ```

3. **变量拼接**

   ```js
   let lovest = 'wx'
   let out = `${lovest}是我`
   console.log(out);//wx是我
   ```

### 简化对象写法

> ​	ES6 允许我们在大括号里面，直接写入变量和函数，作为对象的塑像和方法

```js
let name = '尚硅谷'
let change = function(){
  console.log('我们可以改变你')
}

const school = {
  name,
  change,
  improve(){
    console.log("我们可以提高你的技能")
  }
}
```

### 箭头函数

> ​		ES6 允许使用【箭头】（=>）定义函数

1. **声明函数**

   ```js
   let fn = () => {
     return
   }
   
   //调用函数
   fn()
   ```

2. **特性**

   1. this 是静态的。 this 始终指向函数声明时所在作用域下的 this 值

      ```js
      function getName(){
        console.log(this.name);
      }
      let getName2=()=>{
        console.log(this.name);
      }
      
      //设置 window 对象的 name 属性
      window.name = '尚硅谷'
      const school = {
        name:"ATGUIGU"
      }
      
      //直接调用
      getName() //尚硅谷
      getName2() //尚硅谷
      
      //call 方法调用
      getName.call(school) //ATGUIGU
        getName2.call(school) //尚硅谷
      ```

   2. 不能作为构造实例化对象

      ```js
      let Person = (name, age) => {
        this.name = name
        this.age = age
      }
      
      let me = new Person('xiao',30)
      console.log(me)
      // 报错
      ```

   3. 不能是使用 **arguments** 变量

      ```js
      let fn = () => {
        console.log(arguments)
      }
      fn(1,2,3)
      // 报错
      ```

   4. 箭头函数的简写

      1. 省略小括号，当形参只有一个时

         ```js
         let add = n => {
           return n + n
         }
         console.log(add(9))
         ```

      2. 省略花括号，当代码只有一条语句时，此时 return 必须省略，且语句的执行结果就是函数的返回值

         ```js
         let pow = n => n + n
         console.log(pow(9))
         ```

   5. 使用场景
      1. 箭头函数适合与 this 无关的回调。定时器、数组的方法回调
      2. 箭头函数不适合与 this 有关的回调。 事件回调，对象的方法 

### 函数参数默认值

> ​	ES6 允许给函数参数赋值初始值

1. 形参初始值 具有默认值的参数，一般位置靠后（潜规则）

   ```js
   function add (a,b,c=10) {
     return a + b + c
   }
   let result = add(1, 2)
   console.log(result) //13
   ```

2. 与解构赋值结合

   ```js
   function connect ({host = "127.0.0.1", username, password, port}) {
     console.log(host) // localhost
     console.log(username) // root
     console.log(password) // root
     console.log(port) // 3306
   }
   connect({
     host: 'localhost',
     username: 'root',
     password: 'root',
     port: 3306
   })
   ```

### rest 参数

> ES6 引入 **rest** 参数， 用于获取函数的实参。用来代替 **arguments**

1. 使用

   ```js
   function date (...args) {
     console.log(args)
   }
   rest('11', '22', '33')
   ```

2. rest 参数必须要放到参数最后

   ```js
   function fn (a, b, ...args){
     console.log(a)
     console.log(b)
     console.log(args)
   }
   fn(1, 2, 3, 4, 5, 6)
   ```

### 扩展运算符 

> ES6 引入 【...】 扩展运算符将【数组】转换为以逗号分隔的【参数序列】

```js
//声明一个数组
const tf = ['易烊千玺', '王源', '王俊凯']
//声明一个函数
function chuwan () {
  console.log(arguments)
}
chunean(...tf) // chunwan('易烊千玺', '王源', '王俊凯')
```

1. 数组的合并

   ```js
   const kuaizi = ['1', '2']
   const fenghuang = ['3', '4']
   const kuaizifenghuang = [...kuaizi, ...fenghuang]
   console.log(kuaizifenghuang) // ['1', '2', '3', '4']
   ```

2. 数组的克隆

   ```js
   const sanzihua = ['E', 'G', 'M']
   const sanyecao = [...sanzhihua]
   console.log(sanyecao) // ['E', 'G', 'M']
   ```

3. 将伪数组转化为真正的数组

   ```html
   <div></div>
   <div></div>
   <div></div>
   <script>
     const divs = document.querySelectorAll('div')
     const divArr = [...divs]
     console.log(divArr) //[div, div, div]
   </script>
   ```

### Symbol 基本使用

> ES6 引入一种新的原始数据类型 Symbol， 表示独一无二的值，它是 javaScript 语言的第七种数据类型，是一种类似于字符串的数据类型。

1. Symbol 特点

   1.  Symbol 的值是唯一的，用来解决命名冲突的问题
   2. Symbol 值不能与其他数据进行运算
   3. Symbol 定义的对象属性不能使用for...in循环遍历，但是可以使用 Reflect.ownKeys 来获取对象的所有键名

2. Symbol 的创建

   ```js
   //创建 Symbol
   let s = Symbol()
   // Symbol.for 创建
   let s2 = Symbol.for('123')
   
   //原始数据类型 USONB you are so niubility
   // U undefined
   // S string Symbol
   // O object
   // N null number
   // B boolean
   ```

3. 对象添加 Symbol 类型的属性

   ```js
   let game = {...}
   //声明一个对象
   let methods = {
     up: Symbol(),
     down: Synbol()
   }
   
   game[methods.up] = function () {
     console.log('111')
   }
   game[methods.down] = function () {
     console.log('222')
   }
   
   //
   let youxi = {
     name: "狼人杀",
     [Symbol('say')]: function () {
       console.log('111')
     },
     [Symbol('zibao')]: function () {
       console.log('222')
     }
   }
   ```

### 迭代器

1. 定义

   > 遍历器（`Iterator`）就是一种机制。它是一种接口，为各种不同的数据结构提 供统一的访问机制。任何数据结构只要部署 `Iterator` 接口，就可以完成遍历操作。

   - ES6 创造了一种新的遍历命令 `for...of` 循环，`Iterator` 接口主要供 `for...of` 消费。

   - 原生具备 `iterator`接口的数据(可用for of 遍历)

     - `Array`
     - `Arguments`
     - `Set`
     - `Map`
     - `String`
     - `TypedArray`
     - `NodeList`

     ```js
     //案例：使用 next() 方法遍历原生自带 iterator 接口的数据：
     // 遍历 Map
     const mp = new Map();
     mp.set('a', 1);
     mp.set('b', 2);
     mp.set('c', 3);
     let iter1 = mp[Symbol.iterator]();
     // next() 方法每执行一次，指针自增
     console.log(iter1.next()); // { value: [ 'a', 1 ], done: false }
     console.log(iter1.next()); // { value: [ 'b', 2 ], done: false }
     console.log(iter1.next()); // { value: [ 'c', 3 ], done: false }
     console.log(iter1.next()); // { value: undefined, done: true }
     // 遍历数组
     let xiyou = ['唐僧','孙悟空','猪八戒','沙僧'];
     let iter2 = xiyou[Symbol.iterator]();
     console.log(iter2.next()); // { value: '唐僧', done: false }
     console.log(iter2.next()); // { value: '孙悟空', done: false }
     console.log(iter2.next()); // { value: '猪八戒', done: false }
     console.log(iter2.next()); // { value: '沙僧', done: false }
     ```

     上面的案例只是为了证明他们自带 `iterator` 接口，实际上直接使用 `for...of` 方法遍历即可（`iterator` 接口为 `for...of`）服务。例如，可以使用 `for [k, v] of map` 来遍历 Map 数据结构中的键和值。

     ```js
     const mp = new Map();
     mp.set('a', 1);
     mp.set('b', 2);
     mp.set('c', 3);
     for (let [k, v] of mp) {
         console.log(k, v);
     }
     /*
     a 1
     b 2
     c 3
     */
     ```

2. 工作原理

   - 创建一个指针对象，指向当前数据结构的起始位置
   - 第一次调用对象的 `next` 方法，指针自动指向数据结构的第一个成员
   - 接下来不断调用 `next` 方法，指针一直往后移动，直到指向最后一个成员
   - 每调用 `next` 方法返回一个包含 `value` 和 `done` 属性的对象

   <span style='color:red'>应用场景：需要自定义遍历数据的时候，要想到迭代器。</span>

3. 自定义遍历数据

   我们可以通过给数据结构添加自定义 `[Symbol.iterator]()` 方法来使该数据结构能够直接被遍历，从而使 `for...of` 能够直接遍历指定数据，达到为 `for...of` 服务的功能。

   ```js
   // 需求：遍历对象中的数组
   const xiaomi = {
       uname: '小明',
       course: [ '高数', '大物', '英语', '数据库' ],
       // 通过自定义 [Symbol.iterator]() 方法
       [Symbol.iterator]() {
           // 初始指针对象指向数组第一个
           let index = 0;
           // 保存 xiaomi 的 this 值
           let _this = this;
           return {
               next: function () {
                   // 不断调用 next 方法，直到指向最后一个成员
                   if (index < _this.course.length) {
                       return { value: _this.course[index++], done: false };
                   } else {
                       // 每调用next 方法返回一个包含value 和done 属性的对象
                       return { value: undefined, done: true };
                   }
               }
           }
       }
   }
   // for...of直接遍历达到目的
   for (let v of xiaomi) {
       console.log(v);
   }
   ```

### Generator 生成器函数

> 生成器函数是 ES6 提供的一种 **异步编程解决方案**，语法行为与传统函数完全不同。

1. 生成器函数的声明和调用

   - `*` 的位置没有限制
   - 使用 `function * gen()` 和 `yield` 可以声明一个生成器函数。生成器函数返回的结果是迭代器对象，调用迭代器对象的 `next` 方法可以得到 `yield` 语句后的值。
   - 每一个 `yield` 相当于函数的暂停标记，也可以认为是一个分隔符，每调用一次 `next()`，生成器函数就往下执行一段。
   - `next` 方法可以传递实参，作为 `yield` 语句的返回值

   ```js
   //例如以下生成器函数中，3 个 yield 语句将函数内部分成了 4 段。
   function* generator() {
       console.log('before 111'); // 生成器第 1 段
       yield 111;
       console.log('before 222'); // 生成器第 1 段
       yield 222;
       console.log('before 333'); // 生成器第 1 段
       yield 333;
       console.log('after 333'); // 生成器第 1 段
   }
   let iter = generator();
   console.log(iter.next());
   console.log(iter.next());
   console.log(iter.next());
   console.log(iter.next());
   /*
   before 111
   { value: 111, done: false }
   before 222
   { value: 222, done: false }
   before 333
   { value: 333, done: false }
   after 333
   { value: undefined, done: true }
   */
   ```

2. 生成器函数的参数传递

   ```js
   function* generator(arg) {
       console.log(arg); // 生成器第 1 段
       let one = yield 111;
       console.log(one); // 生成器第 2 段
       let two = yield 222;
       console.log(two); // 生成器第 3 段
       let three = yield 333; 
       console.log(three); // 生成器第 4 段
   }
   
   let iter = generator('aaa'); // 传给生成器第 1 段
   console.log(iter.next());
   console.log(iter.next('bbb')); // 传给生成器第 2 段，作为这一段开始的 yield 语句返回值
   console.log(iter.next('ccc')); // 传给生成器第 3 段，作为这一段开始的 yield 语句返回值
   console.log(iter.next('ddd')); // 传给生成器第 4 段，作为这一段开始的 yield 语句返回值
   /*
   aaa
   { value: 111, done: false }
   bbb
   { value: 222, done: false }
   ccc
   { value: 333, done: false }
   ddd
   { value: undefined, done: true }
   */
   ```


### Promise

#### 1.**Promise 的定义和使用**

> `Promise` 是 ES6 引入的异步编程的新解决方案。语法上 Promise 是一个构造函数，用来封装异步操作并可以获取其成功或失败的结果。

一个 `Promise` 必然处于以下几种状态之一：

- 待定（`pending`）：初始状态，既没有被兑现，也没有被拒绝。
- 已兑现（`fulfilled`）：意味着操作成功完成。
- 已拒绝（`rejected`）：意味着操作失败。

`Promise` 的使用：

- Promise 构造函数：`new Promise((resolve, reject)=>{})`
- `Promise.prototype.then` 方法
- `Promise.prototype.catch` 方法

```js
let p = new Promise(function (resolve, reject) {
    // 使用 setTimeout 模拟请求数据库数据操作
    setTimeout(function () {
        // 这个异步请求数据库数据操作是否正确返回数据
        let isRight = true;
        if (isRight) {
            let data = '数据库中的数据';
            // 设置 Promise 对象的状态为操作成功
            resolve(data);
        } else {
            let err = '数据读取失败！'
            // 设置 Promise 对象的状态为操作失败
            reject(err);
        }
    }, 1000);
});
p.then(function (value) {
    console.log(value);
}, function (reason) {
    console.error(reason);
})
```

#### 2.**Promise 封装读取文件**

```js
// 使用 nodejs 的 fs 读取文件模块
const fs = require('fs');

const p = new Promise(function (resolve, reject) {
    fs.readFile('./resources/为学.txt', (err, data) => {
        // err 是一个异常对象
        if (err) reject(err);
        resolve(data);
    })
})

p.then(function (value) {
    // 转为字符串输出
    console.log(value.toString());
}, function (reason) {
    console.log('读取失败!!');
})
```

#### 3.**Promise 封装 Ajax 请求**

```js
const p = new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open('get', 'https://api.apiopen.top/getJoke');
    xhr.send();
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            if (xhr.status >= 200 && xhr.status < 300) {
                // 成功
                resolve(xhr.response);
            } else {
                // 失败
                reject(xhr.status);
            }
        }
    }
});

// 指定回调
p.then(function (value) {
    console.log(value);
}, function (reason) {
    console.error(reason);
})
```

####  4.**Promise.prototype.then 方法**

##### 1.`Promise` 的三种状态：

- 待定（`pending`）：初始状态，既没有被兑现，也没有被拒绝。
- 已兑现（`fulfilled`）：意味着操作成功完成。
- 已拒绝（`rejected`）：意味着操作失败。

##### 2.`Promise.prototype.then` 

> 方法返回的结果依然是 `Promise` 对象，**对象状态由回调函数的执行结果决定**。

具体情况如下：

1. 若 `then` 方法没有返回值，则 `then` 方法返回的对象的状态值为成功 `fulfilled`，返回结果值为 `undefined`。

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        // resolve('用户数据')
        reject('出错了');
    }, 1000);
})
// 未设定返回值
const res = p.then((value) => {
    console.log(value);
}, (reason) => {
    console.warn(reason);
})
// 打印 then 方法的返回值
console.log(res);
```

打印的结果：

![](D:\Desktop\文件\68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4861636b65722d432f506963747572652d426564406d61696e2f646f63732f6573362d332e35303475736d63346b6573302e706e67.png)

2. 如果回调函数中返回的结果是非 `Promise` 类型的属性，则 `then` 方法返回的对象，其状态为成功（`fulfilled`），返回结果值取决于 `then` 方法所执行的是哪个函数（`resolve` 或 `reject`）。

   ```js
   const p = new Promise((resolve, reject) => {
       setTimeout(() => {
           // resolve('用户数据')
           reject('出错了');
       }, 1000);
   })
    // 返回的非 Promise 对象
   const res = p.then((value) => {
       console.log(value);
       return '成功了！！';
   }, (reason) => {
       console.warn(reason);
       return '出错啦！！'
   })
   // 打印 then 方法的返回值
   console.log(res);
   ```

   打印结果：

   ![](D:\Desktop\文件\68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4861636b65722d432f506963747572652d426564406d61696e2f646f63732f6573362d342e32786463623178386a7961302e706e67.png)

3. 如果回调函数中返回的结果是 `Promise` 类型（`return new Promise()`），则 `then` 方法返回的 `Promise` 对象状态与该返回结果的状态相同，返回值也相同。

   ```js
   const p = new Promise((resolve, reject) => {
       setTimeout(() => {
           resolve('用户数据')
           // reject('出错了');
       }, 1000);
   })
   const res = p.then((value) => {
       console.log(value);
       // 返回 Promise 对象
       return new Promise((resolve, reject) => {
           resolve('（1）成功了！！！');
           // reject('（1）出错了！！！')
       })
   }, (reason) => {
       console.warn(reason);
       return new Promise((resolve, reject) => {
           // resolve('（2）成功了！！！');
           reject('（2）出错了！！！')
       })
   })
   // 打印 then 方法的返回值
   console.log(res);
   ```

   打印结果：

   ![](D:\Desktop\文件\68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4861636b65722d432f506963747572652d426564406d61696e2f646f63732f6573362d352e367a316d736d33787a7063302e706e67.png)

4. 如果回调函数中返回的结果是 `throw` 语句抛出异常，则 `then` 方法的对象的状态值为 `rejected`，返回结果值为 `throw` 抛出的字面量或者 `Error` 对象。

   ```js
   const p = new Promise((resolve, reject) => {
       setTimeout(() => {
           resolve('用户数据');
       }, 1000);
   });
   const res = p.then((value) => {
       console.log(value);
       return new Promise((resolve, reject) => {
           throw new Error('错误了！！');
       })
   });
   // 打印结果
   console.log(res);
   ```

   打印结果如下：

   ![](D:\Desktop\文件\68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4861636b65722d432f506963747572652d426564406d61696e2f646f63732f6573362d362e32633361696263366c3035632e706e67.png)

#### 5.Promise.prototype.catch

> `catch()` 方法返回一个 `Promise`，并且处理拒绝的情况。它的行为与调用 `Promise.prototype.then(undefined, onRejected)` 相同。

即：`obj.catch(onRejected);`

等同于：`obj.then(undefined, onRejected);`

语法：

```js
p.catch(onRejected);

p.catch(function(reason) {
   // 拒绝
});
```

举例：

```js
var p1 = new Promise(function (resolve, reject) {
    resolve('Success');
});

p1.then(function (value) {
    console.log(value); // "Success!"
    throw 'oh, no!';
}).catch(function (e) {
    console.log(e); // "oh, no!"
}).then(function () {
    console.log('有 catch 捕获异常，所以这句输出');
}, function () {
    console.log('没有 catch 捕获异常，这句将不会输出');
});

//输出结果：
//Success
//oh, no!
//有 catch 捕获异常，所以这句输出
```

### Set

> ES6 提供了新的数据结构 `Set`（集合）。它类似于数组，但 **成员的值都是唯一的**，集合实现了 `iterator` 接口，所以可以使用『扩展运算符』和『`for...of`』进行遍历。

1. Set 的定义和使用

   ```js
   //定义一个 Set 集合：
   let st1 = new Set();
   let st2 = new Set([可迭代对象]);
   ```

2. 集合（这里假设有一个集合 `st`）的属性和方法：

   1. `st.size`：返回集合个数
   2. `st.add(item)`：往集合中添加一个新元素 `item`，返回当前集合
   3. `st.delete(item)`：删除集合中的元素，返回 `boolean` 值
   4. `st.has(item)`：检测集合中是否包含某个元素，返回 `boolean` 值
   5. `st.clear()`：清空集合
   6. 集合转为数组：`[...st]`
   7. 合并两个集合：`[...st1, ...st2]`

3. 案例

   ```js
   let arr = [1,2,3,4,5,4,3,2,1]
   //1.数组去重
   let result = [...new Set(arr)]
   console.log(result);
   //2.交集
   let arr2 = [4,5,6,5,6]
   let result = [...new Set(arr)].filter(item => {
     let s2 = new Set(arr2)
     if (s2.has(item)) {
       return true
     } else {
       return false
     }
   })
   //或
   let result = [...new Set(arr)].filter(item => new Set(arr2).has(item))
   console.log(result);
   //3.并集
   let union = [...new Set([...arr, ...arr2])]
   console.log(union);
   //4.差集
   let diff = [...new Set(arr)].filter(item => !(new Set(arr2).has(item)))
   console.log(diff);
   ```

### Map

> ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。但是 “键” 的范围不限于字符串，各种类型的值（包括对象）都可以当作键。Map 也实现了 iterator 接口，所以可以使用『扩展运算符』和『for...of』进行遍历。

1. 定义一个 Map：

   ```js
   let mp1 = new Map();
   mp1.set('aaa', 111);
   mp1.set('bbb', 222);
   mp1.set('ccc', 333);
   
   let mp2 = new Map([
       ['aaa', 111],
       ['bbb', 222],
       ['ccc', 333]
   ]);
   
   console.log(mp1['aaa']); // 111
   console.log(mp2.get('bbb')); // 222
   ```

2. Map 的属性和方法：（`k` 为键，`v`为值）
   - `size`：返回 Map 的元素（键值对）个数
   - `set(k, v)`：增加一个键值对，返回当前 Map
   - `get(k)`：返回键值对的键值
   - `has()`：检测 Map 中是否包含某个元素
   - `clear()`：清空集合，返回 `undefined`

### class 类

> ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过class 关键字，可以定义类。基本上，ES6 的 `class` 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 `class` 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

#### 1.**创建类和对象**

1. 语法：

   ```js
   class ClassName {
       // class body
   }
   ```

2. 创建实例：

   ```js
   let obj = new ClassName();
   ```

3. <span style="color:red;font-size:16px">注意：类必须使用 `new` 实例化对象</span>

#### 2.**static 静态成员**

给成员属性或成员方法添加 `static`，该成员就成为静态成员，静态成员只能由该类调用。

```js
class Person {
    static eat() {
        console.log('eat');
    }
}
let  p = new Person();
Person.eat(); // eat
p.eat(); // 报错
```

##### 1.**extends 类继承和方法的重写**

> ES6 中直接使用 `extends` 语法糖（更简洁高级的实现方式）来实现继承，同时可以重写父类的方法，直接在子类中重新写一次要重写的方法即可覆盖父类方法。

```js
class Phone{
    //构造方法
    constructor(brand, price){
        this.brand = brand;
        this.price = price;
    }
    //父类的成员属性
    call(){
        console.log("我可以打电话!!");
    }
}

class SmartPhone extends Phone {
    //构造方法
    constructor(brand, price, color, size){
        super(brand, price);// Phone.call(this, brand, price)
        this.color = color;
        this.size = size;
    }

    photo(){
        console.log("拍照");
    }

    // 方法的重写
    call(){
        console.log('我可以进行视频通话');
    }
}

const xiaomi = new SmartPhone('小米',799,'黑色','4.7inch');
xiaomi.call();
xiaomi.photo();
```

##### 2.**getter 和 setter**

> 当属性拥有 `get`/`set` 特性时，属性就是访问器属性。代表着在访问属性或者写入属性值时，对返回值做附加的操作。而这个操作就是 `getter`/`setter` 函数。

1. 使用场景： `getter` 是一种语法，这种 `get` 将对象属性绑定到 **查询该属性时将被调用的函数**。适用于某个需要动态计算的成员属性值的获取。`setter` 则是在修改某一属性时所给出的相关提示。

   ```js
   class Test {
       constructor(log) {
           this.log = log;
       }
       get latest() {
           console.log('latest 被调用了');
           return this.log;
       }
       set latest(e) {
           console.log('latest 被修改了');
           this.log.push(e);
       }
   }
   
   let test = new Test(['a', 'b', 'c']);
   // 每次 log 被修改都会给出提示
   test.latest = 'd';
   // 每次获取 log 的最后一个元素 latest，都能得到最新数据。
   console.log(test.latest);
   ```

2. 以上输出：

   ```js
   latest 被修改了
   latest 被调用了
   [ 'a', 'b', 'c', 'd' ]
   ```

### 数值扩展

1. `Number.EPSILON` 是 JavaScript 表示的最小精度，一般用来处理浮点数运算。例如可以用于两个浮点数的比较。

   ```js
   let equal = (x, y) => Math.abs(x - y) < Number.EPSILON;
   console.log(0.1 + 0.2 === 0.3); // false
   console.log(equal(0.1 + 0.2, 0.3)); // true
   ```

2. 二进制和八进制：二进制以 `0b` 开头，八进制以 `0o` 开头。

   ```js
   let b = 0b1010;
   let o = 0o777;
   let d = 100;
   let x = 0xff;
   console.log(x);
   ```

3. `Number.isFinite` 检测一个数值是否为有限数。

   ```js
   console.log(Number.isFinite(100)); // false
   console.log(Number.isFinite(100 / 0)); // true
   console.log(Number.isFinite(Infinity)); // false
   ```

4. Number.parseInt 和 Number.parseFloat
   >ES6 给 `Number` 添加了 `parseInt` 方法，`Number.parseInt` 完全等同于 `parseInt`。将字符串转为整数，或者进行进制转换。`Number.parseFloat` 则等同于 `parseFloat()`

   ```js
   Number.parseInt === parseInt; // true
   Number.parseFloat === parseFloat; // true
   ```

   ```js
   Number.parseInt(s, base);
   ```

   - `s`：待转换的字符串
   - `base`：进位制的基数

   ```js
   console.log(Number.parseInt('5211314love')); // 5211314
   console.log(Number.parseFloat('3.1415926神奇')); // 3.1415926
   ```

5. `Number.isInteger()` 判断一个数是否为整数。

   ```js
   console.log(Number.isInteger(5)); // true
   console.log(Number.isInteger(2.5)); // false
   ```

6. `Math.trunc()` 将数字的小数部分抹掉。

   ```js
   console.log(Math.trunc(3.5)); // 3
   ```

7. `Math.sign` 判断一个数到底为正数 负数 还是零

### 对象方法扩展

> ES6 新增了一些 `Object` 对象的方法。

1. Object.is()

   1. `Object.is()` 方法判断两个值是否完全相同。`Object.is` 比较两个值是否严格相等，与 `===` 行为 **基本一致**。返回一个 `Boolean` 类型。

      ```js
      Object.is(value1, value2);
      ```

   2. `Object.is()` 方法判断两个值是否为同一个值。如果满足以下条件则两个值相等：

      - 都是 `undefined`
      - 都是 `null`
      - 都是 `true` 或 `false`
      - 都是相同长度的字符串且相同字符按相同顺序排列
      - 都是相同对象（意味着每个对象有同一个引用）
      - 都是数字且
        - 都是 `+0`
        - 都是 `-0`
        - 都是 `NaN`
        - 或都是非零而且非 `NaN` 且为同一个值

      与 `==` 运算不同。 `==` 运算符在判断相等前对两边的变量（如果它们不是同一类型）进行强制转换 (这种行为的结果会将 `"" == false` 判断为 `true`)，而 `Object.is` 不会强制转换两边的值。

      与 `===`算也不相同。 === 运算符 (也包括 `==` 运算符) 将数字 `-0` 和 `+0` 视为相等，而将 `Number.NaN` 与 `NaN` 视为不相等。

2.  Object.assign

   `Object.assign` 对象的合并，相当于浅拷贝。

   ```js
   const config1 = {
       host: 'localhost',
       port: 3306,
       name: 'root',
       pass: 'root',
       test: 'test'
   };
   const config2 = {
       host: 'http://atguigu.com',
       port: 33060,
       name: 'atguigu.com',
       pass: 'iloveyou',
       test2: 'test2'
   }
   console.log(Object.assign(config1, config2));
   ```

3. Object.setPrototypeOf 和 Object.getPrototypeof

   `Object.setPrototypeOf` 用于设置对象的原型对象，`Object.getPrototypeof` 用于获取对象的原型对象，相当于 `__proto__`。

   ```js
   const school = {
       name: '尚硅谷'
   }
   const cities = {
       xiaoqu: ['北京','上海','深圳']
   }
   Object.setPrototypeOf(school, cities);
   console.log(Object.getPrototypeOf(school));
   console.log(school);
   ```
   

### ES6 模块化

> 模块化是指将一个大的程序文件，拆分成许多小的文件，然后将小文件组合起来。

####1.模块化的好处

模块化的优势有以下几点：

- 防止命名冲突

- 代码复用

- 高维护性

####2.ES6 之前的模块化规范有：

- CommonJS => NodeJS、Browserify
- AMD => requireJS
- CMD => seaJS

####3.ES6 模块化语法

1. 模块功能主要由两个命令构成：`export` 和 `import`。

   1. `export` 命令用于规定模块的对外接口
   2. `import` 命令用于输入其他模块提供的功能

2. 模块导出数据语法

   1. 单个导出

      ```js
      // 单个导出
      export let uname = 'Rick';
      export let sayHello = function () {
          console.log('Hi, bro!');
      }
      ```

   2. 合并导出

      ```js
      let uname = 'Rick';
      let sayHello = function () {
          console.log('Hi, bro!');
      }
      // 合并导出
      export { uname, sayHello };
      ```

   3. 默认导出

      ```js
      // 默认导出
      export default {
          uname: 'Rick',
          sayHello: function () {
              console.log('Hi, bro!');
          }
      }
      ```

3. 模块导入数据语法

   1. 通用导入方式

      ```js
      import * as m1 from './js/m1.js';
      import * as m2 from './js/m2.js';
      import * as m3 from './js/m3.js';
      ```

   2. 解构赋值导入

      ```js
      import { uname, sayHello } from './js/m1.js';
      // 有重复名可以设置别名
      import { uname as uname2, sayHello as sayHello2 } from './js/m2.js';
      console.log(uname);
      // 配合默认导出
      import {default as m3} from "./src/js/m3.js";
      ```

   3. 简便方式导入，针对默认暴露

      ```js
      import m3 from "./src/js/m3.js";
      ```

   4. ES6 使用模块化方式二

      将文件导入都写进一个 app.js 文件中，然后在里面写入要导入的模块。app.js 中的内容如下：

      ```js
      import * as m1 from './js/m1.js';
      import * as m2 from './js/m2.js';
      import * as m3 from './js/m3.js';
      
      console.log(m1);
      console.log(m2);
      console.log(m3);
      ```

      在 index.html 中引入 app.js 文件内容：

      ```js
      <script src="./app.js" type="module"></script>
      ```

####4.使用 babel 对模块化代码转换

有的浏览器不支持 ES6 语法，这时候就需要使用 babel 来将其转换成 ES5 等价语法。

1. 安装工具

```node
npm i babel-cli babel-preset-env browserify(webpack) -D
```

2. 编译

```node
npx babel src/js -d dist/js --presets=babel-preset-env
```

3. 打包

```node
npx browserify dist/js/app.js -o dist/bundle.js
```

#### 5.ES6 模块化引入 npm 安装的包

```
npm install jquery
```

再通过 `import` 导入即可。

 [![es6-7](https://camo.githubusercontent.com/e30c97d96497fbc4d5e9f23e587bd1ad594c1e7b218e1bb38640bfa200fcad46/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4861636b65722d432f506963747572652d426564406d61696e2f646f63732f6573362d372e323136696f6d647378396d6f2e706e67)](https://camo.githubusercontent.com/e30c97d96497fbc4d5e9f23e587bd1ad594c1e7b218e1bb38640bfa200fcad46/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f4861636b65722d432f506963747572652d426564406d61696e2f646f63732f6573362d372e323136696f6d647378396d6f2e706e67)



## ES7

### 1.Array.prototype.includes

`includes` 方法用来检测数组中是否包含某个元素，返回布尔类型值。

### 2. 指数运算符

在 ES7 中引入指数运算符 `**`，用来实现幂运算，功能与 `Math.pow(a, b)` 结果相同。

```js
2 ** 3 // 8
Math.pow(2, 3) // 8
```

## ES8

### 1.async 和 await

> `async` 和 `await` 两种语法结合可以让异步代码像同步代码一样。（即：看起来是同步的，实质上是异步的。）

#### 1.async

1. `async` 声明（`function`）的函数成为 async 函数，语法：

   ```js
   async function funcName() {
       //statements 
   }
   ```

2. `async` 内部可以使用 `await`，也可以不使用。 `async` 函数的返回值是一个 `Promise` 对象，因此执行这个函数时，可以使用 `then` 和 `catch` 方法。 根据 **函数体内部** 的返回值， `async` 函数返回值具体情况如下：

   - 函数体内不返回任何值，则 `async` 函数返回值为一个成功（`fulfilled`）的 `Promise` 对象，状态值为 `undefined`。

     ```js
     let a = async function() {}
     let res = a()
     console.log(res)
     // Promise{<fullfilled>: undefined}
     ```

   - 返回结果不是一个 `Promise` ，则 `async` 函数返回值为一个成功（`fulfilled`）的 `Promise` 对象，状态值为这个内部返回值。

     ```js
     let a = async function () {
       return 'hello'
     }
     let res = a()
     console.log(res) 
     // Promise{<fullfilled>: 'hello'}
     ```

   - 内部抛出错误，则 `async` 函数返回值为一个失败的 `Promise` 对象。

     ```js
     let a = async function foo() {
       throw new Error('出错了')
     }
     a().catch(reason => {
       console.log(reason)
     })
     ```

   - 若函数内部返回值是一个 `Promise` 对象，则 `async` 函数返回值的状态取决于这个 `Promise` 对象。

     ```js
     let a = async function () {
       return new Promise((resolve, reject) => {
         resolve("成功")
       })
     }
     a().then(value => {
       console.log(value)
     })
     ```

#### 2.await

> `await` 相当于一个运算符，右边接一个值。一般为一个 `Promise` 对象，也可以是一个非 `Promise` 类型。当右接一个非 `Promise` 类型，`await` 表达式返回的值就是这个值；当右接一个 `Promise` 对象，则 `await` 表达式会阻塞后面的代码，等待当前 `Promise` 对象 `resolve` 的值。

> `await` 必须结合 `async` 使用，而 `async` 则不一定需要 `await`。 `async` 会将其后的函数的返回值封装成一个 `Promise` 对象，而 `await` 会等待这个 `Promise` 完成，然后返回 `resolve` 的结果。当这个 `Promise` 失败或者抛出异常时，需要时使用 `try-catch` 捕获处理。

`Promise` 使用链式调用解决了传统方式回调地狱的问题，而 `async-await` 又进一步优化了代码的可读性。

```js
const p = new Promise((resolve, reject)=>{
  resolve('成功')
})
async function main() {
  let res = await p
  console.log(res)
}
main()
// '成功'
	
const p = new Promise((resolve, reject)=>{
  reject('失败')
})
async function main() {
  try {
    let res = await p
    console.log(res)
  } catch(e) {
    console.log(e)
  }
}
main()
// '失败'
```

###  2.Object.values 和 Object.entries

``Object.values()``方法返回一个给定对象的所有可枚举属性值的数组，类似于``Object.keys()``，只是前者返回属性值，后者返回键值组合的数组。

  ```
  let obj = {
    a: 1,
    b: {1:2},
    c: [1,2,3]
  }
  console.log(Object.values(obj))
  // [1, {1: 2}, [1,2,3]]
  console.log(Object.keys(obj))
  // ['a', 'b', 'c']
  ```

``Object.entries()``方法返回一个给定对象自身可遍历属性``[key,value]``的数组（数组元素也是一个个的数组的数组）

  ```
  const obj = {a: 1, b: 2, c: 3};
  console.log(Object.entries(obj))
  // [ [ 'a', 1 ], [ 'b', 2 ], [ 'c', 3 ] ]
  ```

返回的是一个数组，这样就可以使用``for...of``遍历了。

  ```
  const obj = { a: 1, b: 2, c: 3 };
  for (let [k, v] of Object.entries(obj)) {
    console.log(k, v)
  }
  ```

## ES9

### 1.rest 参数

> `Rest` 参数与`spread` 扩展运算符在 ES6 中已经引入, 不过 ES6 中只针对于数组,在 ES9 中为对象提供了像数组一样的 `Rest` 参数和扩展运算符

```js
function connect({ host, port, ...user }) {
  console.log(host); // 127.0.0.1
  console.log(port); // 3306
  console.log(user); //{username: 'root', password: 'root', type: 'master'}
}

connect({
  host: '127.0.0.1',
  port: 3306,
  username: 'root',
  password: 'root',
  type: 'master'
})

const skillOne = {
  q: '天音波'
}
const skillTow = {
  e: '天音波'
}
const skillThree = {
  w: '天音波'
}
const skillFour = {
  r: '天音波'
}

const mangseng = {...skillOne,...skillTow,...skillThree,...skillFour}
console.log(mangseng); //{q: '天音波', e: '天音波', w: '天音波', r: '天音波'}
```

### 2.正则扩展

1. 命名捕获分组

   ```js
   let str = '<a href="http://www.gaoxingyu.com">哈哈哈</a>'
   const reg = /<a href="(?<url>.*)">(?<text>.*)<\/a>/
   const result = reg.exec(str)
   console.log(result);
   
   // 0: "<a href=\"http://www.gaoxingyu.com\">哈哈哈</a>"
   // 1: "http://www.gaoxingyu.com"
   // 2: "哈哈哈"
   // groups:
   // url: "http://www.gaoxingyu.com"
   // text: "哈哈哈"
   // index: 0
   // input: "<a href=\"http://www.gaoxingyu.com\">哈哈哈</a>"
   ```

2. 反向断言

   ```js
   //声明字符串
       let str = 'JS5211314你知道吗999啦啦啦'
       正向断言
       const reg = /\d+(?=啦)/
       const result = reg.exec(str)
       console.log(result); //['999', index: 13, input: 'JS5211314你知道吗999啦啦啦', groups: undefined]
   
       //反向断言
   
       const reg = /(?<=吗)\d+/
       const result = reg.exec(str)
       console.log(result); //['999', index: 13, input: 'JS5211314你知道吗999啦啦啦', groups: undefined]
   ```

3. dotAll模式

   ```js
   //声明正则
   const reg = /<li>.*?<a>(.*?)<\/a>.*?<p>(.*?)<\/p>/gs
   //执行匹配
   let result
   let data = []
   while (result = reg.exec(str)) {
     console.log(result);
     data.push({title:result[1],time:result[2]})
   }
   
   //输出结果
   console.log(data);
   // 0:
   // time: "上映日期：1994-09-10"
   // title: "肖生客的救赎"
   // [[Prototype]]: Object
   // 1:
   // time: "上映日期：1994-07-06"
   // title: "阿甘正传"
   // [[Prototype]]: Object
   // length: 2
   ```

## ES10

### 1.Object.fromEntries

> Object.fromEntries() 方法把可迭代对象的键值对列表转换为一个对象。

语法：

```js
Object.fromEntries(iterable)
```

- `iterable`：类似 Array 、 Map 或者其它实现了可迭代协议的可迭代对象。

- 返回值：一个由该迭代对象条目提供对应属性的新对象。

- 相当于 `Object.entries` （ES8）的逆运算。

  ```js
  const mp = new Map([
    [1, 2],
    [3, 4]
  ])
  const obj = Object.fromEntries(mp)
  console.log(obj)
  // { '1': 2, '3': 4 }
  
  const arr = [[1, 2]]
  console.log(Object.fromEntries(arr))
  // {'1': 2}
  ```

### 2.trimStart() 和 trimEnd()

- `trimStart()` 去除字符串开头连续的空格（`trimLeft` 是此方法的别名）
- `trimEnd()` 去除字符串末尾连续的空格（`trimRight` 是此方法的别名）

### 3.Array.prototype.flat 和 Array.prototype.flatMap

1. `Array.prototype.flat(i)`：展平一个多维数，`i` 为要展开的层数，默认为1，即展开一层。

   ```js
   let arr1 = [1, 2, [3, [4, 5]]]
   console.log(arr1.flat(1)) 
   // [1,2,3,[4,5]
   let arr2 = [1, [2, 3, [4, 5]]]
   console.log(arr2.flat(2))
   // [1,2,3,4,5]
   ```

   使用 `Infinity` 作为深度，展开任意深度的嵌套数组

   ```js
   [1, [2, 3, [4, 5]]].flat(Infinity)
   // [1, 2, 3, 4, 5, 6]
   ```

   也可以使用 `flat` 来去除数组空项

   ```js
   let arr = [1,2,3,,4]
   arr.flat() // [1,2,3,4]
   ```

2. `Array.prototype.flatMap`：相当于 `map` 和 `flat` 的结合，方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。

   ```js
   let arr = [1,2,3,4]
   let res1 = arr.map(x => [x ** 2])
   console.log(res1)
   // [[1],[4],[9],[16]]
   let res2 = arr.flatMap(x => [x ** 2])
   console.log(res2)
   // [1,4,9,16]
   ```

### 4.Symbol.prototype.description

使用 `Symbol()` 创建的 `Symbol` 字面量，可以直接使用 `description` 获取该字面量的描述。

```js
let sym = Symbol('hello')
console.log(sym.description)
// hello
```

## ES11

### 1.类的私有属性

> ES11 提供了类的私有属性，在类的外部无法访问该属性。只有再类的内部能访问。

```js
class Person{
  //公有属性
  name;
  //私有属性
  #age;
  #weight;
  //构造方法
  constructor(name, age, weight){
    this.name = name;
    this.#age = age;
    this.#weight = weight;
  }

  intro(){
    console.log(this.name);
    console.log(this.#age);
    console.log(this.#weight);
  }
}

//实例化
const girl = new Person('晓红', 18, '45kg');

// 外部无法直接访问
// console.log(girl.name);
// console.log(girl.#age);
// console.log(girl.#weight);

girl.intro();
```

### 2.allSettled

> 该 `Promise.allSettled()` 方法返回一个在所有给定的 `promise` 都已经 `fulfilled` 或 `rejected` 后的 `promise`，并带有一个对象数组，每个对象表示对应的 `promise` 结果。`allSettled` 方法返回的 `Promise` 对象始终是成功（`fulfilled`）的。

使用场景：

- 有多个彼此不依赖的异步任务成功完成时使用。
- 想得到每个 `promise` 的结果时使用。

对比于 `Promise.all()`，`all()` 也接受一个 `Promise` 对象数组参数，只要有一个失败（`rejected`），那么返回的 `Promise` 对象就是失败（`rejected`）的。
使用场景：

- 传进去的 `Promise` 对象彼此依赖，且需要在其中任何一个失败的时候停止。

两个 `Promise` 都是成功的情况：

```js
let p1 = new Promise((resolve, reject) => {
  resolve('用户数据-1')
})

let p2 = new Promise((resolve, reject) => {
  resolve('订单数据-2')
})

let res1 = Promise.allSettled([p1, p2])
let res2 = Promise.all([p1, p2])
console.log(res1)
console.log(res2)
```

输出结果： ![es11-1](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/es11-1.2fgw7vvkb0kk.png)

一个成功，一个失败：

```js
let p1 = new Promise((resolve, reject) => {
  resolve('用户数据-1')
})

let p2 = new Promise((resolve, reject) => {
  reject('失败了')
})

let res1 = Promise.allSettled([p1, p2])
let res2 = Promise.all([p1, p2])
console.log(res1)
console.log(res2)Copy to clipboardErrorCopied
```

打印结果： ![ES11-2](https://cdn.jsdelivr.net/gh/Hacker-C/Picture-Bed@main/docs/ES11-2.17q27y7sy9mk.png)

### 3.matchAll

> `matchAll()` 方法返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器。

```js
const regexp = /t(e)(st(\d?))/g;
const str = 'test1test2';

const array = [...str.matchAll(regexp)];

console.log(array[0]);
// expected output: Array ["test1", "e", "st1", "1"]

console.log(array[1]);
// expected output: Array ["test2", "e", "st2", "2"]
```

### 4.可选链

1. 定义

   > 可选链 `?.` 是一种访问嵌套对象属性的安全的方式。即使中间的属性不存在，也不会出现错误。
   
   原则：如果可选链 `?.` 前面的部分是 `undefined` 或者 `null`，它会停止运算并返回该部分。

   ```js
   let user = {
     address: {
     }
   }
   console.log( user?.address?.street ); // undefined（不报错）
   ```

2. 短路效应

   > 短路效应：正如前面所说的，如果 `?.` 左边部分不存在，就会立即停止运算（“短路效应”）。所以，如果后面有任何函数调用或者副作用，它们均不会执行。
   
   这有和 `&&` 的作用类似，但上述改用 `&&` 会显得代码冗余度高：

   ```js
   console.log(user && user.address && user.address.street)
   ```
   
3. 其它变体：?.()，?.[]

   > 可选链 `?.` 不是一个运算符，而是一个特殊的语法结构。它还 **可以与函数和方括号一起使用**。

   例如，将 `?.()` 用于调用一个可能不存在的函数（即使不存在也不报错）。

   ```js
   function foo() {
     console.log('hello')
   }
   foo?.()
   // helloCopy to clipboardErrorCopied
   ```

   `?.[]` 允许从一个可能不存在的对象上安全地读取属性。（即使不存在也不报错）。

   ```js
   let obj = {
     key: 123
   }
   console.log(obj?.['key'])
   // 123
   ```
   

### 5.动态 import 导入

```js
const btn = document.getElementById('btn');

btn.onclick = function(){
  import('./hello.js').then(module => {
    module.hello();
}
```

### 6.BigInt

> `BigInt` 是一种特殊的数字类型，它提供了对任意长度整数的支持。

创建 `bigint` 的方式有两种：在一个整数字面量后面加 `n` 或者调用 `BigInt` 函数，该函数从字符串、数字等中生成 `bigint`。

```js
let n1 = 123n
let n2 = 456n
let n3 = BigInt(789)
console.log(typeof n1) // bigint
console.log(n1+n2) // 579n
console.log(n2+n3) // 1245n
```

比较运算符：

- 例如 

  ``<``和 ``>``，使用它们来对``bigint``和 nu`mber 类型的数字进行比较没有问题：

  ```js
  alert( 2n > 1n ); // true
  alert( 2n > 1 ); // trueCopy to clipboardErrorCopied
  ```

- 但是请注意，由于``number``和``bigint``属于不同类型，它们可能在进行``==``比较时相等，但在进行``===``（严格相等）比较时不相等：

  ```js
  alert( 1 == 1n ); // true
  alert( 1 === 1n ); // false
  ```

### 7.globalThis

> 全局对象提供可在任何地方使用的变量和函数。默认情况下，这些全局变量内置于语言或环境中。
> 在浏览器中，它的名字是 `window`，对 Node.js 而言，它的名字是 `global`，其它环境可能用的是别的名字。
> ES11中 `globalThis` 被作为全局对象的标准名称加入到了 JavaScript 中，所有环境都应该支持该名称。所有主流浏览器都支持它。
> 使用场景： 假设我们的环境是浏览器，我们将使用 `window`。如果你的脚本可能会用来在其他环境中运行，则最好使用 `globalThis`。
