[TOC]

# jQuery

## jQuery 概述

1. **JavaScript 库**
   1. 常见的 JavaScript 库
      - jQuery
      - prototype
      - YUI
      - Dojo
      - Ext JS
      - zepto (移动端)
2. **jQuery概念**
   1. jQuery 是一个快速, 简洁的 JavaScript 库

## jQuery 基本使用

1. **jQuery 的入口函数**

   ```javascript
   1.
   $(function () {
       ... //此处是页面DOM加载完成的入口
   });
       
   2. 
   $(document).ready(function () {
       ... //此处是页面DOM加载完成的入口
   });
   ```

2. **jQuery 的顶级对象 $**

   1. $ 是 jQuery 的别称, 在代码中可以使用jQuery 代替 $, 一般为了方便,通常直接使用 $
   2. $ 是 jQuery 的顶级对象, 相当于JavaScript 中的 window

3. **jQuery 对象和 DOM 对象**

   1. jQuery 方法获取的元素就是 jQuery 对象
   2. jQuery 对象本质是:利用 $ 对 DOM 对象包装后产生的对象(伪数组形式储存)

   3. jQuery  对象与 DOM 对象相互转换

      ```html
      <video src="mov.mp4" muted></video>
      <script>
          // 1. DOM对象转换为 jQuery对象
          // (1) 我们直接获取视频，得到就是jQuery对象
          // $('div')
          $('video');
          // (2) 我们已经使用原生js 获取过来 DOM对象
          var myvideo = document.querySelector('video');
          // $(myvideo).play();  jquery里面没有play 这个方法
          // 2.  jQuery对象转换为DOM对象
          // $('div')[index] index 是索引号
          // $('div').get(index) 
          $('video')[0].play()
          $('video').get(0).play()
      </script>
      ```

## jQuery 常用 API

### jQuery 选择器

1. **jQuery 基础选择器**

   `$（"选择器"）// 里面直接写CSS 选择器`

2. **jQuery 层级选择器**

   ```javascript
   // 1. 子代选择器
   $("ul>li");
   // 2. 后代选择器
   $("ul li");
   ```

3. **隐式迭代**

   1. 隐式迭代就是把匹配的所有元素内部进行遍历循环，给每一个元素添加css这个方法

4. **jQuery 筛选选择器**

   | 语法       | 用法              | 描述                               |
   | ---------- | ----------------- | ---------------------------------- |
   | :first     | $("li:first")     | 获取第一个li'                      |
   | :last      | $("li:last")      | 获取最后一个li                     |
   | :eq(index) | $("li:eq(index)") | 获取到的li元素中索引号为2的元素    |
   | :odd       | $("li:odd")       | 获取到的li元素中索引号为奇数的元素 |
   | :even      | $("li:even")      | 获取到的li元素中索引号为偶数的元素 |

   | 语法                   | 用法                           | 说明                                                    |
   | ---------------------- | ------------------------------ | ------------------------------------------------------- |
   | **parent()**           | $("li").parent();              | 查找父级                                                |
   | **children(selector)** | $("ul").children("li")         | 相当于$("u1>1i"),最近一级（亲儿子）                     |
   | **find(selector)**     | $("ul").find("1i");            | 相当于$("u"),后代选择器                                 |
   | **siblings(selector)** | $(".first").siblings("li");    | 查找兄弟节点，不包括自己本身                            |
   | nextAll([expr])        | $(".first").nextAll()          | 查找当前元素之后所有的同辈元素                          |
   | prevtAll([expr])       | $(".1ast").prevA.11()          | 查找当前元素之前所有的同辈元素                          |
   | hasClass(class)        | $('div').hasclass("protected") | 检查当前的元素是否含有某个特定的类，如 果有，则返回true |
   | **eq(index)**          | $("1i").eq(2);                 | 相当于$("1i:eq(2)"),index从0开始                        |

5. **链式编程**

   `$(this).css('color', 'red').sibling().css('color','');`

###  jQuery 样式操作

1. **操作 CSS 方法**

   1. 参数只写属性名,则是返回属性值

      `$(this).css("color");`

   2. 参数是 **属性名, 属性值, 逗号分隔**, 是设置一组样式,属性必须加引号,值如果是数字可以不用跟单位和引号

      `$(this).css("color","red");`

   3. 参数可以是对向行式,方便设置多组样式, 属性名和属性值用冒号隔开,属性可以不加引号

      ```javascript
      $(this).css({"color":"white","font-size":"20px"});
      
      $("div").css({
          width: 400,
          height: 400,
          backgroundColor: "red"
          // 如果是复合属性则必须采取驼峰命名法，如果值不是数字，则需要加引号
      })
      ```

2. **设置类样式方法**

   1. 添加类

      `$("div").addClass("current");`

   2. 移除类

      `$("div").removeClass("current");`

   3. 切换类

      `$("div").toggleClass("current");`

3. **类操作与className区别**

   1. 原生JS中className 会覆盖元素原先里面的类名
   2. jQuery 里面类操作只是对指定类进行操作, 不影响原先的类名

### jQuery 效果

