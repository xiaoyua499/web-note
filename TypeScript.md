# TypeScript

## 一、TypeScript介绍

### 1.1 什么是TypeScript

> 在引入编程社区 20 多年后，JavaScript 现在已成为有史以来应用最广泛的跨平台语言之一。JavaScript 最初是一种用于向网页添加微不足道的交互性的小型脚本语言，现已发展成为各种规模的前端和后端应 用程序的首选语言。虽然用 JavaScript 编写的程序的大小、范围和复杂性呈指数级增长，但 JavaScript 语言表达不同代码单元之间关系的能力却没有。结合 JavaScript 相当奇特的运行时语义，语言和程序复 杂性之间的这种不匹配使得 JavaScript 开发成为一项难以大规模管理的任务.

> 程序员编写的最常见的错误类型可以描述为类型错误：在预期不同类型的值的地方使用了某种类型的 值。这可能是由于简单的拼写错误、无法理解库的 API 表面、对运行时行为的错误假设或其他错误。 TypeScript 的目标是成为 JavaScript 程序的静态类型检查器——换句话说，是一个在代码运行之前运行 的工具（静态）并确保程序的类型正确（类型检查）。

> TypeScript 是一种由微软开发的自由和开源的编程语言。它是 JavaScript 的一个超集，而且本质上向这 个语言添加了可选的静态类型和基于类的面向对象编程。

> TypeScript 是一种非常受欢迎的 JavaScript 语言扩展。它在现有的 JavaScript 语法之上加入了一层类型 层，而这一层即使被删除，也丝毫不会影响运行时的原有表现。许多人认为 TypeScript "只是一个编译 器"，但更好的理解其实是把 TypeScript 看作两个独立的系统：编译器（即处理语法的部分）和语言工 具（即处理与编辑器集成的部分）。通过独立看待这两个系统，就可以得到能够解释我们之前所做决策 的两个重要视角。

> 在 npm[3] 上，TypeScript 的下载量每年都在翻倍。截止2021 年 12 月 1 日，它的每周下载量超过为 2200 万次。而在去年 12 月，这一数字约为 1200 万次。它仍保持着高速增长的趋势，没有任何放缓的 迹象。

> 从 2.0 版本开始，TypeScript 每两月定期发布一个 release。但是现在放缓了发布的节奏，改为每三个 月发布一次。其中会花一个月编写新 features 并发布 beta 版本，剩下两个月对 beta 版进行测试和 bug 修复，这使得后续的发布更加稳定.

### 1.2 JS,ES,TS的关系

- 1995年：JavaScript
  - 当时的网景公司正凭借其Navigator浏览器成为Web时代开启时最著名的第一代互联网公司
  - 由于网景公司希望能在静态HTML页面上添加一些动态效果，于是 Brendan Eich 在两周之内设计出了 JavaScript语言。
  - 为什么起名叫JavaScript？原因是当时Java语言非常红火，所以网景公司希望借Java的名气来推广，但事 实上JavaScript除了语法上有点像Java，其他部分基本上没啥关系.
- 1997年：ECMAScript
  - 因为网景开发了JavaScript，一年后微软又模仿JavaScript开发了JScript，为了让JavaScript成为全球标 准，几个公司联合ECMA（European Computer Manufacturers Association）（欧洲计算机制造商协 会）组织制定了JavaScript 语言的标准，被称为ECMAScript标准.
- 2015年：TypeScript
  - TypeScript 是 JavaScript 的超集，即包含JavaScript 的所有元素，能运行JavaScript 的代码，并扩展了 JavaScript 的语法。相比于JavaScript ，它还增加了静态类型、类、模块、接口和类型注解方面的功能， 更易于大项目的开发。
  - TypeScript 提供最新的和不断发展的 JavaScript 特性，包括那些来自 2015 年的 ECMAScript 和未来的 提案中的特性，比如异步功能和 Decorators，以帮助建立健壮的组件。下图显示了 TypeScript 与 ES5、ES2015+ 之间的关系：
  - <img src="C:\Users\30287\Downloads\uTools_1665406404455.png" style="zoom:50%;" />

### 1.3 TypeScript与JavaScript的区别

| TypeScript                                     | JavaScript                                 |
| ---------------------------------------------- | ------------------------------------------ |
| JavaScript 的超集用于解决大型项目的代码复杂性  | 一种脚本语言，用于创建动态网页             |
| 可以在编译期间发现并纠正错误                   | 作为一种解释型语言，只能在运行时发现错误   |
| 强类型，支持静态和动态类型                     | 弱类型，没有静态类型选项                   |
| 最终被编译成 JavaScript 代码，使浏览器可以理解 | 可以直接在浏览器中使用                     |
| 支持模块、泛型和接口                           | 不支持模块、泛型或接口                     |
| 支持 ES3，ES4，ES5 和 ES6+功能                 | 不支持编译其他 ES3，ES4，ES5 或 ES6+功能   |
| 社区的支持仍在增长，而且还不是很大             | 大量的社区支持以及大量文档和解决问题的支持 |

