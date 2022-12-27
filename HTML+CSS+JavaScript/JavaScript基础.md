[TOC]



# JavaScript

1. **JavaScript组成：**

   1. ECMAScript：JavaScript语法
   2. DOM：页面文档对象模型
   3. BOM：浏览器对象模型

2. **JavaScript输入输出语句**

   |       方法       |              说明              |
   | :--------------: | :----------------------------: |
   |   alert（msg）   |        浏览器弹出警示框        |
   | console.log(msg) |    浏览器控制台打印输出信息    |
   |   prompt(info)   | 浏览器弹出输入框，用户可以输入 |


## 变量

1. 声明变量

   1. `var age;`声明一个名称为**age**的变量

   2. var是一个JS关键字，用来声明变量

2. 赋值

   1. `age=18;`

3. 变量的初始化

   1. ```var age = 18 ;```

4. 变量语法的拓展

   1. 更新变量：

      一个变量被重新赋值后，它原有的值就会被覆盖，变量值将以最后一次的值为准。

      ```javascript
      var age = 18;
      age = 81;
      //最后的结果就是81因为18被覆盖掉了
      ```

   2. 同时声明多个变量

      同时声明多个变量时，只需写一个var，多个变量名之间用英文逗号隔开。

      ```javascript
      var age = 10,name = 'zs',sex = 2;
      ```

   3. 声明变量的特殊情况
      1. 只声明不赋值结果显示`undefined`未定义的
      2. 不声明不赋值会报错
      3. 不声明直接赋值可以使用
   
5. 变量命名规范

## 数据类型

1. **数据类型简介**

   1. JavaScript的变量数据类型是只有程序在运行过程中，根据等号右边的值来判断
   2. JavaScript是动态语言，变量的数据类型可以变换

2. **简单数据类型**

   | 简单数据类型 |                     说明                      |  默认值   |
   | :----------: | :-------------------------------------------: | :-------: |
   |    Number    |          数值型，包含整值型和浮点型           |     0     |
   |   Boolean    |      布尔值型，如true、false，等价于1和0      |   false   |
   |    String    |              字符串型，如“张三”               |    “ ”    |
   |  Undefined   | var a；声明了变量a但没有给值，此时a=undefined | undefined |
   |     Null     |         var a=null；声明了变量a为空值         |   null    |

   1. **数值型number**

      1. 数字型进制
         1. 八进制在数字前面加“0”
         2. 十六进制在数字前面加“0x”

      2. 数字型范围

      ```javascript
          在‘
           s <L>:?aC字型特殊值
      ```

   2. **字型特殊值**

      1. 无穷大：Infinity
      2. 无穷小：-Infinity
      3. NaN：非数字
      4. isNaN（）可以判断数据是否为数字型

   1. **字符串型String**

      1. 字符串转义符

         | 转义符 |         解释说明         |
         | :----: | :----------------------: |
         |   \n   | 换行符，n是newline的意思 |
         |  \\\   |          斜杠\           |
         |  \\'   |         ‘ 单引号         |
         |  \\”   |         “ 双引号         |
         |   \t   |         tab 缩进         |
         |   \b   |   空格，b是blank的意思   |

      2. **获取字符串的长度lenght**

      ```javascript
          //获取字符串的长度 length
          var str = 'my name is andy';
          console.log(str.length);//15
      ```

      1. **字符串的拼接 +**

      ```javascript
      cinsole.log('沙漠'+'骆驼')//显示 ’沙漠骆驼‘
      
      数字相加，字符相连
      ```

   2. **布尔型 Boolean**

      1. 布尔类型有两个值：true和false，其中true表示真，而false表示假。
      2. 布尔型和数字型相加的时候，true的值为1，false的值为0

   3. **Undefined和Null**

      1. 一个声明后没有被赋值的变量会有一个默认值undefined
      2. 一个声明变量给null值，里面存的值为空

3. **获取变量的数据类型typeof**

