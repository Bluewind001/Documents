
Markdown 的宗旨是实现「易读易写」。一份Markdown文件是以纯文本的形式发布的，可以使普通文本具有一定的格式。Markdown语法是由一些符号组成的，而且这些符号简单易懂。

Markdown 和 HTML 是不同，但类似。HTML是一种发布的格式，Markdown是一种书写的格式。Markdown是想让文档更容易读、写和改。它兼容HTML标签，不在Markdown涵盖范围之内的标签都可以直接用HTML语法来实现，也就是说Markdown文件中可以方便的嵌套HTML标签。但是在HTML __区块标签__ 内使用Markdown的语法是无效的，但是在HTML __区段标签__ 内是有效的。比如我的blog就是用Markdown，其中的代码显示部分使用的HTML标签「并没有用Markdown本身的显示代码的语法，主要是显示的太丑了」。在Markdown中插入HTML便签，有的需要在其前后加上空行与其他内容分开，有的则不需要，建议都加上空行也方便显示。同时还要求开始标签和结束标签不能用制表符或空格来缩进。

**一些特殊字符：**如`'<'和'&'`字符如果想显示他们的原型就要写成`&lt;和&amp;`，还有支持版权字符比如你想显示 &copy; 写`&copy;`就可以了。
<br/>

#### **Markdown的语法：**
**Markdown段落：**
前后要有一个上的空行，且普通的段落不能用制表符或空格来缩进，其中的换行可以用`<br />`来实现。
<br/>

**Markdown标题：**
在行首插入1到6个`#`就对应1到6阶标题，如：
```
#这是一阶标题
##这是二阶标题
######这是六阶标题
```
同样可以在行尾加上`#`，使其闭合，但是行尾的个数无影响，随便几个都可以。
<br/>

**区块引用：**
在文章中插入一段引用在行首加入`>`，效果如
```
>这是一个引用段落 
```
效果：
>这是一个引用段落

你可以在引用段落的每一行行首都加上`>`，也可以只加在段落的第一行。
引用可以嵌套，只要更具层次加上不同个数的`>`。
在引用块中可以使用Markdown的其他语法，包括标题，列表等：
```
> #这是一个一级标题
```
如果引用段落结束，需要在最后多加一个空行。
<br/>

**列表：**
支持有序列表和无序列表。

无序列表用` * ，  + ， - `作为标记：
```
+ 列表一
+ 列表二
+ 列表三
```
效果：

+ 列表一
+ 列表一
+ 列表一

换成`+ 或 -` 效果一样。

有序列表：
```
1. 1
2. 2
3. 3
4. 4
8. 5
```
效果：

1. 1
2. 2
3. 3
4. 4
8. 5

在列表标记上的数字不会影响显示的结果。列表标记的开始前要和前面的内容空一行以上。如果列表之间有空行则会在列表项中加上了`<p>`标签，
```
1. 1

2. 2

3. 3

4. 4

8. 5
```
效果「间隔会大一点」：

1. 1

2. 2

3. 3

4. 4

8. 5

如果需要在列表里放置多个段落，至少首行需要缩进4 个空格或是 1 个制表符：
```
+ this is one.
	this is two.

+ this is 1.
	this is 2.
``` 
效果：

+ this is one.
	this is two.

+ this is 1.
	this is 2.

如果要放代码区块的话，该区块就需要空一行且缩进两次「也就是 8 个空格或是 2 个制表符」：
```
+ this is one.
	this is two.
		
		#include<iostream>
		using namespace std;
		int main(){
			int a = 0;
			return 0;
		}
+ this is 1.
	this is 2.
```
<br/>

**代码区块：**
Markdown 会用`<pre>`和`<code>`标签来把代码区块包起来。在Markdown建立代码区块只需要简单的缩进一行就可以，这里要强调的是代码的每一行都要缩进，这个缩进不会显示出来，一个代码区块会一直持续到没有缩进的那一行。代码区块里的特殊符号直接会被转换成本身的意义，如：`& < 和 >`。

如果想在段落中插一小段代码可以用“ ` ”符号「键盘中1键左面那个，反引号」中间包含的就是代码片段。也可以使用三个反引号单独一行作为代码的开始标记，在次利用三个反引号可以作为结束标记。同时也可以加上是什么语言。
```
	``` c++
		#include<iostream>
		using namespace std;
		
		int main(){
			int a = 1;
			cout << a << endl;
			return 0;
		}
	```
