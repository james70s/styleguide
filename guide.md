前端规范
==========

背景
----------
规范是一面镜子.

<a name="HTML"></a>
HTML:
----------

**语言规范**

1. doctype 声明使用 html5:

		<!doctype html>

2. 标签以及属性名使用小写;

3. 对于以下 html 标签可以不结尾:

		<img>, <col>, <base>, <link>, <meta>
 
4. 标签自定义属性使用 data-name="value" 的形式来写, 如果自定义属性特别多, 可以考虑使用标准 json 的方式去写: data-json='{"a":"a", "b":"b"}'; ( 注: 不要使用诸如 a:a, b:b 这种方式来写, 因为对于 boolean 或者 数组, 对象来说, 很难去解析, 所以, 这里以标准的 json 方式来说写, 避免解析纠纷 ) ( [Why?][w3-custom-data] ) 

		data-json="a:1, b:true, c:[1, 2]" , 对于这样的写法, 在解析的时候很难搞清楚 value 值的类型
		data-json='"a":1, "b":true, "c":[1, 2]' -- 正确的写法

5. 对于 JS 钩子, 以 J_CamelCase 的驼峰形式来命名;

6. 对于普通 class 或者 id 命名, 统一使用小写字母, 第一个字符必须为字母, 连接符用中划线 '-', 例如: 

		class="sns-box"
		class="box"

8. css 引用置于头部 `<head>` 标签内;

9. js 引用置于底部 `</body>` 标签前;

10. 非特殊的页面的页面文件编码都使用 gbk 编码, meta 标签 charset 设置为 gbk;

11. 常用的一个页面的 html 结构参考;
        
        <!doctype html>
        <html>
        <head>
            <meta charset="gbk" />
            <title>标题</title>
            <link href="style.css" type="text/css" rel="stylesheet" />
            <script src="some_core_script.js"></script>
        </head>
        <body>
            <div id="page">
                <div id="header">
                ...
                </div>
                <div id="content">
                ...
                </div>
                <div id="footer">
                ...
                </div>
            </div>
            <script src="script.js"></script>
        </body>
        </html>


**标签使用**

1. `<base>` 标签必须放在 `<head>` 内 (注: 否则在某些浏览器下可能会失效);

2. <del>每个页面最多使用一个 `<h1>` 标签;</del> [HTML5 section element][section].

3. `<strong>` 标签用于强调重要性, `<em>` 标签用于表示内容的着重点;( [Why?][strong&em] )

5. 当 link 元素用于引用CSS文档时, 默认 media 是 screen, 如为特殊终端提供样式, 请指定 media 属性, 如 media=“print”;

6. `<img>` 标签要加上 alt 属性(对于使用屏幕阅读者来说, alt 很重要, 它是图片的替代文字, 如果没有设置 alt, 那么阅读器将会读取图片文件名, 因此, 为每一个图片添加 alt 属性是非常重要的, 即使它为空或者 null);

8. `<a>` 链接的 href 属性一般要加上具体的链接, 不要使用空链接 # 和 javascript:void(0);

9. 对于表单控件对应的文本必须使用 `<label>` 元素标记, 且使用 for 属性指向该控件 id;
    
        <label for="username"><input type="text" name="username" id="username" value=""/></label>

**标签嵌套规范**

1. 块元素可以包含内联元素或某些块元素, 但内联元素却不能包含块元素, 它只能包含其它的内联元素;

		<div><h1></h1><p></p></div> --- 对
		<a href="#"><span></span></a> --- 对
		<span><div></div></span> --- 错

2. 块级元素不能放在 `<p>` 里面;

		<p><ol><li></li></ol></p> --- 错
		<p><div></div></p> --- 错

3. 有几个特殊的块级元素只能包含内嵌元素, 不能再包含块级元素, 这几个特殊的标签是;

		h1, h2, h3, h4, h5, h6, p, dt

5. 块级元素与块级元素并列, 内嵌元素与内嵌元素并列;

		<div><h2></h2><p></p></div> --- 对
		<div><a href="#"></a><span></span></div> --- 对
		<div><h2></h2><span></span></div> --- 错