4. **数据类型的转换**

   1. **转换为字符串类型**

      1. toString（ ）

         `变量.toString( )`

      2. String（ ）

         `String(变量)`

      3. **加号（+）拼接字符串**(隐式转换)

         `console.log(num+' ');`

   2. **转换为数字型**
      1. **parseInt(string)**
      2. **parseFloat(string)**
      3. Number() 强制转换函数
      4. js隐式转换（- * /）
      
   3. **转换成布尔型**
   
      1. **Boolean( )**

## 运算符

1. **算数运算符**

2. **递增递减运算符**

   1. 前置递增  **++num**

   2. 前置递减  **--num**

      **先加/减1，后返回值**

   3. 后置递增 **num++**

   4. 后置递减 **num--**

      **先返回原值，后自加/减**

3. **比较运算符**

4. **逻辑运算符**

   1. 与：**$$**

      **短路运算**：

      1. 如果**表达式1**为真则返回**表达式2**

      2. 如果**表达式1**为假则返回**表达式1**

   2. 或：**||**

      **短路运算：**

      1. 如果**表达式1**为真则返回**表达式1**
      2. 如果**表达式1**位假则返回**表达式2**

      ```javascript
      var num = 0;
      console.log(123 || num++); // 123
      console.log(num); // 0
      //逻辑中断会影响程序的运算结果
      ```

   3. 非 ：**！**

5. **赋值运算符**

   1. 直接赋值 **=**
   2. 加减一个数后在赋值 **+=、-=**
   3. 乘、除、取模 后在赋值 ***=、/+、%=**

6. **运算符的优先级**

## 流程控制

1. **顺序流程控制**

2. **分支流程控制**

   1. **if分支语句**

      ```javascript
      if(条件语句){
          //执行语句
      }
      //执行思路：
      //如果if里面的表达式结果为真 则执行大括号里面的 执行语句
      //如果if里面的表达式结果为假 则执行大括号外面的代码
      ```

   2.  **if...else...语句**

      ```javascript
      if(条件语句){
          //[如果]执行语句
      }
      else{
          //[否则]执行语句
      }
      //执行思路：
      //如果条件语句表达式结果为真 则执行大括号里面的执行语句
      //如果条件语句表达式结果为假 则执行else里面的执行语句
      ```

   3. **if...else if 多分支语句**

      ```javascript
      if(条件表达式1){
          //语句1
      }
      else if(条件表达式2){
          //语句2
      }
      else if(条件表达式3){
          //语句3
      }
      else{
          //语句4
      }
      //执行思路：
      //如果条件语句表达式1结果为真 则执行语句1，执行完毕后退出if语句
      //如果条件语句表达式2结果为真 则执行语句2,执行完毕后退出if语句，以此类推
      //所有条件语句都不满足则执行else里面的执行语句
      //注意：多分支语句是多选一，只能执行一个语句
      ```

   4. **三元运算符**

      1. 语法结构：**条件表达式 ？ 表达式1 : 表达式2**
      2. 执行思路：如果表达式结果为**真**，则返回**表达式1的值** ；如果表达式的结果为**假**，则返回**表达式2的值**

   5. **switch语句**

      ```javascript
      switch(表达式){
          case value1:
              //执行语句1;
              break;
          case value2:
              //执行语句2;
              break;
          default:
              //执行语句3;
      }
      //执行思路：
      //利用表达式的值和case里面value值相匹配，如果匹配上，就执行case里面的语句
      //如果没有能与之相匹配的value值，则执行default里面的语句
      //注意：1、表达式里面的值和case里面的value值必须是全等才可以匹配
      //	   2、如果当前的case里面没有back，则不会退出swicth将继续执行下一个case，直到遇见back或default
      ```

3. **循环**

   1. **for循环**

      ```javascript
      for(初始化变量;条件表达式;操作表达式){
          //循环体
      }
      ```

   2. **while循环**

      ```javascript
      while(条件表达式){
          //循环体
      }
      //执行思路：
      //当条件表达式结果为true 则执行循环 否则退出循环
      ```

   3. **do...while循环**

      ```javascript
      do{
          //循环体
      }while(循环条件)
      //与while不同的是 do...while是先执行一次循环后判断是否继续执行循环
      ```

   4. **continue break**
      1. continue：跳出本次循环
      2. break：跳出整个循环