## 二、TypeScript入门

### 2.1 发现问题

JavaScript 中的每个值都有一组行为，您可以通过运行不同的操作来观察。这听起来很抽象，我们来举 一个简单的例子，考虑我们可能对名为 message 的变量运行的一些操作：

```js
// 在 'message' 上访问属性 'toLowerCase'，并调用它
message.toLowerCase();
// 调用 'message'
message();
```

如果我们分解它，第一行可运行的代码访问一个属性 toLowerCase ，然后调用它。第二个尝试 message 直接调用。

但是假设我们不知道 message 。这很常见——我们无法可靠地说出尝试运行任何这些代码会得到什么结 果。每个操作的行为完全取决于我们最初给 message 的赋值。

- 可以调用 message 吗？ 
- 它有 toLowerCase 这个属性吗？ 
- 如果能， toLowerCase 可以调用吗？ 
- 如果这两个值都是可调用的，它们返回什么？

这些问题的答案通常是我们在编写 JavaScript 时牢记在心的东西，我们必须希望所有细节都正确。 假设 message 按以下方式定义:

```js
const message = "Hello World!";
```

正如您可能猜到的，如果我们尝试运行 message.toLowerCase() ，我们只会得到相同的小写字符串。 那第二行代码呢？如果您熟悉 JavaScript，您就会知道这会失败并出现异常：

```js
TypeError: message is not a function
```

如果我们能避免这样的错误，那就太好了.

当我们运行我们的代码时，我们的 JavaScript 运行时选择做什么的方式是通过确定值的类型——它具有 什么样的行为和功能。这 TypeError 就是暗指的一部分- 它说字符串 "Hello World!" 不能作为函数调 用。

对于某些值，例如基本类型 string 和 number ，我们可以在运行时使用 typeof 运算符识别它们的类 型。但是对于函数之类的其他东西，没有相应的运行时机制来识别它们的类型。例如，考虑这个函数：

```tsx
function fn(x) {
	return x.flip();
}
```

我们可以通过阅读代码观察到这个函数只有在给定一个具有可调用 flip 属性的对象时才能工作，但是 JavaScript 并没有以我们可以在代码运行时检查的方式来显示这些信息。在纯 JavaScript 中，告诉 fn 特 定值做什么的唯一方法是调用它并查看会发生什么。这种行为使得在运行之前很难预测代码会做什么， 这意味着在编写代码时更难知道代码会做什么.

这样看来，类型是描述可以传递给 fn 哪些值会崩溃的概念。JavaScript 只真正提供动态类型——运行代 码看看会发生什么。

另一种方法是使用静态类型系统在运行之前预测预期的代码.

### 2.2 静态类型检查

回想一下 `TypeError `我们之前尝试将 `string `作为函数调用的情况。 大多数人不喜欢在运行他们的代码 时出现任何类型的错误 - 这些被认为是错误！当我们编写新代码时，我们会尽量避免引入新的错误.

理想情况下，我们可以有一个工具来帮助我们在代码运行之前发现这些错误。这就是像 TypeScript 这样 的静态类型检查器所做的。 静态类型系统描述了当我们运行程序时我们的值的形状和行为。像 TypeScript 这样的类型检查器，告诉我们什么时候事情可能会出轨。

<img src="https://fastly.jsdelivr.net/gh/xiaoyua499/imageBox@main/1665407027948uTools_1665406935762.png" style="zoom:80%;" />

在我们运行代码之前，使用 TypeScript 运行最后一个示例会给我们一条错误消息。

### 2.3 非异常故障

到目前为止，我们一直在讨论运行时错误——JavaScript 运行时告诉我们它认为某些东西是无意义的情 况。出现这些情况是因为ECMAScript 规范明确说明了语言在遇到意外情况时应该如何表现。

例如，规范说尝试调用不可调用的东西应该抛出错误。也许这听起来像是“明显的行为”，但您可以想象 访问对象上不存在的属性也应该抛出错误。相反，JavaScript 给了我们不同的行为并返回值 `undefined `：

```tsx
const user = {
	name: "小千",
	age: 26,
};
user.location; // 返回 undefined
```

最终，静态类型系统要求必须调用哪些代码，应该在其系统中标记，即使它是不会立即抛出错误的“有 效”JavaScript。比如：在 TypeScript 中，以下代码会产生关于 location 未定义的错误：