6. [嵌套规则图][inline-rule]:

   ![嵌套规则图](http://www.junchenwu.com/upload/allowednesting.gif)


**注释规范**

1. 对每一个 html 模块, 使用注释包裹, 并加上模块标识: 

		<!-- tsearch begin -->
		<div id="tsearch">
			<form method="post" action="#">
				<!-- ... -->
			</form>
		</div>
		<!-- tsearch end -->

   对于特意需要留有空行 / 空格, 或特意不需要的地方, 使用注释明确指出

2. 修改别人代码时, 加入修改信息. 至少加入修改者大名和修改时间: 

		<!--@author fahai-->
		<!--@last-modified 2010-12-15 13:21-->


3. ie 条件注释:

   IE 5 以上版本识别:

		<!--[if IE]>
		<![endif]-->

   仅某一版本 IE 可以识别:

		<!--[if IE 6]>
		<![endif]-->

		<!--[if IE 7]>
		<![endif]-->

		<!--[if IE 8]>
		<![endif]-->

   低于某一版本 IE 可以识别:

		<!--[if lt IE 7]>
		<![endif]-->

   低于或等于某一版本 IE 可以识别:

		<!--[if lte IE 7]>
		<![endif]-->

   高于某一版本 IE 可以识别:

		<!--[if gt IE 7]>
		<![endif]-->

   高于或等于某一版本 IE 可以识别:

		<!--[if gte IE 7]>
		<![endif]-->

   非 IE 可以识别(不建议使用):

		<!--[if !IE]>
		<!--<![endif]-->

**其他注意事项**

1. 非发布日, 因紧急需求加入页面的 style 和 script, 应加入注释，并在下一次发布时加到对应的 css 文件或是 js 文件里面, 如果所修改的样式生命周期不长则灵活应对;


<a name="CSS"></a>
CSS:
----------

**语言规范**

1. 样式文件中不要出现大写的标签定义, 不要对 JS 钩子进行样式定义; 

2. 避免出现 .a.b 之类的定义, 如果做 hack 使用请注明; ( ie6 不支持此定义 )

3. 稀奇古怪的 hack 请加注释; 

4. 避免使用 !important , 如果必须请加注释; 

5. 缩进以4个空格为单位; 

6. 每条规则为一行, 左大括号跟最后一条, 空一格, 例: 

		.box,
		.content .box {
			color:red;
			font-size:12px;
		}

7. 样式使用竖排, 不要使用横排以及 n 级缩进等;

8. 对于使用 position:relative; 的样式, 请注明使用原因; ( 此样式在 ie6 下经常出现各种问题, 请尽量避免使用 )

9. 对于所有 hack 请放到每个样式定义的最后边;

10. class selector 层级尽量控制在 5 层以内;

**属性使用**

1. border: 以 width, style, color 的顺序书写, width 单位使用 px, 例如:

		border: 1px solid #000;
		border-top: 1px solide #000;
		border-top-color: red;
		border: 0;

   ( 注: 请避免使用 border:none 代替 border:0 [Why?][css-border])

2. background: 以 color, image, repeat, position 的顺序来书写, url 省略引号, 例如:

		background:#003 url(http://www.taobao.com/loading.png) no-repeat 0 0;
		background-color:red;

3. 在使用 CSS expression 时一定要检测性能, 尽量避免使用;

4. CSS属性书写顺序参考
        
        /*
         * display
         * float
         * position
         * z-index
         * width
         * height
         * overflow
         * left(right)
         * top(bottom)
         * text-xxx
         * font-xxx
         * color
         * border
         * background
         * cursor
         */

5. 为了节省图片的开销，有时候小三角形可以用css border来生成, 看看本规范里面小三角按钮，更要看看[乔花的分享](http://ued.taobao.com/blog/2010/08/04/css-border使用小分享/)

**注释规范**

1. 文件头注释:

		/**
		 * Style for module header.
		 * @author fahai
		 * @version 1.0.0 build 2010-12-8
		 * @modified shiran 2011-2-18
		 */

2. 对应于 html 模块, 每一个模块使用注释包裹, 并加上模块标识: 

		/* top-banner { */
		.top-header .top-banner {
			width: 100%;
			height: 40px;
		}


		.top-header .top-banner img {
			vertical-align: middle;
		}
		/* } */

3. 神奇代码和鬼才 hack 添加注释: 

		background-color: transparent; /* flexible background gradient */
		font-family: serif; /* text floating bug in ie6 */

4. 修改别人的 CSS 请添加注释
        
        /* modified by qiaofu 2011-03-03 */


**其他注意事项**

1. 对页面的某一块区域修改的需求时, 当涉及到样式和结构都更改的时候, 要 **注意结构（HTML）的代码和样式（CSS）的代码发布的顺序**, 避免出现结构先上线, 样式后上线导致页面样式出现问题.

2. CSS 中的图片地址在上线前都要替换为线上地址.


<a name="JavaScript"></a>
JavaScript:
----------

**基本格式**

1. 缩进以 4 个空格为基本单位;

2. 三元操作符不要涉及大段的复杂的代码, 如果可以请改为 if else; 

3. 空格

    需要前后加空格的运算符包括: 

		 =, ==, ===, !=, !==, >, <, <=, >= , ? :, -, +, +=, -=, /, *, %, &&, &, ||, |, {}

	不需要出现空格的包括: 

		;, ., (), []

	后边带空格的包括: 

		,, if, for, while, do, catch, with, new, 非三元表达式中的:

	例如: 

		a += 2 ;
		b = true ? a : 1;

    括号中的参数之间加空格

    例如: 
    
        get(x, b, c);

        function get(a, b, c) {
            //work with a,b,c    
        }


4. 每段函数或者逻辑之间空行; 

5. 奇淫技巧必须注释; 

6. 避免使用全局变量, 如果不能避免则尽量减少数量; 

7. 将每条语句放置在一个单独的代码行中保持可读性, 不要出现 aNum++; anOtherNum++;在同一行, var 也一样; 

8. 一定要记住写分号; 

**命名规范**

通常, 使用 functionNamesLikeThis, variableNamesLikeThis, ClassNamesLikeThis, EnumNamesLikeThis, methodNamesLikeThis, 和 SYMBOLIC_CONSTANTS_LIKE_THIS.

1. 属性和方法

	* 文件或类中的 私有 属性, 变量和方法名应该以下划线 "_" 开头. 
	* 保护属性, 变量和方法名不需要下划线开头, 和公共变量名一样.
	* 方法名按描述过程或描述项的方式, 动名词结合. 来命名, 以小写字母开头, 连接词使用混合大小写的驼峰形式, 例如: getAncestorByTagName.

2. 方法和函数参数 

   可选参数以 opt_ 开头.

   函数的参数个数不固定时, 应该添加最后一个参数 var_args 为参数的个数. 你也可以不设置 var_args而取代使用 arguments.

   可选和可变参数应该在 @param 标记中说明清楚. 虽然这两个规定对编译器没有任何影响, 但还是请尽量遵守

3. Getters 和 Setters 

   Getters 和 setters 并不是必要的. 但只要使用它们了, 就请将 getters 命名成 getFoo() 形式, 将 setters 命名成 setFoo(value) 形式. (对于布尔类型的 getters, 使用 isFoo() 也可.)

4. 命名空间 

   JavaScript 不支持包和命名空间. 

   不容易发现和调试全局命名的冲突, 多个系统集成时还可能因为命名冲突导致很严重的问题. 为了提高 JavaScript 代码复用率, 我们遵循下面的约定以避免冲突. 

   为全局代码使用命名空间 

5. 在全局作用域上, 使用一个唯一的, 与工程/库相关的名字作为前缀标识. 比如, 你的工程是 "Project Sloth", 那么命名空间前缀可取为 sloth.*. 

			var sloth = {};

			sloth.sleep = function() {
			  ...
			};

   许多 JavaScript 库, 包括 [the Closure Library][Closure Library] and [Dojo toolkit][Dojo] 为你提供了声明你自己的命名空间的函数. 比如: 

        goog.provide('sloth');

		sloth.sleep = function() {
		  ...
		};

6. 明确命名空间所有权 

   当选择了一个子命名空间, 请确保父命名空间的负责人知道你在用哪个子命名空间, 比如说, 你为工程 'sloths' 创建一个 'hats' 子命名空间, 那确保 sloths 团队人员知道你在使用 sloths.hats.

7. 外部代码和内部代码使用不同的命名空间 

   "外部代码" 是指来自于你代码体系的外部, 可以独立编译. 内外部命名应该严格保持独立. 如果你使用的外部库的所有对象都在 foo.hats.* 下, 那么你自己的代码不能在foo.hats.*下命名, 因为一旦外部库做了修改就有可能会影响到你的代码. 所以永远 **不要修改不属于你管理范畴的对象**

		foo.require('foo.hats');

		/**
		 * WRONG -- Do NOT do this.
		 * @constructor
		 * @extend {foo.hats.RoundHat}
		 */
		foo.hats.BowlerHat = function() {
		};

   如果你需要在外部命名空间中定义新的 API, 那么你应该直接导出一份外部库, 然后在这份代码中修改. 在你的内部代码中, 应该通过他们的内部名字来调用内部 API , 这样保持一致性可让编译器更好的优化你的代码.

		foo.provide('googleyhats.BowlerHat');

		foo.require('foo.hats');

		/**
		 * @constructor
		 * @extend {foo.hats.RoundHat}
		 */
		googleyhats.BowlerHat = function() {
		  ...
		};

		goog.exportSymbol('foo.hats.BowlerHat', googleyhats.BowlerHat);

8. 重命名那些名字很长的变量, 提高可读性, 同时通过局部变量来访问可以在一定程度提升性能

   主要是为了提高可读性. 局部空间中的变量别名只需要取原名字的最后部分.

		/**
		 * @constructor
		 */
		some.long.namespace.MyClass = function() {
		};

		/**
		 * @param {some.long.namespace.MyClass} a
		 */
		some.long.namespace.MyClass.staticHelper = function(a) {
		  ...
		};

		myapp.main = function() {
		  var MyClass = some.long.namespace.MyClass;
		  var staticHelper = some.long.namespace.MyClass.staticHelper;
		  staticHelper(new MyClass());
		};

   不要对命名空间创建别名.

		myapp.main = function() {
		  var namespace = some.long.namespace;
		  namespace.MyClass.staticHelper(new namespace.MyClass());
		};

   除非是枚举类型, 不然不要访问别名变量的属性.

		/** @enum {string} */
		some.long.namespace.Fruit = {
		  APPLE: 'a',
		  BANANA: 'b'
		};

		myapp.main = function() {
		  var Fruit = some.long.namespace.Fruit;
		  switch (fruit) {
			case Fruit.APPLE:
			  ...
			case Fruit.BANANA:
			  ...
		  }
		};
		myapp.main = function() {
		  var MyClass = some.long.namespace.MyClass;
		  MyClass.staticHelper(null);
		};

   不要在全局范围内创建别名, 而仅在函数块作用域中使用.

9. 文件名 

   文件名应该使用小写字符, 以避免在有些系统平台上不识别大小写的命名方式. 文件名以.js结尾, 不要包含除 - 和 _ 外的标点符号(使用 - 优于 _).

10. 构造函数

    使用首字母大写的形式, 通常为名词, 例如: Class; 

	但是, 对于内部基类, 也就是不直接调用生成实例的基类, 使用 _ 和首字母大写的形式命名, 例如: _Base;

11. 布尔值

	以 is 开头的驼峰形式, 例如 var isGirl = true; 

12. this 

	命名为 <del>that</del> <ins>host</ins>(借鉴 YUI3 写法: host 本身有宿主的意思, 而 that 其实基本没有什么语义, 所以相对来说, host 更适合使用); 

13. 在循环中, 尽量使用单字符变量名称, 例如: i, j, k, m, n; 

14. 避免使用保留字或语言构造命名;

    保留字列表:

		abstract boolean break byte case catch char class const
		continue default do double else extends false final finally
		float for function goto if implements import in instanceof
		int interface long native new null package private protected
		public return short static super switch synchronized this
		throw throws transient true try var void while with
    

15. 尽量保持所有名称最短, 但是一定要保证名称具有描述性; 

16. 临时变量命名:

		字符 c, d, e 
		坐标 x, y, z 
		异常 e 
		图形 g 
		对象 o 
		流 in, out 
		字符串 s

**语言规范**

1. 变量: 声明变量必须加上 var 关键字. 

   当你没有写 var, 变量就会暴露在全局上下文中, 这样很可能会和现有变量冲突. 另外, 如果没有加上, 很难明确该变量的作用域是什么, 变量也很可能像在局部作用域中, 很轻易地泄漏到 Document 或者 Window 中, 所以务必用 var 去声明变量.

2. 常量: 常量的形式如: NAMES_LIKE_THIS, 即使用大写字符, 并用下划线分隔. 你也可用 @const 标记来指明它是一个常量. 但请永远不要使用 const 关键词.

   对于基本类型的常量, 只需转换命名.

		/**
		 * The number of seconds in a minute.
		 * @type {number}
		 */
		goog.example.SECONDS_IN_A_MINUTE = 60;

   对于非基本类型, 使用 @const 标记.

		/**
		 * The number of seconds in each of the given units.
		 * @type {Object.<number>}
		 * @const
		 */
		goog.example.SECONDS_TABLE = {
		  minute: 60,
		  hour: 60 * 60,
		  day: 60 * 60 * 24
		}

   这标记告诉编译器它是常量. 

   至于关键词 const, 因为 IE 不能识别, 所以不要使用.

3. 分号: 总是使用分号. 

   如果仅依靠语句间的隐式分隔, 有时会很麻烦. 你自己更能清楚哪里是语句的起止.

   而且有些情况下, 漏掉分号会很危险:

		// 1.
		MyClass.prototype.myMethod = function() {
		  return 42;
		}  // No semicolon here.

		(function() {
		  // Some initialization code wrapped in a function to create a scope for locals.
		})();


		var x = {
		  'i': 1,
		  'j': 2
		}  // No semicolon here.

		// 2.  Trying to do one thing on Internet Explorer and another on Firefox.
		// I know you'd never write code like this, but throw me a bone.
		[normalVersion, ffVersion][isIE]();


		var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]  // No semicolon here.

		// 3. conditional execution a la bash
		-1 == resultOfOperation() || die();

4. 嵌套函数: 可以使用 

   嵌套函数很有用, 比如,减少重复代码, 隐藏帮助函数, 等. 没什么其他需要注意的地方, 随意使用.

5. 块内函数声明: 不要在块内声明一个函数 

   不要写成:

		if (x) {
		  function foo() {}
		}

   虽然很多 JS 引擎都支持块内声明函数, 但它不属于 ECMAScript 规范 (见 ECMA-262, 第13和14条). 各个浏览器糟糕的实现相互不兼容, 有些也与未来 ECMAScript 草案相违背. ECMAScript 只允许在脚本的根语句或函数中声明函数. 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

		if (x) {
		  var foo = function() {}
		}

6. 异常: 可以使用

   你在写一个比较复杂的应用时, 不可能完全避免不会发生任何异常. 大胆去用吧.

7. 自定义异常: 可以使用

   有时发生异常了, 但返回的错误信息比较奇怪, 也不易读. 虽然可以将含错误信息的引用对象或者可能产生错误的完整对象传递过来, 但这样做都不是很好, 最好还是自定义异常类, 其实这些基本上都是最原始的异常处理技巧. 所以在适当的时候使用自定义异常.

8. 标准特性: 总是优于非标准特性.

   最大化可移植性和兼容性, 尽量使用标准方法而不是用非标准方法, (比如, 优先用string.charAt(3) 而不用 string[3] , 通过 DOM 原生函数访问元素, 而不是使用应用封装好的快速接口.

9. 封装基本类型: 不要

   没有任何理由去封装基本类型, 另外还存在一些风险:

		var x = new Boolean(false);
		if (x) {
		  alert('hi');  // Shows 'hi'.
		}

   除非明确用于类型转换, 其他情况请千万不要这样做！

		var x = Boolean(0);
		if (x) {
		  alert('hi');  // This will never be alerted.
		}
		typeof Boolean(0) == 'boolean';
		typeof new Boolean(0) == 'object';

   有时用作 number, string 或 boolean时, 类型的转换会非常实用.

10. 多级原型结构: 不是首选

   多级原型结构是指 JavaScript 中的继承关系. 当你自定义一个D类, 且把B类作为其原型, 那么这就获得了一个多级原型结构. 这些原型结构会变得越来越复杂!

   使用 the Closure 库 中的 goog.inherits() 或其他类似的用于继承的函数, 会是更好的选择. 

		function D() {
		  goog.base(this)
		}
		goog.inherits(D, B);

		D.prototype.method = function() {
		  ...
		};

11. 方法定义: 

		Foo.prototype.bar = function() { ... }; 

    有很多方法可以给构造器添加方法或成员, 我们更倾向于使用如下的形式:

		Foo.prototype.bar = function() {
		  /* ... */
		};

12. 闭包: 可以, 但小心使用.

    闭包也许是 JS 中最有用的特性了. 有一份比较好的介绍闭包原理的文档. 

    有一点需要牢记, 闭包保留了一个指向它封闭作用域的指针, 所以, 在给 DOM 元素附加闭包时, 很可能会产生循环引用, 进一步导致内存泄漏. 比如下面的代码: 

		function foo(element, a, b) {
		  element.onclick = function() { /* uses a and b */ };
		}

    这里, 即使没有使用 element, 闭包也保留了 element, a 和 b 的引用, . 由于 element 也保留了对闭包的引用, 这就产生了循环引用, 这就不能被 GC 回收. 这种情况下, 可将代码重构为:

		function foo(element, a, b) {
		  element.onclick = bar(a, b);
		}

		function bar(a, b) {
		  return function() { /* uses a and b */ }
		}


13. eval(): 只用于解析序列化串 (如: 解析 RPC 响应) 

	eval() 会让程序执行的比较混乱, 当 eval() 里面包含用户输入的话就更加危险. 可以用其他更佳的, 更清晰, 更安全的方式写你的代码, 所以一般情况下请不要使用 eval(). 当碰到一些需要解析序列化串的情况下(如, 计算 RPC 响应), 使用 eval 很容易实现. 

	解析序列化串是指将字节流转换成内存中的数据结构. 比如, 你可能会将一个对象输出成文件形式:

		users = [
		  {
			name: 'Eric',
			id: 37824,
			email: 'jellyvore@myway.com'
		  },
		  {
			name: 'xtof',
			id: 31337,
			email: 'b4d455h4x0r@google.com'
		  },
		  ...
		];

	很简单地调用 eval 后, 把表示成文件的数据读取回内存中.

	类似的, eval() 对 RPC 响应值进行解码. 例如, 你在使用 XMLHttpRequest 发出一个 RPC 请求后, 通过 eval () 将服务端的响应文本转成 JavaScript 对象: 

		var userOnline = false;
		var user = 'nusrat';
		var xmlhttp = new XMLHttpRequest();
		xmlhttp.open('GET', 'http://chat.google.com/isUserOnline?user=' + user, false);
		xmlhttp.send('');
		// Server returns:
		// userOnline = true;
		if (xmlhttp.status == 200) {
		  eval(xmlhttp.responseText);
		}
		// userOnline is now true.

14. with() {}: 不要使用 

	使用 with 让你的代码在语义上变得不清晰. 因为 with 的对象, 可能会与局部变量产生冲突, 从而改变你程序原本的用义. 下面的代码是干嘛的?

		with (foo) {
		  var x = 3;
		  return x;
		}

	答案: 任何事. 局部变量 x 可能被 foo 的属性覆盖, 当它定义一个 setter 时, 在赋值 3 后会执行很多其他代码. 所以不要使用 with 语句.

15. this: 仅在对象构造器, 方法, 闭包中使用. 

	this 的语义很特别. 有时它引用一个全局对象(大多数情况下), 调用者的作用域(使用 eval时), DOM 树中的节点(添加事件处理函数时), 新创建的对象(使用一个构造器), 或者其他对象(如果函数被 call() 或 apply()).

	使用时很容易出错, 所以只有在下面两个情况时才能使用:

	在构造器中
	对象的方法(包括创建的闭包)中

16. for-in 循环: 只用于 object/map/hash 的遍历

	对 Array 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值. 下面就是一些失败的使用案例:

		function printArray(arr) {
		  for (var key in arr) {
			print(arr[key]);
		  }
		}

		printArray([0,1,2,3]);  // This works.

		var a = new Array(10);
		printArray(a);  // This is wrong.

		a = document.getElementsByTagName('*');
		printArray(a);  // This is wrong.

		a = [0,1,2,3];
		a.buhu = 'wine';
		printArray(a);  // This is wrong again.

		a = new Array;
		a[3] = 3;
		printArray(a);  // This is wrong again.

	而遍历数组通常用最普通的 for 循环.

		function printArray(arr) {
		  var l = arr.length;
		  for (var i = 0; i < l; i++) {
			print(arr[i]);
		  }
		}

17. 关联数组: 永远不要使用 Array 作为 map/hash/associative 数组. 

	数组中不允许使用非整型作为索引值, 所以也就不允许用关联数组. 而取代它使用 Object 来表示 map/hash 对象. Array 仅仅是扩展自 Object (类似于其他 JS 中的对象, 就像 Date, RegExp 和 String)一样来使用.


18. 多行字符串: 不要使用 

	不要这样写长字符串:

		var myString = 'A rather long string of English text, an error message \
						actually that just keeps going and going -- an error \
						message to make the Energizer bunny blush (right through \
						those Schwarzenegger shades)! Where was I? Oh yes, \
						you\'ve got an error and all the extraneous whitespace is \
						just gravy.  Have a nice day.';

	在编译时, 不能忽略行起始位置的空白字符; "\" 后的空白字符会产生奇怪的错误; 虽然大多数脚本引擎支持这种写法, 但它不是 ECMAScript 的标准规范.


19. Array 和 Object 直接量: 使用 

	使用 Array 和 Object 语法, 而不使用 Array 和 Object 构造器.

	使用 Array 构造器很容易因为传参不恰当导致错误.

		// Length is 3.
		var a1 = new Array(x1, x2, x3);

		// Length is 2.
		var a2 = new Array(x1, x2);

		// If x1 is a number and it is a natural number the length will be x1.
		// If x1 is a number but not a natural number this will throw an exception.
		// Otherwise the array will have one element with x1 as its value.
		var a3 = new Array(x1);

		// Length is 0.
		var a4 = new Array();

	如果传入一个参数而不是2个参数, 数组的长度很有可能就不是你期望的数值了.

	为了避免这些歧义, 我们应该使用更易读的直接量来声明.

		var a = [x1, x2, x3];
		var a2 = [x1, x2];
		var a3 = [x1];
		var a4 = [];

	虽然 Object 构造器没有上述类似的问题, 但鉴于可读性和一致性考虑, 最好还是在字面上更清晰地指明.

		var o = new Object();

		var o2 = new Object();
		o2.a = 0;
		o2.b = 1;
		o2.c = 2;
		o2['strange key'] = 3;

	应该写成:

		var o = {};

		var o2 = {
		  a: 0,
		  b: 1,
		  c: 2,
		  'strange key': 3
		};

	修改内置对象的原型

20. 修改内置对象的原型: 不要使用

	千万不要修改内置对象, 如 Object.prototype 和 Array.prototype 的原型. 而修改内置对象, 如 Function.prototype 的原型, 虽然少危险些, 但仍会导致调试时的诡异现象. 所以也要避免修改其原型.

21. IE下的条件注释: 不要使用 

	不要这样子写:

		var f = function () {
			/*@cc_on if (@_jscript) { return 2* @*/  3; /*@ } @*/
		};

	条件注释妨碍自动化工具的执行, 因为在运行时, 它们会改变 JavaScript 语法树.



**编码风格**

1. 自定义 toString() 方法: 应该总是成功调用且不要抛异常. 

   可自定义 toString() 方法, 但确保你的实现方法满足: (1) 总是成功 (2) 没有其他负面影响. 如果不满足这两个条件, 那么可能会导致严重的问题, 比如, 如果 toString() 调用了包含 assert 的函数, assert 输出导致失败的对象, 这在 toString() 也会被调用.

2. 延迟初始化: 可以 

   没必要在每次声明变量时就将其初始化.

3. 明确作用域: 任何时候都需要 

   任何时候都要明确作用域 - 提高可移植性和清晰度. 例如, 不要依赖于作用域链中的 window 对象. 可能在其他应用中, 你函数中的 window 不是指之前的那个窗口对象.

4. 代码格式化: 主要依照C++ 格式规范 ( [中文版][c-style-cn] ), 针对 JavaScript, 还有下面一些附加说明.

	* 大括号: 分号会被隐式插入到代码中, 所以你务必在同一行上插入大括号. 例如:

			if (something) {
			  // ...
			} else {
			  // ...
			}

	* 数组和对象的初始化 

      如果初始值不是很长, 就保持写在单行上:

			var arr = [1, 2, 3];  // No space after [ or before ].
			var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.

	* 初始值占用多行时, 缩进2个空格.

			// Object initializer.
			var inset = {
			  top: 10,
			  right: 20,
			  bottom: 15,
			  left: 12
			};

			// Array initializer.
			this.rows_ = [
			  '"Slartibartfast" <fjordmaster@magrathea.com>',
			  '"Zaphod Beeblebrox" <theprez@universe.gov>',
			  '"Ford Prefect" <ford@theguide.com>',
			  '"Arthur Dent" <has.no.tea@gmail.com>',
			  '"Marvin the Paranoid Android" <marv@googlemail.com>',
			  'the.mice@magrathea.com'
			];

			// Used in a method call.
			goog.dom.createDom(goog.dom.TagName.DIV, {
			  id: 'foo',
			  className: 'some-css-class',
			  style: 'display:none'
			}, 'Hello, world!');

	* 比较长的标识符或者数值, 不要为了让代码好看些而手工对齐. 如:

			CORRECT_Object.prototype = {
			  a: 0,
			  b: 1,
			  lengthyName: 2
			};

      不要这样做:

			WRONG_Object.prototype = {
			  a          : 0,
			  b          : 1,
			  lengthyName: 2
			};

	* 函数参数 

      尽量让函数参数在同一行上. 如果一行超过 80 字符, 每个参数独占一行, 并以4个空格缩进, 或者与括号对齐, 以提高可读性. 尽可能不要让每行超过80个字符. 比如下面这样:

			// Four-space, wrap at 80.  Works with very long function names, survives
			// renaming without reindenting, low on space.
			goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
				veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
				tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
			  // ...
			};

			// Four-space, one argument per line.  Works with long function names,
			// survives renaming, and emphasizes each argument.
			goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
				veryDescriptiveArgumentNumberOne,
				veryDescriptiveArgumentTwo,
				tableModelEventHandlerProxy,
				artichokeDescriptorAdapterIterator) {
			  // ...
			};

			// Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
			// low on space.
			function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
						 tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
			  // ...
			}

			// Parenthesis-aligned, one argument per line.  Visually groups and
			// emphasizes each individual argument.
			function bar(veryDescriptiveArgumentNumberOne,
						 veryDescriptiveArgumentTwo,
						 tableModelEventHandlerProxy,
						 artichokeDescriptorAdapterIterator) {
			  // ...
			}

	* 传递匿名函数 

      如果参数中有匿名函数, 函数体从调用该函数的左边开始缩进2个空格, 而不是从 function 这个关键字开始. 这让匿名函数更加易读 (不要增加很多没必要的缩进让函数体显示在屏幕的右侧).

			var names = items.map(function(item) {
									return item.name;
								  });

			prefix.something.reallyLongFunctionName('whatever', function(a1, a2) {
			  if (a1.equals(a2)) {
				someOtherLongFunctionName(a1);
			  } else {
				andNowForSomethingCompletelyDifferent(a2.parrot);
			  }
			});

	* 更多的缩进 

	  事实上, 除了 初始化数组和对象 , 和传递匿名函数外, 所有被拆开的多行文本要么选择与之前的表达式左对齐, 要么以4个（而不是2个）空格作为一缩进层次.

			someWonderfulHtml = '' +
								getEvenMoreHtml(someReallyInterestingValues, moreValues,
												evenMoreParams, 'a duck', true, 72,
												slightlyMoreMonkeys(0xfff)) +
								'';

			thisIsAVeryLongVariableName =
				hereIsAnEvenLongerOtherFunctionNameThatWillNotFitOnPrevLine();

			thisIsAVeryLongVariableName = 'expressionPartOne' + someMethodThatIsLong() +
				thisIsAnEvenLongerOtherFunctionNameThatCannotBeIndentedMore();

			someValue = this.foo(
				shortArg,
				'Some really long string arg - this is a pretty common case, actually.',
				shorty2,
				this.bar());

			if (searchableCollection(allYourStuff).contains(theStuffYouWant) &&
				!ambientNotification.isActive() && (client.isAmbientSupported() ||
													client.alwaysTryAmbientAnyways()) {
			  ambientNotification.activate();
			}

	* 空行 

	  使用空行来划分一组逻辑上相关联的代码片段.

			doSomethingTo(x);
			doSomethingElseTo(x);
			andThen(x);

			nowDoSomethingWith(y);

			andNowWith(z);

	* 二元和三元操作符 

	  操作符始终跟随着前行, 这样就不用顾虑分号的隐式插入问题. 如果一行实在放不下, 还是按照上述的缩进风格来换行.

			var x = a ? b : c;  // All on one line if it will fit.

			// Indentation +4 is OK.
			var y = a ?
				longButSimpleOperandB : longButSimpleOperandC;

			// Indenting to the line position of the first operand is also OK.
			var z = a ?
					moreComplicatedB :
					moreComplicatedC;

	* if...else 写法:

			if (something) {
			  // ...
			} else if(something) {
			  // ...
			} else {
			  // ...
			}

	* switch 语句写法:

			switch(condition) {
				case something:
					//...
				break;
				case something:
					//...
				break;
				default:
					//...
			}

	* try ... catch 语句写法:

			try {
				//...
			} catch(e) {};

			try {
				//...
			} catch(e) {
				//...
			} finally {

			}

	* while 语句写法:

			while(condition) {


			}

	* do ... while 语句写法:

			do {
				//...
			} while(condition);

5. 括号: 只在需要的时候使用 

   不要滥用括号, 只在必要的时候使用它.

   对于一元操作符(如delete, typeof 和 void ), 或是在某些关键词(如 return, throw, case, new )之后, 不要使用括号.

6. 字符串: 用 ' 优于 "

   单引号 (') 优于双引号 ("). 当你创建一个包含 HTML 代码的字符串时就知道它的好处了.

		var msg = 'This is some HTML';

7. 可见性 (私有域和保护域): 推荐使用 JSDoc 中的两个标记: @private 和 @protected 

   JSDoc 的两个标记 @private 和 @protected 用来指明类, 函数, 属性的可见性域.

   标记为 @private 的全局变量和函数, 表示它们只能在当前文件中访问.

   标记为 @private 的构造器, 表示该类只能在当前文件或是其静态/普通成员中实例化; 私有构造器的公共静态属性在当前文件的任何地方都可访问, 通过 instanceof 操作符也可. 

   永远不要为 全局变量, 函数, 构造器加 @protected 标记.

		// File 1.
		// AA_PrivateClass_ and AA_init_ are accessible because they are global
		// and in the same file.

		/**
		 * @private
		 * @constructor
		 */
		AA_PrivateClass_ = function() {
		};

		/** @private */
		function AA_init_() {
		  return new AA_PrivateClass_();
		}

		AA_init_();

   标记为 @private 的属性, 在当前文件中可访问它; 如果是类属性私有, "拥有"该属性的类的所有静态/普通成员也可访问, 但它们不能被不同文件中的子类访问或覆盖.

   标记为 @protected 的属性, 在当前文件中可访问它, 如果是类属性保护, 那么"拥有"该属性的类及其子类中的所有静态/普通成员也可访问. 

   注意: 这与 C++, Java 中的私有和保护不同, 它们是在当前文件中, 检查是否具有访问私有/保护属性的权限, 有权限即可访问, 而不是只能在同一个类或类层次上. 而 C++ 中的私有属性不能被子类覆盖. (C++/Java 中的私有/保护是指作用域上的可访问性, 在可访问性上的限制. JS 中是在限制在作用域上. PS: 可见性是与作用域对应) 

		// File 1.

		/** @constructor */
		  AA_PublicClass = function() {
		};

		/** @private */
		AA_PublicClass.staticPrivateProp_ = 1;

		/** @private */
		AA_PublicClass.prototype.privateProp_ = 2;

		/** @protected */
		AA_PublicClass.staticProtectedProp = 31;

		/** @protected */
		AA_PublicClass.prototype.protectedProp = 4;

		// File 2.

		/**
		 * @return {number} The number of ducks we've arranged in a row.
		 */
		AA_PublicClass.prototype.method = function() {
		  // Legal accesses of these two properties.
		  return this.privateProp_ + AA_PublicClass.staticPrivateProp_;
		};

		// File 3.

		/**
		 * @constructor
		 * @extends {AA_PublicClass}
		 */
		AA_SubClass = function() {
		  // Legal access of a protected static property.
		  AA_PublicClass.staticProtectedProp = this.method();
		};
		goog.inherits(AA_SubClass, AA_PublicClass);

		/**
		 * @return {number} The number of ducks we've arranged in a row.
		 */
		AA_SubClass.prototype.method = function() {
		  // Legal access of a protected instance property.
		  return this.protectedProp;
		};

8. JavaScript 类型: 烈建议你去使用编译器. 

   如果使用 JSDoc, 那么尽量具体地, 准确地根据它的规则来书写类型说明. 目前支持两种 JS2 和 JS1.x 类型规范.

   * JavaScript 类型语言 <a href="js-type.txt" class="expand J_Expand"></a>

     S2 提议中包含了一种描述 JavaScript 类型的规范语法, 这里我们在 JSDoc 中采用其来描述函数参数和返回值的类型.
     JSDoc 的类型语言, 按照 JS2 规范, 也进行了适当改变, 但编译器仍然支持旧语法.

   * JavaScript中的类型  <a href="js-type-example.txt" class="expand J_Expand"></a>

   * 可空 vs. 可选 参数和属性

     JavaScript 是一种弱类型语言, 明白可选, 非空和未定义参数或属性之间的细微差别还是很重要的.

     对象类型(引用类型)默认非空. 注意: 函数类型默认不能为空. 除了字符串, 整型, 布尔, undefined 和 null 外, 对象可以是任何类型.

			/**
			 * Some class, initialized with a value.
			 * @param {Object} value Some value.
			 * @constructor
			 */
			function MyClass(value) {
			  /**
			   * Some value.
			   * @type {Object}
			   * @private
			   */
			  this.myValue_ = value;
			}

     告诉编译器 myValue_ 属性为一对象或 null. 如果 myValue_ 永远都不会为 null, 就应该如下声明: 

			/**
			 * Some class, initialized with a non-null value.
			 * @param {!Object} value Some value.
			 * @constructor
			 */
			function MyClass(value) {
			  /**
			   * Some value.
			   * @type {!Object}
			   * @private
			   */
			  this.myValue_ = value;
			}

     这样, 当编译器在代码中碰到 MyClass 为 null 时, 就会给出警告.

     函数的可选参数可能在运行时没有定义, 所以如果他们又被赋给类属性, 需要声明成:

			/**
			 * Some class, initialized with an optional value.
			 * @param {Object=} opt_value Some value (optional).
			 * @constructor
			 */
			function MyClass(opt_value) {
			  /**
			   * Some value.
			   * @type {Object|undefined}
			   * @private
			   */
			  this.myValue_ = opt_value;
			}

     这告诉编译器 myValue_ 可能是一个对象, 或 null, 或 undefined.

     注意: 可选参数 opt_value 被声明成 {Object=}, 而不是 {Object|undefined}. 这是因为可选参数可能是 undefined. 虽然直接写 undefined 也并无害处, 但鉴于可阅读性还是写成上述的样子.

     最后, 属性的非空和可选并不矛盾, 属性既可是非空, 也可是可选的. 下面的四种声明各不相同:

			/**
			 * Takes four arguments, two of which are nullable, and two of which are
			 * optional.
			 * @param {!Object} nonNull Mandatory (must not be undefined), must not be null.
			 * @param {Object} mayBeNull Mandatory (must not be undefined), may be null.
			 * @param {!Object=} opt_nonNull Optional (may be undefined), but if present,
			 *     must not be null!
			 * @param {Object=} opt_mayBeNull Optional (may be undefined), may be null.
			 */
			function strangeButTrue(nonNull, mayBeNull, opt_nonNull, opt_mayBeNull) {
			  // ...
			};

9. 编译: 推荐使用.

   建议您去使用 JS 编译器, 如 Closure Compiler.


10. var: 尽量在函数头部统一声明, 局部变量声明时不要丢失 var, 避免嵌套声明( var a=(b=(c+5)+1)+3 ). 例如:

		var a = 1, 
			b = 2;

11. 尽量避免将基本类型转换为 object, 例如: var x = new Number(1);

12. 在为对象定义 toString() 方法时, 请不要对源对象进行修改;
 
**注释**

我们使用 [JSDoc][jsdoc] 中的注释风格. 行内注释使用 // 变量 的形式. 另外, 我们也遵循 [C++ 代码注释风格][c-style-cn] . 这也就是说你需要: 

* 版权和著作权的信息,
* 文件注释中应该写明该文件的基本信息(如, 这段代码的功能摘要, 如何使用, 与哪些东西相关), 来告诉那些不熟悉代码的读者.
* 类, 函数, 变量和必要的注释,
* 期望在哪些浏览器中执行,
* 正确的大小写, 标点和拼写.

为了避免出现句子片段, 请以合适的大/小写单词开头, 并以合适的标点符号结束这个句子.

现在假设维护这段代码的是一位初学者. 这可能正好是这样的!

目前很多编译器可从 JSDoc 中提取类型信息, 来对代码进行验证, 删除和压缩. 因此, 你很有必要去熟悉正确完整的 JSDoc .

1. 顶层/文件注释

   顶层注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西. 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息. 如下:
 
		// Copyright 2009 Google Inc. All Rights Reserved.

		/**
		 * @fileoverview Description of file, its uses and information
		 * about its dependencies.
		 * @author user@google.com (Firstname Lastname)
         * @modified shiran 2011-2-18
		 */
 
2. 类注释

   每个类的定义都要附带一份注释, 描述类的功能和用法. 也需要说明构造器参数. 如果该类继承自其它类, 应该使用 @extends 标记. 如果该类是对接口的实现, 应该使用 @implements 标记.
 
		/**
		 * Class making something fun and easy.
		 * @param {string} arg1 An argument that makes this more interesting.
		 * @param {Array.<number>} arg2 List of numbers to be processed.
		 * @constructor
		 * @extends {goog.Disposable}
		 */
		project.MyClass = function(arg1, arg2) {
		  // ...
		};
		goog.inherits(project.MyClass, goog.Disposable);

 
3. 方法与函数的注释

   提供参数的说明. 使用完整的句子, 并用第三人称来书写方法说明.
 
		/**
		 * Converts text to some completely different text.
		 * @param {string} arg1 An argument that makes this more interesting.
		 * @return {string} Some return value.
		 */
		project.MyClass.prototype.someMethod = function(arg1) {
		  // ...
		};

		/**
		 * Operates on an instance of MyClass and returns something.
		 * @param {project.MyClass} obj Instance of MyClass which leads to a long
		 *     comment that needs to be wrapped to two lines.
		 * @return {boolean} Whether something occured.
		 */
		function PR_someMethod(obj) {
		  // ...
		}

   对于一些简单的, 不带参数的 getters, 说明可以忽略.

		/**
		 * @return {Element} The element for the component.
		 */
		goog.ui.Component.prototype.getElement = function() {
		  return this.element_;
		};
 
4. 属性注释: 
 
		/**
		 * Maximum number of things per pane.
		 * @type {number}
		 */
		project.MyClass.prototype.someProperty = 4;

5. 类型转换的注释 

   有时, 类型检查不能很准确地推断出表达式的类型, 所以应该给它添加类型标记注释来明确之, 并且必须在表达式和类型标签外面包裹括号.

	/** @type {number} */ (x)
	(/** @type {number} */ x)

6. 枚举

		/**
		 * Enum for tri-state values.
		 * @enum {number}
		 */
		project.TriState = {
		  TRUE: 1,
		  FALSE: -1,
		  MAYBE: 0
		};

   注意一下, 枚举也具有有效类型, 所以可以当成参数类型来用.

		/**
		 * Sets project state.
		 * @param {project.TriState} state New project state.
		 */
		project.setState = function(state) {
		  // ...
		};

7. JSDoc 缩进 

   如果你在 @param, @return, @supported, @this 或 @deprecated 中断行, 需要像在代码中一样, 使用4个空格作为一个缩进层次.

		/**
		 * Illustrates line wrapping for long param/return descriptions.
		 * @param {string} foo This is a param with a description too long to fit in
		 *     one line.
		 * @return {number} This returns something that has a description too long to
		 *     fit in one line.
		 */
		project.MyClass.prototype.method = function(foo) {
		  return 5;
		};

   不要在 @fileoverview 标记中进行缩进.

   虽然不建议, 但也可对说明文字进行适当的排版对齐. 不过, 这样带来一些负面影响, 就是当你每次修改变量名时, 都得重新排版说明文字以保持和变量名对齐.

		/**
		 * This is NOT the preferred indentation method.
		 * @param {string} foo This is a param with a description too long to fit in
		 *                     one line.
		 * @return {number} This returns something that has a description too long to
		 *                  fit in one line.
		 */
		project.MyClass.prototype.method = function(foo) {
		  return 5;
		};

8. 例子注释:

		/**
		 * @example
		 * var bleeper = makeBleep(3);
		 * bleeper.flop();
		 */

9. Typedefs 

   有时类型会很复杂. 比如下面的函数, 接收 Element 参数:

		/**
		 * @param {string} tagName
		 * @param {(string|Element|Text|Array.<Element>|Array.<Text>)} contents
		 * @return {Element}
		 */
		goog.createElement = function(tagName, contents) {
		  ...
		};

   你可以使用 @typedef 标记来定义个常用的类型表达式. 

		/** @typedef {(string|Element|Text|Array.<Element>|Array.<Text>)} */
		goog.ElementContent;

		/**
		* @param {string} tagName
		* @param {goog.ElementContent} contents
		* @return {Element}
		*/
		goog.createElement = function(tagName, contents) {
		...
		};

10. JSDoc 标记表 <a href="jsdoc-tag.txt" class="expand J_Expand"></a>

11. 在第三方代码中, 你还会见到其他一些 JSDoc 标记. 这些标记在 [JSDoc Toolkit Tag Reference][jsdoc-tag] 都有介绍到, 但在 Google 的代码中, 目前不推荐使用. 你可以认为这些是将来会用到的 "保留" 名. 它们包含: 

	* @augments
	* @argument
	* @borrows
	* @class
	* @constant
	* @constructs
	* @default
	* @event
	* @example
	* @field
	* @function
	* @ignore
	* @inner
	* @link
	* @memberOf
	* @name
	* @namespace
	* @property
	* @public
	* @requires
	* @returns
	* @since
	* @static
	* @version

12. JSDoc 中的 HTML
 
	类似于 JavaDoc, JSDoc 支持许多 HTML 标签, 如 `<code>, <pre>, <tt>, <strong>, <ul>, <ol>, <li>, <a>,` 等等.

	这就是说 JSDoc 不会完全依照纯文本中书写的格式. 所以, 不要在 JSDoc 中, 使用空白字符来做格式化:

		/**
		 * Computes weight based on three factors:
		 *   items sent
		 *   items received
		 *   last timestamp
		 */

	上面的注释, 出来的结果是:

		Computes weight based on three factors: items sent items received items received 

	应该这样写:

		/**
		 * Computes weight based on three factors:
		 * <ul>
		 * <li>items sent
		 * <li>items received
		 * <li>last timestamp
		 * </ul>
		 */

	另外, 也不要包含任何 HTML 或类 HTML 标签, 除非你就想让它们解析成 HTML 标签.

		/**
		 * Changes <b> tags to <span> tags.
		 */

	出来的结果是:

		Changes tags to tags. 

	另外, 也应该在源代码文件中让其他人更可读, 所以不要过于使用 HTML 标签:

		/**
		 * Changes &lt;b&gt; tags to &lt;span&gt; tags.
		 */

	上面的代码中, 其他人就很难知道你想干嘛, 直接改成下面的样子就清楚多了:

		/**
		 * Changes 'b' tags to 'span' tags.
		 */

13. @TODO 注释表示将要做的东西, 请注明大概完成日期, 不要让此注释常驻; 

14. @FIXME 表示被注释的代码需要被修正, 请注明大概完成日期, 不要让此注释常驻; 

15. @XXX 表示被注释的代码虽然实现了功能, 但是实现方案有待商榷, 希望将来能改进, 请注明大概完成日期, 不要让此注释常驻;

接口
----------

1. 单一职能原则:

   一个函数或者一个类只应该负责一件事, 这可以为我们后期的维护以及测试节省很多的成本.

   比如: YUI.DOM.setStyle 专门负责设置元素样式, 而 YUI.DOM.getStyle 负责获取元素样式.

2. 接口分离原则:

   跟单一职能原则联系比较紧密, 遵循单一职能原则, 将功能进行拆分.

   比如: dojo.style 方法, 它本身包含了 get 和 set 两个接口, 应该将其拆分, 如 YUI.DOM.setStyle, YUI.DOM.getStyle.

3. 遵循现有规范/标准:

   所有的接口设计都应该遵循已有的接口以及现有的规范, 不要因个人的喜好去做修改, 简化或者美化, 带来的学习, 使用成本都会很高.

   比如: Ajbridge.store.getItem, Ajbridge.store.setItem 与现代浏览器的本地存储接口一致: localStorage.getItem, localStorage.setItem.

   比如: KISSY.indexOf(value, array, fromIndex) 的参数顺序, 在原生支持的浏览器下, 接口为 Array.indexOf(value, fromIndex), 但是 KISSY 的 indexOf 方法颠倒了参数的顺序, 违背了使用习惯以及现有规范, 为使用者得学习带来较高成本. ([Mozilla Array IndexOf][moz-array-indexof])

4. 接口应该有合理的返回值, 应正确区分 undefined 和 null:

   合理的返回值可以减轻我们很多的工作量, 在使用过程中会更顺畅.

   比如: UA.ie, 在 ie 浏览器下我们应该返回正确的版本号, 而在其它浏览器下应该返回 undefined.

5. 不要过多的干预使用者:

   我们不应该想当然的认为使用者应该怎样使用, 而应与实践相结合提供接口.

   比如: 异步请求的回调函数, 我们应该为使用者提供什么样的参数? 添加什么样的作用域? 这个应该由用于来决定, 而不是由我们来决定.


 
数据
----------
 
1. 返回的数据以标准的 JSON 格式来书写:

		{
			"result": {
				"name": "jolin",
				"age": 30,
				"other": [1, 2]
			},
			"status": "1",
			"msg": "系统错误, 请稍候再试"			
		}



参考资料:
----------

* [Google JavaScript Style Guide][gjsg]
* [Google JavaScript Style Guide 中文版][gjsg-cn]
* [Code Style][cs]
* [IE 条件注释][ie-comment]
* [ OOP 设计原则][oop-design]
* [ HTML5 设计原理][html5-theory]
* [ Mozilla Developer ][mdc]
* [The Principles of Good Programming][TPOGP]
* [Real World CSS Practices][RWCP]
* [10 best practices to follow while writing code comments][BestComemntPractices]

[strong&em]: http://www.css88.com/archives/644 "em和strong的区别"
[w3-custom-data]: http://dev.w3.org/html5/spec/Overview.html#embedding-custom-non-visible-data-with-the-data-attributes "Embedding custom non-visible data with the data-* attributes"
[css-border]: http://archivist.incutio.com/viewlist/css-discuss/6297 "[css-d] border: 0; vs. border: none;"
[gjsg]: http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Nested_functions#Nested_functions 
[gjsg-cn]: http://docs.kissyui.com/docs/html/styleguide/google/javascriptguide.xml
[cs]: http://www.codestyle.org/
[q-html]: #HTML
[q-css]: #CSS
[q-js]: #JavaScript
[Closure Library]: http://code.google.com/closure/library/
[Dojo]: http://www.dojotoolkit.org/
[c-style-cn]: http://yangyubo.com/google-cpp-styleguide/formatting.html
[jsdoc]: http://code.google.com/p/jsdoc-toolkit/
[jsdoc-tag]: http://code.google.com/p/jsdoc-toolkit/wiki/TagReference
[inline-rule]: http://www.junchenwu.com/2007/01/allowed_nesting_of_elements_in_html_4_strict_and_xhtml_10_strict.html
[ie-comment]: http://wenku.baidu.com/view/f24197b665ce05087632133c.html
[oop-design]: http://blog.csdn.net/httphttpcn/archive/2010/12/16/6079004.aspx
[html5-theory]: http://www.cn-cuckoo.com/2010/10/21/the-design-of-html5-2151.html
[moz-array-indexof]: https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Array/indexOf
[mdc]: https://developer.mozilla.org/
[TPOGP]: http://www.artima.com/weblogs/viewpost.jsp?thread=331531
[section]: http://www.w3.org/TR/2011/WD-html5-20110525/sections.html#the-section-element
[RWCP]: http://blog.echoenduring.com/2011/08/19/real-world-css-practices/
[BestComemntPractices]: http://www.yousaytoo.com/10-best-practices-to-follow-while-writing-code-comments/981354