## 数组

1. **创建数组**

   1. **利用 new 创建数组**

      `var arr = new Array( ); //创建一个新数组`

   2. **利用数组字面量**

      ```javascript
      var arr = [ ];//创建一个新的数组
      //数组里面用 , 分隔
      ```

   3. **获取数组里面的元素**

      ```javascript
      //格式：数组名[索引号]
      var arr = [1, 2,'pink老师',true];
      console.log(arr[2]); //pink老师
      ```

   4. **遍历数组**

      ```javascript
      //遍历数组就是把数组从头到尾访问一遍
      //因为数组的索引号是从0开始的，所以i要从0开始
      var arr = ['red','green','blue'];
      for (var i = 0; i < 3; i++) {
          console.log(arr[i]);
      }
      //red
      //green
      //blue
      ```

   5. **数组的长度**

      1. **数组名.length**

         ```javascript
         for (var i = 0; i < arr.length; i++) {
             console.log(arr[i]);
         }
         //1. 数组的长度是元素个数，不要与索引号混淆
         //2. arr.length 是动态监测数组的个数
         ```

   6. **新增数组元素**

      1. **修改length长度**

         ```javascript
         var arr = [1,2,3];
         arr.length = 4;
         console.log(arr);
         //[1,2,3,undefined,undefined]
         //新增的元素没有声明变量，所以默认值为undefined
         ```

      2. **修改索引号 追加数组元素**

         ```javascript
         var arr = [1,2,3];
         arr[3] = pink;
         console.log(arr);
         //[1,2,3,'pink']
         arr[0] = 10;
         console.log(arr[0]);
         // 10
         //不要直接给数组名赋值，否则会替换原来的数组元素
         ```

      ### 冒泡排序

      ```javascript
      var arr = [5, 4, 3, 2, 1];
      for (var i = 0; i <= arr.length - 1; i++) { //外层循环管趟数
          for (var j = 0; j <= arr.length - i - 1; j++) { //里面的循环 每一趟交换次数
              //内部交换2个变量的值 前一个和后一个数组元素相比较
              if (arr[j] > arr[j + 1]) {
                  var temp = arr[i];
                  arr[j] = arr[j + 1];
                  arr[j + 1] = temp;
              }
      	}
      }
      console.log(arr);
      ```

## 函数

1. **函数的使用**

   ```javascript
   //声明函数
   function 函数名 ( ) {
       //函数体
   } 
   //1、function 声明函数的关键字 全部小写
   //2、函数是做某些事情，函数名一般是动词
   //3、函数不调用自己不执行
   //调用函数
   函数名 ( ) ; 
   ```

2. **函数的参数**

   ```javascript
   function 函数名 (形参1,形参2...) {
       
   }
   函数名 (实参1,实参2...);
   //形参：形式上的参数 函数定义的时候 传递的函数 当前不知道是什么
   //实参：实际上的参数 函数调用的时候传递的参数 实参是传递给形参的
   //函数的参数可以有也可以没有
   ```

3. **函数的返回值**

   ```javascript
   function 函数名 () {
       return 需要返回的结果;
   }
   函数名 ();
   //只要函数遇到return 就把后面的结果返回给后面的函数调用者 函数名() = return后面的结果
   //return会终止函数且只能返回一个值
   ```

4. **arguments的使用**
   1. **伪数组** 并不是真正意义上的数组
   2. 具有数组的 **length** 属性
   3. 按照**索引**的方式进行储存
   4. 它没有真正数组的一些方法 **pop( ), push()**等
   
5. **两种函数命名方式**

   ```javascript
   //1.利用函数关键字自定义函数
   function fn() {
       
   }
   fn();
   //2.函数表达式(匿名函数)
   var fun = function() {
       
   }
   fun();
   //fun是变量名 不是函数名
   //函数表达式声明变量跟声明变量差不多,只不过变量里面存的是值而函数表达式里面存的是函数
   ```

