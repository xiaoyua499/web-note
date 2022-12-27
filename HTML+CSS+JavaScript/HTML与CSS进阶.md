[TOC]



# HTML与CSS进阶

## 平面转换

1. **目标**:使用**transform**属性实现元素的**位移,旋转,缩放**等效果

2. **属性:transform**

   1. 位移:**translate**

      ```css
      /*语法  transform:translate(水平移动距离,垂直移动距离);*/
      translate()/*只给一个值,表示X轴方向移动*/
      translateX() translateY()/*单独控制X轴与Y轴*/
      /*绝对定位居中*/
      .son {
          position: absolute;
          left: 50%;
          top: 50%;
          /* margin-left: -100px;
          margin-top: -50px; */
      
          transform: translate(-50%, -50%);
      
          width: 203px;
          height: 100px;
          background-color: pink;
      }
      ```

   2. 旋转:**rotate**

      ```css
      /*语法 transform:rotate(角度)*/
      /*注意:角度单位是deg*/
      
      转换原点
      transform-origin:原点水平位置 原点垂直位置;
      取值:
      方位名词(left,top,right,bottom,center)
      像素单位数值
      百分比(按照盒子自身大小计算)
      ```

   3. **多重转换**

      ```css
      tarnsform复合属性
      transform: translate(600px) rotate(360deg);
      ```

   4. 缩放:**scale**

      `transform:scale(x轴缩放倍数,y轴缩放倍数);`

   5. 渐变背景

      ```css
      background-image: linear-gradient(
      	颜色1,
      	颜色2
      );
      
      transparent  透明
      ```

## 空间转换

1. 目标:使用**transform**属性实现元素在空间内的**位移,旋转,缩放**等效果

2. 属性:**transform**

   1. 位移:**translate3d**

      ```css
      语法: 
      transform:translate3d(x,y,z);
      transform:translateX(值);
      transform:translateY(值);
      transform:translateZ(值);
      ```

   2. 透视:**perspective:值** (**加给父级**)

      1. 取值(透视距离):一般在**800-1200**
      2. 透视距离也称为视距,所谓视距就是人的**眼睛到屏幕的距离**

   3. 旋转:**rotte**

      ```css
      transform:rotateZ(值);
      transform:rotateX(值);
      transform:rotateY(值);
      拓展:rotate3d(x,y,z,角度); :用来自定义旋转轴的位置
      x,y,z取值为0-1
      ```

   4. 立体呈现

      ```css
      transform-style:preserve-3d;(加给父级) 呈现立体图形
      默认值:flat,表示子级处于2d空间
      ```

   5. 缩放:**scale**

      ```css
      tranform:scaleX(倍数);
      tranform:scaley(倍数);
      tranform:scalez(倍数);
      tranform:scale3d(x,y,z);
      ```

## 动画

1. **目标:**使用**animation**添加**动画**效果

2. **动画效果:**实现**多个状态**之间的变化过程,动画过程可控(**重复播放,最终画面,是否暂停**)

   ```css
   1.定义动画
   @keyframes 动画名称 {
       from {}
       to {}
   }
   
   @keyframes 动画名称 {
       0% {}
       10% {}
       15% {}
       100% {}
   }
   
   2.使用动画
   animation: 动画名称 动画花费时长;
   
   复合属性
   animation:动画名称 动画花费时长 速度曲线 延迟时间 重复次数(infinite 无限循环) 动画反向(alternate) 执行完毕时状态(动画停留在结束状态 forwards);
   ```

   | 属性                      |        作用        |                    取值                    |
   | :------------------------ | :----------------: | :----------------------------------------: |
   | animation-name            |      动画名称      |                                            |
   | animation-duration        |      动画时长      |                                            |
   | animation-delay           |      延迟时间      |                                            |
   | animation-fill-mode       | 动画执行完毕时状态 | forwards:最后一帧状态;backwards:第一帧状态 |
   | animation-timing-mode     |      速度曲线      |            steps(数字):逐帧动画            |
   | animation-iteration-count |      重复次数      |             infinite:无限循环              |
   | animation-direction       |    动画执行方向    |              alternate:反方向              |
   | animation-play-state      |      暂停动画      |       paused:暂停,通常配合:hover使用       |

# 移动web

## 移动端特点

1. **分辨率**

   1. 分辨率分类
      - **物理分辨率**是生产屏幕是就固定的,他是不可改变的
      - **逻辑分辨率**是在软件(驱动)决定的的
   2. 视口:meta
   3. 二倍图

2. **百分比布局**

   1. 百分比布局,也叫**流式布局**
   2. 效果:**宽度自适应,高度固定**