1. **显示隐藏**

   1. **显示**语法规范

      `show([speed,[easing],[fn]])`

   2. **隐藏**语法规范

      `hide([speed,[easing],[fn]])`

   3. **切换**语法规范

      `toggle([speed,[easing],[fn]])`

   4. 参数

      1. 参数都可以省略， 无动画直接显示。
      2. speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
      3. easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
      4. fn: 回调函数，在动画完成时执行的函数，每个元素执行一次。

2. **滑动**

   1. **下拉滑动**语法规范

      `slideDown([speed,[easing],[fn]])`

   2. **上拉滑动**语法规范

      `slideUp([speed,[easing],[fn]])`

   3. **切换滑动**语法规范

      `slideToggle([speed,[easing],[fn]])`

   4. 参数

      1. 参数都可以省略， 无动画直接显示。
      2. speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
      3. easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
      4. fn: 回调函数，在动画完成时执行的函数，每个元素执行一次。

3. **事件切换**(鼠标经过和离开的复合写法)

   1. 语法规范

      `hover([over,]out)`

   2. 参数

      1. over:鼠标移到元素上要触发的函数（相当于mouseenter）
      2. out:鼠标移出元素要触发的函数（相当于mouseleave）
      3. 如果只写一个函数，则鼠标经过和离开都会触发它

4. **动画队列及其停止排队方法**

   1. 动画或效果队列

      动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。

   2. 停止排队

      `stop()`

      stop() 方法用于停止动画或效果。

      注意： stop() 写到动画或者效果的**前面， 相当于停止结束上一次的动画。**

5. **淡入淡出效果**

   1. 淡入效果语法规范

      `fadeIn([speed,[easing],[fn]])`

   2. 淡出效果语法规范

      `fadeOut([speed,[easing],[fn]])`

   3. 淡入淡出切换效果语法规范

      `fadeToggle([speed,[easing],[fn]])`

   4. **参数**

      1. 参数都可以省略。
      2. speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
      3. easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
      4. fn: 回调函数，在动画完成时执行的函数，每个元素执行一次。

6. **渐进方式调整到指定的不透明度**

   1. 语法规范

      `fadeTo([[speed],opacity,[easing],[fn]])`

   2. 效果参数

      1. **opacity 透明度必须写，取值 0~1 之间。**
      2. **speed：**三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。必须写
      3. easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
      4. fn: 回调函数，在动画完成时执行的函数，每个元素执行一次。

7. **自定义动画** **animate**

   1. 语法规范

      `animate(params,[speed],[easing],[fn])`

   2. 参数

      1. **params: 想要更改的样式属性，以对象形式传递，必须写。 属性名可以不用带引号， 如果是复合属性则需要采取驼峰命名法 borderLeft。**其余参数都可以省略。
      2. speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
      3. easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
      4. fn: 回调函数，在动画完成时执行的函数，每个元素执行一次。

## jQuery 属性操作

### 设置或获取元素固有属性值 prop()

1. **获取属性语法**

   `prop(''属性'')`

2. **设置属性语法**

   `prop(''属性'', ''属性值'')`

### 设置或获取元素自定义属性值 attr()

1. **获取属性语法**

   `attr(''属性'')   // 类似原生 getAttribute()`

2. **设置属性语法**

   `attr(''属性'', ''属性值'')  // 类似原生 setAttribute()`

### 数据缓存 data()

1. **附加数据语法**

   `data(''name'',''value'')  // 向被选元素附加数据  `

2. **获取数据语法**

   `date(''name'')       //  向被选元素获取数据  `

## jQuery 内容文本值

1. **普通元素内容html()（ 相当于原生inner HTML)**

   `html()       // 获取元素的内容`

   `html(''内容'')  // 设置元素的内容`

2. **普通元素文本内容text()  (相当与原生innerText)**

   `text()           // 获取元素的文本内容`

   `text(''文本内容'')  // 设置元素的文本内容`

3. **表单的值 val()（ 相当于原生value)**

   `val()       // 获取表单的值`

   `val(''内容'')  // 设置表单的值`

## jQuery 元素操作

### 遍历元素

1. **语法1：**

   `$("div").each(function (index, domEle) { xxx; }）    `

   1. each() 方法遍历匹配的每一个元素。主要用DOM处理。 each 每一个

   2. 里面的回调函数有2个参数： index 是每个元素的索引号; demEle 是**每个DOM元素对象，不是jquery对象**

   3. **要想使用jquery方法，需要给这个dom元素转换为jquery对象 $(domEle)**

2. **语法2：**

   `$.each(object，function (index, element) { xxx; }）`

   1. $.each()方法可用于遍历任何对象。主要用于数据处理，比如数组，对象

   2. 里面的函数有2个参数： index 是每个元素的索引号; element 遍历内容

### 创建元素

1. **语法**

   `$(''<li></li>'');  `

### 添加元素

1. **内部添加**

   `element.append(''内容'') `

   把内容放入匹配元素内部最**后面**，类似原生 appendChild

   `element.prepend(''内容'') `

   把内容放入匹配元素内部最**前面**。