## JavaScript的作用域

1. **作用域**

   1. 全局作用域: 整个script标签或者一个单独的文件
   2. 局部作用域(函数作用域): 在函数内部就是局部作用域 这个代码只在函数内部器效果和作用

2. **变量的作用域**

   1. 全局变量:
      1. 在全局作用域下的变量
      2. **注意:**如果在函数内部没有声明直接赋值的变量也属于全局变量
   2. 局部变量:
      1. 在局部作用域下的变量
      2. **注意:**函数的形参也可以看做局部变量

3. **作用域链**

   内部函数访问外部函数的变量,采取的是链式查找的方式来决定去那个值,这种结构我们称为作用域链  (就近原则)

## JavaScript预解析

1. **预解析**

   1. js引擎运行js分为两步:

      1. 预解析:js引擎会把所有的**var**和**function**提升到当前作用域的最前面

         **变量提升:**把所有的**变量声明**提升到当前作用域的最前面 **不提升赋值操作**

         **函数提升:**把所有的**函数声明**提升到当前作用域的最前面 **不调用函数**

      2. 代码执行:按照代码书写顺序从上到下执行

      ```javascript
      var num = 10;
      function fn() {
          console.log(num);
          var num = 20;
          console.log(num);
      }
      fn();
      //相当于进行了一下操作
      var num;
      function fn() {
          var num;
          console.log(num);
          num = 20;
          console.log(num);
      }
      num = 10;
      fn();
      //undefined
      //20
      ```

## 对象

​	在JavaScript中,对象是一组无序的相关属性,所有的事物都是对象,例如:字符串 数值 数组 函数等

1. 对象是由**属性**和**方法**组成的

   - 属性:事物的特征
   - 方法:事物的行为

2. 创建对象

   1. 利用对象字面量创建对象 {}

      ```javascript
      var obj = {
          uname:'张三丰',
          age:18,
          sex:'男',
          sayHi:function() {
              console.log('Hi~~');
          }
      }
      //(1) 里面的属性值或者方法采取键值对的形式 键(属性名):值(属性值)
      //(2) 多个属性或者方法中间用逗号隔开
      //(3) 方法冒号后面的是一个匿名函数
      //使用对象
      //(1) 调用对象的属性采取 对象名.属性名
      console.log(obj.uname);
      //对象名['属性名']
      console.log(obj['age']);
      //调用对象的方法 对象名.方法名()
      console.log(obj.sayHi());
      ```

   2. 利用 **new Object** 创建对象

      ```javascript
      var obj = new Object();
      obj.uname = '张三丰';
      obj.age = 18;
      obj.sex = '男';
      obj.sayHi = function(){
          console.log('Hi~');
      }
      // 1.利用 = 赋值的方法 添加对象的属性和方法
      // 2.每个属性和方法之间用分号结束
      ```

   3. **构造函数**

      ```javascript
      //语法格式
      function 构造函数名(){
          this.属性 = 值;
          this.方法 = funcion() {}
      }
      new 构造函数名();
      //1.构造函数首字母大写
      //2.构造函数不需要return
      //3.用构造函数必须用new
      //构造函数抽象了函数的公共部分,封装到了函数里面,它泛指某一大类
      //创建对象特指某一个,通过new关键字创建对象的过程也称为对象实例化
      function Star(uname, age, sex) {
          this.name = uname;
          this.age = age;
          this.sex = sex;
      }
      var ldh = new Star('刘德华', 18, '男');
      ```

   4. **new关键字**
      1. new关键字的执行过程
         1. **new** 构造函数在内存中创建一个空对象
         2. **this** 就会指向刚才创建的空对象
         3. 执行构造函数里面的代码 给这个空对象添加**属性**和**方法**
         4. **返回**这个对象

   5. **遍历对象**

      ```javascript
      //for...in 遍历对象
      for(变量 in 对象){
          
      }
      for (var k in obj){
          console.log(k); // k(变量) 得到的是 属性名
          console.log(obj[k]); //obj[k] 得到的是 属性值
      }
      ```