```
效果：
``` c++
	#include<iostream>
	using namespace std;
	
	int main(){
		int a = 1;
		cout << a << endl;
		return 0;
	}
```
<br/>

**链接：**
链接方式有两种。
一种是用“[]”扩起来链接文字接着在后面的小括号里面写上网址链接，如果想加上链接的 title 的话，在网址后面用双引号把title引起来就可以了。
如：
```
This is an example [link](http://example.com/ "title").
```
效果： This is an example [link](http://example.com/ "title").

另一种是在链接文字后面在加一个方括号，在第二个方括号中要填上标识链接的id，链接辨别标签可以有字母、数字、空白和标点符号，但是并不区分大小写。同时可以在两个中括号之间加上最多一个空格，可以在文件的任意处，把这个标记的链接内容定义出来。
如：
```
This is another [link][id].
[id]: http://example.com "title"
```
效果：  This is another [link][id].
[id]: http://example.com "title"
<br/>
链接内容定义的形式为：

+ 方括号（前面可以选择性地加上至多三个空格来缩进），里面输入链接文字
+ 接着一个冒号
+ 接着一个以上的空格或制表符
+ 接着链接的网址
+ 选择性地接着 title 内容，可以用单引号、双引号或是括弧包着

Markdown支持隐式链接，就是在id的方括号内不写id，把链接文字当作id：

	I get 10 times more traffic from [Google][] than from
	[Yahoo][] or [MSN][].
	
	[google]: http://google.com/        "Google"
	[yahoo]:  http://search.yahoo.com/  "Yahoo Search"
	[msn]:    http://search.msn.com/    "MSN Search"
<br/>

**强调：**
被`* 或 _`包围的字就是强调的文字。一个符号表示斜体，两个符号连用表示加粗。但是注意符号的内测不能是空格。
` *斜体* `  ------>效果：*斜体* 
`_斜体_`   -------->效果：_斜体_
`**加粗**`   -------->效果：**加粗**
`__加粗__`   -------->效果：__加粗__
<br/>

**分割符**
单独一行`---`，效果：

--------------
<br/>

**删除线**
在要划删除线的文本前后添加\~\~，如`\~\~看《冰与火之歌》\~\~`，效果：~~看冰与火之歌~~
<br/>


**小功能**

1. 要想使用缩进，在中文输入法中改成「全角」输入，再按两个空格。
2. 想要分成两行，需要在行尾输入两个空格。
3. 标签功能
4. 注脚功能，实例：`You can create footnotes like this[^footnote].`<br/> ` [^footnote]: Here is the *text* of the **footnote**.`
5. 公式的使用可是访问 [MathJax](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference) 参考更多使用方法。
6. 定义型列表。词的下一行使用`：`加Tab键。如下：

定义A
:	这里是定义

可以使用图标：http://fortawesome.github.io/Font-Awesome/3.2.1/icons/
<br/>

**待办事宜 Todo 列表**
使用带有 [ ] 或 [x] （未完成或已完成）项的列表语法撰写一个待办事宜列表，并且支持子列表嵌套以及混用Markdown语法，例如：
``` makedown
 - [ ] **Cmd Markdown 开发**
        - [ ] 改进 Cmd 渲染算法，使用局部渲染技术提高渲染效率
        - [ ] 支持以 PDF 格式导出文稿
        - [x] 新增Todo列表功能 [语法参考](https://github.com/blog/1375-task-lists-in-gfm-issues-pulls-comments)
        - [x] 改进 LaTex 功能
            - [x] 修复 LaTex 公式渲染问题
            - [x] 新增 LaTex 公式编号功能 [语法参考](http://docs.mathjax.org/en/latest/tex.html#tex-eq-numbers)
    - [ ] **七月旅行准备**
        - [ ] 准备邮轮上需要携带的物品
        - [ ] 浏览日本免税店的物品
        - [x] 购买蓝宝石公主号七月一日的船票
```

-[] something1
	-[] something 2
	-[x] somtthing 3
-[x] this is down

<br/>

**插入图片：**
图片的链接和普通的链接很像，就是在普通额链接文字前面加上一个感叹号“ ! ”。也是可以使用两种方法。图片会直接显示到网页中。
方法1：
`this is ![picture](http://pic26.nipic.com/20121227/2531170_112836130000_2.jpg "title") `   注：此图片来源于网上。

方法2：
` this is ![picture][id]
[id]: http://pic26.nipic.com/20121227/2531170_112836130000_2.jpg "title2" `

图片的显示可以用`<img>`代替。




Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

\   反斜线
`   反引号
*   星号
_   底线
{}  花括号
[]  方括号
()  括弧
\#   井字号
+   加号
-   减号
.   英文句点
!   惊叹号
<br/>

上面摘自：http://wowubuntu.com/markdown/   和  http://www.markdown.cn/

<br/>
补充内容：流程图的简单使用。       ------ by wy 2015.9.12
画简单的流程图：
```sequence
Title: Here is title.
#Example of a comment, just a comment, cannt see this.
DispatcherServlet->Controller: D to C
Controller-->DispatcherServlet: C to D
DispatcherServlet->>Model: D to M
DispatcherServlet-->>View: D to V
```
上面的代码：
```
	```sequence
	Title: Here is title.
	#Example of a comment, just a comment, cannt see this.
	DispatcherServlet->Controller: D to C
	Controller-->DispatcherServlet: C to D
	DispatcherServlet->>Model: D to M
	DispatcherServlet-->>View: D to V
	```
```
注意：语言说明**sequence**是必须的，因为还会有其他的比图flow。可以画**4种不同的箭头**，但是要注意：在画箭头的语句中的**`->`**这部分左右两侧最好不要添加空格，同时语句中的**`:`**部分左侧不要有空格，右侧最好有空格「为了美观」。

```sequence
Title: this note.
participant B
participant C
participant A
Note left of A: this is left\n note of A.
Note over B: Note over B
Note over B,C: Note over\n both B and C
Note right of C: this is right\n note of C.
```
上面例子的代码：
```
	```sequence
	Title: this note.
	participant B
	participant C
	participant A
	Note left of A: this is left\n note of A.
	Note over B: Note over B
	Note over B,C: Note over\n both B and C
	Note right of C: this is right\n note of C.
	```
```
可以通过定义参与者改变它们的顺序。还可以添加一些note，语法如上。
详细的例子请查阅：http://bramp.github.io/js-sequence-diagrams/


``` flow
st=>start: Start:>http://cn.bing.com[blank]
e=>end:>http://cn.bing.com
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes or No?:>http://cn.bing.com
io=>inputoutput: catch something...

st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```
基本元素：start,end,operation,subroutine,condition,inputoutput。

可以给每个元素设置链接：语句后面加上 ":>http://cn.bing.com[blank]" 
可以指定连接线的位置如cond(yes,bottom) cond(yes,right/left)。或者指定其他链接线的位置，sub(right/left/bottom) 不知道上面是什么。

``` flow
st=>start: Start|past:>http://cn.bing.com[blank]
e=>end: End|future:>http://cn.bing.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes
or No?|approved:>http://cn.bing.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|future

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
```
可以指定每个元素的状态，使用"| 
past/future/current/invalid/apporved/rejected"，

流程图：http://adrai.github.io/flowchart.js/

__表格语法__：

基本格式：
one|two|three
---|---|----
1  |2  |3
4  |5  |6
代码：
``` markdown
one|two|three
---|---|----
1  |2  |3
4  |5  |6
```
每列的宽度是根据内容自动调整的，这里面的是最根本的语法形式。同样可以在每行的左右再加上“ | ” 如：|1 | 2 | 3| ，也是可以的。
可以设置每列的对齐方式，但是无法设置列名的对齐方式：
|左对齐 | 右对齐| 居中对齐 |
|:-------|------:|:---------:|
|这里的内容比较长| 这内容短可以看出是|这里长度正好是居中对齐的|
|可以看出是左对齐的|右对齐的|注意列名的位置|
代码：
``` markdown
|左对齐 | 右对齐| 居中对齐 |
|:-------|------:|:---------:|
|这里的内容比较长| 这内容短可以看出是|这里长度正好是居中对齐的|
|可以看出是左对齐的|右对齐的|注意列名的位置|

```