3. **Flex布局/弹性布局**

   1. 是一种浏览器提倡的布局模型

   2. 设置方式:父级元素添加 display:flex,子集可以自动的挤压或拉伸

   3. 组成:

      - 父级:弹性容器
      - 子集:弹性盒子
      - 主轴:弹性盒子默认沿主轴排列
      - 侧轴/交叉轴

   4. **justify-content**调节元素在主轴的对齐方式

      | 属性值       |                        作用                         |
      | ------------ | :-------------------------------------------------: |
      | flex-start   |               默认值,起点开始依次排列               |
      | flex-end     |                  终点开始依次排列                   |
      | center       |                   沿主轴居中排列                    |
      | space-around | 弹性盒子沿主轴均匀排列,空白间距均分布在弹性盒子两侧 |
      | space-beween |  弹性盒子沿主轴均匀排列,空白间距均分在相邻盒子之间  |
      | apace-evenly |  弹性盒子沿主轴均匀排列,弹性盒子与容器之间间距相等  |

   5. **anlign-items**调节元素在侧轴的对齐方式

      | 属性值     |                   作用                    |
      | ---------- | :---------------------------------------: |
      | flex-start |          默认值,起点开始依次排列          |
      | flex-end   |             终点开始依次排列              |
      | center     |              沿侧轴居中排列               |
      | stretch    | 默认值,弹性盒子沿着主轴线被拉伸至铺满容器 |

   6. **anlign-self** 控制某一个弹性盒子在侧轴的对称方式

   7. **伸缩比**

      1. 属性:flex:值  只占用父盒子的剩余尺寸

   8. **flex-direction**改变元素排列方向

      | 属性值         |      作用       |
      | -------------- | :-------------: |
      | row            | 行,水平(默认值) |
      | **column**     |   **列,垂直**   |
      | row-reverse    |   行,从右向左   |
      | column-reverse |   列,从下向上   |

   9. flex-wrap实现弹性盒子多行排列效果

      - flex-wrap: nowrap; 默认(不换行)
      - **flex-wrap: wrap;** 换行

   10. **align-content** 调整行对齐方式

       | 属性值       |                        作用                         |
       | ------------ | :-------------------------------------------------: |
       | flex-start   |               默认值,起点开始依次排列               |
       | flex-end     |                  终点开始依次排列                   |
       | center       |                   沿主轴居中排列                    |
       | space-around | 弹性盒子沿主轴均匀排列,空白间距均分布在弹性盒子两侧 |
       | space-beween |  弹性盒子沿主轴均匀排列,空白间距均分在相邻盒子之间  |

   ## 移动适配

4. **rem移动适配**

   1. **rem单位**

      - 相对单位
      - rem单位是相对于HTML标签的字号计算结果
      - 1rem = 1HTML字号(根标签字号)大小

   2. **媒体查询**

      1. **媒体查询**能够**检测视口的宽度**,然后写**差异化**的CSS样式

         ```css
         @media (媒体特性) {
             选择器 {
                 CSS属性
             }
         }
         
         @media (width:320px) {
             html {
                 font-size: 32px;
             }
         }
         
         目前rem布局方案中,将网页等分成10份.HTML标签的字号为视口宽度的1/10
         ```

5. **less(CSS预处理器)语法**

   1. 使用**Less语法**快速编译生成CSS代码

   2. **运算**
      加 减 乘 直接写计算表达式
      除法需要添加小括号或 .

      ```less
       .box {
          width: 100 + 50px;
          height: 5 * 32px;
          
          width: (100 / 4px);
          height: 100 ./ 4px;
      }
      ```

   3. **嵌套**
      快速生成后代选择器

      ```less
      语法:
      .父级选择器 {
          //父级样式
          .子级选择器{
              //子级样式
          }
      }
      
      .father {
          color: red;
          .son {
              width: 100px;
          }
      }
      注意: &不生成后代选择器,表示当前选择器,通常配合伪类或伪元素使用
      ```

   4. **变量**

      ```less
      语法:
      定义变量:@变量名:值;
      使用变量:CSS属性:@变量名;
      ```

   5. **导入**
      1. @import"文件路径"
   6. **导出**
      1. 方法一:配置EasyLess配件,实现所有Less有相同的导出路径
      2. 方法二: 在less文件第一行添加 // out: ./css/common.css
   7. **禁止导出**
      1. 在less文件第一行添加: out:false
   
6. **vw/vh** 解决方案

   1. **vw:** viewport width
      - 1vw = 1/100视口宽度
   2. **vh:** viewport heifht
      - 1vh = 1/100视口高度

## 响应式

1. **媒体查询**

   1. **max-min-width**

      ```css
      开发常用写法
      min-width(从小到大)
      max-width(从大到小)
      @media (媒体特性) {
          选择器{
              样式
          }
      }
      
      /* 视口宽度小于等于768px， 网页背景色是粉色 */
      @media (max-width: 768px) {
          body {
              background-color: pink;
          }
      }
      
      /* 视口宽度大于等于1200px， 网页背景色是skyblue */
      @media (min-width: 1200px) {
          body {
              background-color: skyblue;
          }
      }
      
      
      完整写法
      @media 关键词 媒体条件 and (媒体特性) { CSS代码 }
      关键词: and only not
      媒体条件: screen(屏幕) print(打印预览) speech(阅读器) all(不区分类型)
      ```

   2. **link导入**

      ```css
      <link rel="stylesheet" media="(min-width: 992px)" href="./one.css">
      <link rel="stylesheet" media="(min-width: 1200px)" href="./two.css">
      ```