## 内置对象

内置对象:js语言自带的一些对象,这些对象供开发者使用,并提供了一些常用的或基本而必要的功能(属性和方法)

1. 查文档:**MDN**

2. Math数学对象

   1. **Math.PI** 圆周率

   2. **Math.max( )/Math.min** 求最大值/最小值

      ```javascript
      //最大值
      console.log(Math.max(1,99,3)); //99
      console.log(Math.max(1,5,8)); //8
      //最小值
      console.log(Math.max(1,99,3)); //1
      console.log(Math.max(2,5,8)); //2
      //如果没有参数，则结果为 - Infinity
      //如果有任一参数不能被转换为数值，则结果为 NaN
      ```

   3. **Math.abs** 绝对值

   4. **三个取整方法**

      ```javascript
      //Math.floor() 向下取整
      console.log(Math.floor(1.1)); //1
      console.log(Math.floor(1.9)); //1
      //Math.ceil() 向上取整
      console.log(Math.ceil(1.1)); //2
      console.log(Math.ceil(1.9)); //2
      //Math.round() 四舍五入
      console.log(Math.round(1.1));//1
      console.log(Math.round(1.9));//2
      console.log(Math.round(-1.1));//-1
      console.log(Math.round(1.5));//-1
      ```

   5. **Math.rendom()**随机数方法

      ```javascript
      //两个数之间去随机整数
      function getRandom(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min; //含最大值，含最小值 
      }
      var arr = ['张三', '李四','李思思', '迪丽热巴', '刘元松']
      console.log(arr[getRandom(0, 4)]);
      ```

3. **Date( )** 日期对象

    1. **Date( )** 是一个构造函数 必须用**new**

       ```javascript
       var date = new Date();
       console.log(date);
       //1.使用Date 如果没有参数 返回当前系统的时间
       //2.参数常用写法: 数字型 2019, 10, 01 或者是 字符串型 '2019-10-1 8:8:8'
       var date = new Date(2019, 10, 01);
       console.log(date);// 返回 11月 不是 10月
       var date = new Date('2019-10-1 8:8:8');
       console.log(date);//Oct 01 2019 08:08:08
       ```

   2. **日期格式化**

      ```javascript
      var date = new Date();
      console.log(date);
      console.log(date.getFullYear());//返回当前日期年份
      console.log(date.getMonth() + 1);//返回的月份比当前月份小一个月
      console.log(date.getDate());//返回日期
      console.log(date.getDay());//周日返回 0
      
      var year = date.getFullYear();
      var month = date.getMonth() + 1;
      var dates = date.getDate();
      var day = date.getDay();
      var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
      console.log('今天是:' + year + '年' + month + '月' + dates + '日' + arr[day]);
      //今天是:2022年3月6日星期日
      
      //获得Date总的毫秒数(时间戳)  不是当前时间的毫秒数 而是距离1970年1月1日的中毫秒数
      //1.通过 valueOf() getTime()
      var date = new Date();
      console.log(date.valueOf());
      console.log(date.getTime());
      //2.简单的写法
      var date = +new Date();//+new Date() 返回的是总毫秒数
      console.log(date);
      //3. H5 新增的 获得总毫秒数
      console.log(Date.now());
      ```

