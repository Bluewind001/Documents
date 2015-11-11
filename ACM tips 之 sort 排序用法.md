&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在ACM解题过程中，经常碰到排序问题，刚接触的人可能会自己去写排序，不仅是为了熟悉算法的思想，也是为了练习写代码的能力。但熟悉了之后就不需要在自己写了，调用c++的库就好了。接下来进入正题。介绍几个简单的方法。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这篇文章知识简单的提了一下排序函数的调用，还有很多其他的内容，如：稳定排序。希望看完之后可以自己扩展阅读。我在最后贴了一个链接。后续我会继续更新。

##数组排序：
<pre name="code" class="cpp">
    // 初始化数组
    int a[10] ={23,32,54,12,52,56,8,30,44,94};
    int len = 10;
    
    // 排序方法
    sort(a,a+len);
    
    // 显示
    for(int i=0; i&lt;len; ++i)
        printf(&quot;%d &quot;,a[i]);
    printf(&quot;\n&quot;);

	//结果 8 12 23 30 32 44 52 54 56 94
</pre>
<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sort函数的头文件，必须要` #include<algorithm> `，第一个参数是要排序数组的开头，第二个参数是最后一个数字的下一个位置。如果数组的下标从1开始的话就是：`sort(a+1,a+1+len)`而排序的结果是按照从小到大排序的。

如果要想从大到小排序，需要自己写排序的函数，作为sort函数的第三个参数传进去，
<pre name="code" class="cpp">
	// 排序规则定义，从大到小
	bool cmp(const int &amp;a, const int &amp;b){
	    return a&gt;b;
	}
	
	// 初始化数组
	int a[10] ={23,32,54,12,52,56,8,30,44,94};
	int len = 10;
	
	// 排序     这里加上了第三个参数
	sort(a,a+len,cmp);
	
	// 显示
	for(int i=0; i&lt;len; ++i)
		printf(&quot;%d &quot;,a[i]);
	printf(&quot;\n&quot;);

	//结果 94 56 54 52 44 32 30 23 12 8
</pre>
<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;函数的写法，一定要就加上` const `和` & `修饰。比较函数体写法：第一个参数小于第二个参数，就是升序；第一个参数大于第二个参数就是降序「是不是很好记 ^-^」。

<br/>
##结构体数组排序
结构体排序有两种方法，一种和数组的排序类似，如。
<pre name="code" class="cpp">
	// 结构体定义
	struct Node{
	    int x;
	    int y;
	    int z;
	    Node(){x=0; y=0; z=0;}
	};
	
	// 定义结构体数组
	Node a[10];
	
	/*
	   函数的排序规则和数组排序的一样，对应第一个参数和第二个参数。<br/>
	   函数说明：
	   首先按照x升序排序，
	   如果x相同了就按照y降序排序，
	   如果y相同了就按照z升序排序。
	*/
	bool cmp(const Node &amp;a, const Node &amp;b){
	   if(a.x!=b.x)
	       return a.x&lt;b.x;
	   else if(a.y!=b.y)
	       return a.y&gt;b.y;
	   else return a.z&lt;b.z;
	}

	// 排序函数调用
	sort(a,a+len,cmp);
</pre>
<br />
另一种就是在结构体里定义排序规则，重载符号操作符。
<pre name="code" class="cpp">
	// 结构体定义
	struct Node{
	    int x;
	    int y;
	    int z;
	    Node(){x=0; y=0; z=0;}
	    
		// 排序规则定义，同样b代表第二个参数，意义同前。
	    bool operator &lt; (const Node &amp;b)const{
	        if(x!=b.x)
	            return x&lt;b.x;
	        else if(y!=b.y)
	            return y&gt;b.y;
	        else return z&lt;b.z;
	    }
	};
	
	Node a[10];
	
	// 排序方法
    sort(a,a+len);
    
    //这里同样适用sort(a+1,a+1+len),这种写法。
</pre>
<br />


##STL排序
STL排序也有两种，一种还是写排序函数，适用于容器在装元素的时候无序装载，排序需要调用sort函数排序。如：vector。
<pre name="code" class="cpp">
	// 结构体定义
	struct Node{
	    int x;
	    int y;
	    int z;
	    Node(){x=0; y=0; z=0;}
	};
	
	// 定义排序函数
	bool cmp(const Node &amp;a, const Node &amp;b){
	    if(a.x!=b.x)
	        return a.x&lt;b.x;
	    else if(a.y!=b.y)
	        return a.y&gt;b.y;
	    else return a.z&lt;b.z;
	}
	
	// 变量声明
	vector&lt;Node&gt; vet;
	
	// 排序调用
	sort(vet.begin(),vet.end(),cmp);
</pre>
<br />
另一种适用于在容器装载元素的时候就是按照顺序装载的。如set，这种需要自己重载操作符。
<pre name="code" class="cpp">
	// 结构体定义
	struct Node{
	    int x;
	    int y;
	    int z;
	    Node(){x=0; y=0; z=0;}
	};
	
	// 排序结构体定义
	struct cmp{
	    bool operator ()(const Node &amp;a, const Node &amp;b){
		    if(a.x!=b.x)
		        return a.x&lt;b.x;
		    else if(a.y!=b.y)
		        return a.y&gt;b.y;
		    else return a.z&lt;b.z;
	    }
	};
	
	// 变量定义和声明，在插入的时候会自动排序
	set&lt;Node, cmp&gt; sets;
</pre>
<br/>

扩展阅读：
http://www.cnblogs.com/BeyondAnyTime/archive/2012/05/26/2519492.html