2. **外部添加**

   `element.after(''内容'')    // 把内容放入目标元素后面`

   `element.before(''内容'')   // 把内容放入目标元素前面 `

### 删除元素

1. **语法**

   `element.remove()  // 删除匹配的元素（本身）`

   `element.empty()  //  删除匹配的元素集合中所有的子节点`

   `element.html('''')  //  清空匹配的元素内容`

   1. **remove 删除元素本身。**
   2. **empt() 和 html('''') 作用等价，都可以删除元素里面的内容，只不过 html 还可以设置内容。**

## jQuery 尺寸、位置操作

### jQuery 尺寸

1. 语法

   `width()/height()`

   取得匹配元素宽度和高度值只算width/height

2. 语法

   `innerWidth()/innerHieght()`

   取得匹配元素宽度和高度值包含padding

3. 语法

   `outerWidth()/outerHeight()`

   取得匹配元素宽度和高度值包含padding、border

4. 语法

   `outerWidth(true)/outerHeight(true)`

   取得匹配元素宽度和高度值包含padding、borde、margin

5. **注意**

   ​	以上参数为空，则是获取相应值，返回的是数字型。

   ​	如果参数为数字，则是修改相应值。

   ​	参数可以不必写单位。

### jQuery 位置

1. **offset()设置或获取元素偏移**
   1. offset() 方法设置或返回被选元素相对于**文档**的偏移坐标，跟父级没有关系。
   2. 该方法有2个属性 left、top 。offset().top 用于获取距离文档顶部的距离，offset().left 用于获取距离文档左侧的距离。
   3. 可以设置元素的偏移：offset({ top: 10, left: 30 });
2. **position() 获取元素偏移**
   1. position() 方法用于返回被选元素相对于**带有定位的父级**偏移坐标，如果父级都没有定位，则以文档为准。
   2. 该方法有2个属性 left、top。position().top 用于获取距离定位父级顶部的距离，position().left 用于获取距离定位父级左侧的距离。
   3. 该方法只能获取。
3. **scrollTop()/scrollLeft()设置或获取元素被卷去的头部和左侧**
   1. scrollTop() 方法设置或返回被选元素被卷去的头部。
   2. 不跟参数是获取，参数为不带单位的数字则是设置被卷去的头部。

## jQuery 事件

### jQuery 事件注册

1. **语法**

   `element.事件(function(){})    `

   其他事件和原生基本一致。

### jQuery 事件处理

1. **事件处理 on() 绑定事件**

   1. 语法

      `element.on(events,[selector],fn)    `

   2. **注意**

      1. events:一个或多个用空格分隔的事件类型，如"click"或"keydown" 
      2. selector: 元素的子元素选择器 。
      3. fn:回调函数 即绑定在元素身上的侦听函数。 

   3. **on() 方法优势1：**

      1. 可以绑定多个事件，多个处理事件处理程序。 

         ```javascript
         $(“div”).on({
           mouseover: function(){}, 
           mouseout: function(){},
           click: function(){}	
         });       
         ```

      2. 如果事件处理程序相同 

         ```javascript
         $(“div”).on(“mouseover mouseout”, function() {
            $(this).toggleClass(“current”);
         }); 
         ```

   4. **on()方法优势2：**

      1. 可以事件委派操作 。事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素。

         ```javascript
         $('ul').on('click', 'li', function() {
             alert('hello world!');
         });       
         ```

   5. **on() 方法优势3：**

      1. 动态创建的元素，click() 没有办法绑定事件， on() 可以给动态生成的元素绑定事件 

         ```javascript
         $(“div").on("click",”p”, function(){
              alert("俺可以给动态生成的元素绑定事件")
          });       
         $("div").append($("<p>我是动态创建的p</p>"));
         ```

2. **事件处理 off() 解绑事件**

   1. off() 方法可以移除通过 on() 方法添加的事件处理程序。

      ```javascript
      $("p").off() // 解绑p元素所有事件处理程序
      $("p").off( "click")  // 解绑p元素上面的点击事件 后面的 foo 是侦听函数名
      $("ul").off("click", "li");   // 解绑事件委托
      ```

   2. 如果有的事件只想触发一次， 可以使用 one() 来绑定事件。

      ```javascript
      $("p").one("click", function() {
          alert(11);
      })
      ```

3. **自动触发事件 trigger()** 

   ```JavaScript
   element.click()  // 第一种简写形式
   element.trigger("type") // 第二种自动触发模式
   element.triggerHandler(type)  // 第三种自动触发模式
   //triggerHandler模式不会触发元素的默认行为，这是和前面两种的区别。
   ```

### jQuery 事件对象

1. 事件被触发，就会有事件对象的产生。

   ```JavaScript
   element.on(events,[selector],function(event) {})       
   //阻止默认行为：event.preventDefault()   或者 return  false 
   //阻止冒泡： event.stopPropagation()       
   ```

## jQuery 多库共存

1. **jQuery** **解决方案：**
   1. 把里面的 $ 符号 统一改为 jQuery。 比如 jQuery(''div'')
   2. jQuery 变量规定新的名称：$.noConflict()    var xx = $.noConflict();

​		