4. **数组对象**

   1. **检测是否为数组**

      ```javascript
      //1. instanceof 运算符 它可以用来检测是否为数组
      var arr = [];
      console.log(arr instanceof Array); //true
      //2. Array.isArray(参数);
      console.log(Array.isArrsy(arr));
      ```

   2. **添加删除数组元素**

      ```javascript
      //1. push() 在数组的末尾 添加一个或者多个元素
      var arr = [1, 2, 3];
      arr.push(4, 'pink');
      //(1) push 是可以给数组追加新元素
      //(2) push() 参数直接写数组元素就可以了
      //(3) push完毕后,返回的结果是 新数组的长度
      //(4) 原数组也会发生变化
      //2. unshift 在数组的开头添加一个说多个元素
      arr.unshift(4, 'pink');
      //3. pop() 删除数组的最后一个元素
      arr.pop();
      //返回值为被删除元素
      //4. shift 删除数组中第一个元素
      arr.shitf();
      ```

   3. **数组排序**

      ```javascript
      //1. reverse 翻转数组
      var arr = [1, 2, 3];
      arr.reverse();
      //2. sort 数组排序(冒泡排序)
      arr.sort();//无法进行两位数以上的排序
      //解决方法
      arr.sort(function(a, b){
          return a - b; //升序排序
          return b - a; //降序排序
      }); 
      ```

   4. **数组索引方法**

      ```javascript
      //indexOf 返回数组元素索引号
      //只返回第一个满足条件的索引号
      //如果数组里面找不到元素,则返回-1
      var arr = ['red', 'green', 'blue', 'pink'];
      arr.indexOf('blue')
      //lastindexOf 从后面开始查找
      ```

   5. **数组转换为字符串**

      ```javascript
      //1. toString() 将数组转换为字符串
      var arr = [1, 2, 3];
      console.log(arr.toString()); // 1,2,3
      //2. join(分隔符)
      var arr = ['green', 'blue', 'pink'];
      console.log(arr.join()); // green,blue,pink
      console.log(arr.join('-')); // green-blue-pink
      ```

5. **字符串对象**

   ```javascript
   //基本包装类型:就是把简单数据类型包装成复杂数据类型,这样基本数据类型就有了属性和方法
   var str = 'andy';
   console.log(str.length);
   ```

   1. **根据字符返回位置**

      ```javascript
      // 根据字符串返回位置 str.indexOf('要查找的字符', [起始的位置])
      var str = '改革春风吹满地,春天来了';
      console.log(str.indexOf('春'));
      console.log(str.indexOf('春', 3)); // 从索引号是3的位置开始查
      //lastindexOf 从后面开始查找
      ```

   2. **根据位置返回字符**

      ```javascript
      //1. charAt(index) 根据位置返回字符
      var str = 'andy';
      console.log(str.charAt(3));
      //遍历所有字符
      fou (var i = 0; i < str.length; i++) {
          console.log(str.charAt(i));
      }
      //2. charCodeAt(index) 返回相应的ASVII值 目的: 判断用户按下了那个键
      console.log(str.charCodeAt(0)); // 97
      //3. str[undex] H5新增的
      console.log(str[0]); // a
      ```

   3. **字符串的操作方法**

      ```javascript
      //1. concat('字符串1', '字符串2'....)
      var str = 'andy';
      console.log(str.concat('red')); // 'andyred'
      //2. substr('截取的起始位置', '截取几个字符');
      var str = '改革春风吹满地';
      console.log(str.substr(2, 2)); // '春风'
      //3. replace('被替换的字符', '替换的字符')
      var str = 'andyandy';
      console.log(str.replace('a', 'b'));// 'bndyandy'
      //只会替换第一出现的字符
      //4. 字符转换为数组 split('分隔符')
      var str = 'red', 'pink', 'blue';
      console.log(str.split(',')); // ['red', 'pink', 'blue']
      ```

## 简单数据类型和复杂数据类型

1. 简单数据类型又叫基本数据类型或者**值类型**,复杂类型又叫做**引用类型**
   - 值类型:简单数据类型/基本数据类型,在储存时变量中储存的是值本身,因此叫做值类型 string,number,boolean,null
   - 引用数据类型:复杂数据类型,在储存时变量中存储的仅仅是地址(引用),因此叫做引用数据类型通过**new关键字**创建的对象(系统对象,自定义对象),如 Object,Array,Date等
2. **堆和栈**
   1. 简单数据类型:存放在栈里面,里面直接开辟一个空间存放值
   2. 复杂数据类型:首先在栈里面存放地址 (十六进制表示) 然后这个地址指向堆里面的数据
3. **简单数据类型传参**
4. **复杂数据类型传参**

​	