## BootStrap框架

1. **BootStrap栅格系统**

   1. **BootStrap3**默认将网页分成**12等份**

      |          | 超小屏幕 |  小屏幕  | 中等屏幕 |  大屏幕   |
      | -------- | :------: | :------: | :------: | :-------: |
      | 相应断点 | < 768px  | >= 768px | >= 992px | >= 1200px |
      | 别名     |    xs    |    sm    |    md    |    lg     |
      | 容器宽度 |   100%   |  750px   |  970px   |  1170px   |
      | 类前缀   | col-xs-* | col-sm*  | col-md-* | col-lg-*  |
      | 列数     |    12    |    12    |    12    |    12     |
      | 列间隙   |   30px   |   30px   |   30px   |   30px    |

   2.  **.container** 应用该类名的盒子,默认已被**指定宽度且居中**
   3.  **.container-fluid** 应用该类名的盒子,宽度均为**100%**
   4. 分别用**.row类**名和**.col类**布局定义栅格布局的行和列
      - **container**类自带间距15px
      - **row**类自带间距-15px
   
2. **组件**

   1. BootStrap提供的常见功能,包含了HTML结构和CSS样式
   2. 使用方法
      1. 引入BootStrap样式
      2. 复制结构,修改内容

3.  **Glyphicons 字体图标**

   1. 空标签调用对应类名
      1. glyphicon
      2. 图标类

4. **插件**

   1. BootStrap插件实现常见的交互效果
   2. 使用方法
      1. 引入BootStrap样式
      2. 引入js文件:jQuery.js+BootStrap.min.js

# HTML5与CSS3

## HTML5新特性

1. **HTML5新增的语义标签**

   ```html
   <header>:头部标签
   <nav>:导航标签
   <article>:内容标签
   <setion>:定义文档某个区域
   <aside>:侧边栏标签
   <footer>:尾部标签
   ```

   

2. **HTML5新增的多媒体标签**

   ```html
   音频:<audio>
       语法:<audio src="文件地址" controls="controls"></audio>
   视频:<video>
       语法: <video src="文件地址" controls="controls"></video>
   ```

3. **HTML5新增的input类型**

   | 属性值            |            说明             |
   | ----------------- | :-------------------------: |
   | type="email"      | 限制用户输入必须为Email类型 |
   | type="url"        |  限制用户输入必须为URL类型  |
   | type="date"       | 限制用户输入必须为日期类型  |
   | type="time"       | 限制用户输入必须为时间类型  |
   | type="month"      |  限制用户输入必须为月类型   |
   | type="week"       |  限制用户输入必须为周类型   |
   | **type="number"** | 限制用户输入必须为数字类型  |
   | **type="tel"**    |          手机号码           |
   | **type="search"** |           搜索框            |
   | type="color"      |    生成一个颜色选择表单     |

   **新增表单属性**

   | 属性            | 值        | 说明                                                         |
   | --------------- | --------- | :----------------------------------------------------------- |
   | required        | required  | 表单拥有该属性表示其内容不能为空,必填                        |
   | **placeholder** | 提示文本  | 表单的提示信息,存在默认值将不显示                            |
   | autofocus       | autofocus | 自动聚焦属性,页面加载完成自动聚焦到指定表单                  |
   | autocomplete    | off/on    | 当用户在字段开始键入时,浏览器基于之前键入过得值,应该显示在字段中填写的选项.<br />默认已经打开,如 autocomplete="on",关闭autocomplete="off"<br />需要放在表单内,同时加上name属性,同时成功提交 |
   | **multipe**     | multipe   | 可以多选文件提交                                             |

## CSS3新特性

1. **CSS3新增选择器**

   1. **属性选择器**

      | 选择符        |                 简介                  |
      | ------------- | :-----------------------------------: |
      | E[att]        |        选择具有att属性的E元素         |
      | E[att="val"]  | 选择具有att属性且属性值等于val的E元素 |
      | E[att^="val"] |  匹配具有att属性且值以val开头的E元素  |
      | E[att$="val"] |  匹配具有att属性且值以val结尾的E元素  |
      | E[att*=val]   |   匹配具有att属性且值含有val的E元素   |

   2. **新增结构伪类选择器**

      | 选择符           | 简介                |
      | ---------------- | ------------------- |
      | E:first-of-type  | 指定类型E的第一个   |
      | E:last-of-type   | 指定类型E的最后一个 |
      | E:nth-of-type(n) | 指定类型E的第n个    |

