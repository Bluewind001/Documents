转载请注明出处： 
http://blog.csdn.net/wybluewind/article/details/47756905

codeforces 上的题解：http://codeforces.com/blog/entry/15353
<br/>

##[A. Watching a movie][A]
[A]: http://codeforces.com/contest/499/problem/A "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;播放器上有两个按钮，一个是看当前一分钟的电影，另一个是跳过x分钟，即如果当前播放的是第t分钟，按完这个按钮就跳到了（t+x）分钟。给出一个电影的多个高潮部分要全部看完，至少要看多少分钟。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;简单题，标记当前的播放分钟数，找到离下一个高潮开始时间最近的可以跳到的时间点，这个时间点就是需要开始看的最早时间。加上此时间到结束的时间差「不要忘了要+1」，把当前时间标记未结束时间的下一分钟，继续循环就行了。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cstdio&gt;
	#include&lt;cstdlib&gt;
	#include&lt;utility&gt;
	#include&lt;algorithm&gt;
	using namespace std;
	
	int n,x;
	pair&lt;int , int&gt; best[55];
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	    while(cin &gt;&gt; n &gt;&gt; x){
	        for(int i=0; i&lt;n; ++i){
	            cin &gt;&gt; best[i].first &gt;&gt; best[i].second;
	        }
	        sort(best,best+n);
	        int st = 1;
	        int ans=0;
	        for(int i=0; i&lt;n; ++i){
	            int diff = best[i].first-st;
	            ans += diff - diff/x * x + best[i].second-best[i].first+1;
	            st = best[i].second+1;
	        }
	        printf(&quot;%d\n&quot;,ans);
	    }
	    return 0;
	}
</pre>
<br/>

##[B. Lecture][B]
[B]: http://codeforces.com/contest/499/problem/B "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;给出1和2两种语言同意单词的对照表，给出第1种语言的多个单词，如果第2种语言同意单词比这个短，则用第2种语言的此单词代替。输出替换后的结果。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;利用map存1和2种语言的对照，输入存到string数组里，一个个判断，若小则替换。在输出就好了。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;string&gt;
	#include&lt;cstdio&gt;
	#include&lt;cstring&gt;
	#include&lt;cstdio&gt;
	#include&lt;map&gt;
	using namespace std;
	
	int n,m;
	map&lt;string, string&gt; mp;
	string content[3009];
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	    while(cin &gt;&gt; n &gt;&gt; m){
	        for(int i=0; i&lt;m; ++i){
	            string s1,s2;
	            cin &gt;&gt; s1 &gt;&gt; s2;
	            mp[s1]=s2;
	        }
	        for(int i=0; i&lt;n; ++i)
	            cin &gt;&gt; content[i];
	
	        for(int i=0; i&lt;n; ++i){
	            int len1 = content[i].size();
	            int len2 = mp[content[i]].size();
	            if(len1&gt;len2)
	                content[i] = mp[content[i]];
	        }
	        cout &lt;&lt; content[0] ;
	        for(int i=1; i&lt;n; ++i){
	            cout &lt;&lt; &quot; &quot; &lt;&lt; content[i];
	        }
	        printf(&quot;\n&quot;);
	    }
	    return 0;
	}
</pre>
<br />


##[C. Crazy Town][C]
[C]: http://codeforces.com/contest/499/problem/C "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;平面上用n条直线，不平行与坐标轴。这些直线把平面分成多个区域，给位于区域内的两个点，问从一个点到另一个点需要穿过多少个区域。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;数学题，换一个角度，如果这两个点在一条直线的两侧，那么这条直线一定要穿过。穿过一条直线就意味着，需要多走一个区域。所以直接判断这两个点都位于哪些直线的两侧，即可。注意：数字会很大！！

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cstdio&gt;
	using namespace std;
	
	struct Node{
	    long long a,b,c;
	    Node(){a=0; b=0; c=0;}
	}p1,p2;
	int n;
	Node coeff[309];
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	    while(cin &gt;&gt; p1.a &gt;&gt; p1.b){
	        cin &gt;&gt; p2.a &gt;&gt; p2.b;
	
	        cin &gt;&gt; n;
	        for(int i=0; i&lt;n; ++i)
	            cin &gt;&gt; coeff[i].a &gt;&gt; coeff[i].b &gt;&gt; coeff[i].c;
	
	        int ans=0;
	        for(int i=0; i&lt;n; ++i){
	            long long r1 = coeff[i].a*p1.a + coeff[i].b*p1.b + coeff[i].c;
	            long long r2 = coeff[i].a*p2.a + coeff[i].b*p2.b + coeff[i].c;
	            if((r1&lt;0 &amp;&amp; r2&gt;0) || (r1&gt;0 &amp;&amp; r2&lt;0))
	                ans++;
	        }
	        cout &lt;&lt; ans &lt;&lt; endl;
	    }
	    return 0;
	}
</pre>
<br />

[D. Name That Tune][D]
[D]: http://codeforces.com/contest/499/problem/D "题目链接"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 求概率问题，对不起，我怂了放弃这题了。完全没思路，等后面在慢慢看。

大概是个dp的问题。Mark！

这里是codeforces上的题解：http://codeforces.com/blog/entry/15353
<br/>

[E. Array and Operations][E]
[E]: http://codeforces.com/contest/499/problem/E "题目链接"
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 本来以为是个数学问题，wa了一发发现错了，想得太简单了。细思急恐！ 竟然是个匹配的问题，也放弃了，以后再来解决！！！

题解上面也有。
