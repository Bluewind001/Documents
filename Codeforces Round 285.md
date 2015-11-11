转载请注明出处，谢谢：
http://blog.csdn.net/wybluewind/article/details/47818925

codeforces 上的题解：http://codeforces.com/blog/entry/15743


##[A. Contest][A]
[A]: http://codeforces.com/contest/501/problem/A "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Codeforces比赛中，Misha在c分钟过了a分的题，Vasya在d分钟过了b分的题。最终的得分的计算方法：max(3p/10, p-pt/250)[在t分钟过了p分的题];

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;简单，带入公式算一下就行，注意：不是int类型。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cstdio&gt;
	#include&lt;algorithm&gt;
	using namespace std;
	
	double a,b,c,d;
	double m,v;
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	    while(cin &gt;&gt; a &gt;&gt; b &gt;&gt; c &gt;&gt; d){
	        m = max(3*a/10,a-a*c/250);
	        v = max(3*b/10,b-b*d/250);
	        if(m&gt;v)
	            printf(&quot;Misha\n&quot;);
	        else if(v&gt;m)
	            printf(&quot;Vasya\n&quot;);
	        else printf(&quot;Tie\n&quot;);
	    }
	    return 0;
	}
</pre>
<br />

##[B. Misha and Changing Handles][B]
[B]: http://codeforces.com/contest/501/problem/B "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;改名字，只有没用过的新名字才可以改，可以改多次。找出最少改了一次的人的最开始的名字和最后改好的名字。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先判断，每一次更改能否成功，把不能修改的记录去掉「状态置为false」。并把用过的名字记录对应到他们的id，这样后面方便查找。从1开始处理，找到一个名字，看他的新名字是否有更改记录，如果有继续向下查找，直到没有修改记录。在向下查找的过程中把用过记录删掉「即把状态置为false」。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cstdio&gt;
	#include&lt;map&gt;
	#include&lt;string&gt;
	#include&lt;cstring&gt;
	#include&lt;utility&gt;
	using namespace std;
	
	int q;
	struct Node{
	    string old,news;
	    bool is;
	    Node(){old=&quot;&quot;; news=&quot;&quot;; is=true;}
	}req[1009];
	string old,news;
	
	map&lt;string, int&gt; used;
	map&lt;string, string&gt; ans;
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	    while(cin &gt;&gt; q){
	        for(int i=1; i&lt;=q; ++i){
	            cin &gt;&gt; old &gt;&gt; news;
	            req[i].old=old;
	            req[i].news=news;
	            req[i].is = true;
	        }
	        used.clear();
	        for(int i=1; i&lt;=q; ++i){
	            used[req[i].old]=i;
	            if(used.count(req[i].news)==0){
	                used[req[i].news]=1009;
	            }
	            else{
	                req[i].is=false;
	            }
	        }
	        ans.clear();
	        for(int i=1; i&lt;=q; ++i){
	            if(req[i].is){
	                news = req[i].news;
	                while(used[news]&lt;=q &amp;&amp; used[news]&gt;0 &amp;&amp; req[used[news]].is){
	                    req[used[news]].is= false;
	                    news=req[used[news]].news;
	                }
	                ans[req[i].old]=news;
	            }
	        }
	        cout &lt;&lt; ans.size() &lt;&lt; endl;
	        for(map&lt;string, string&gt;::iterator it=ans.begin(); it!=ans.end(); ++it)
	            cout &lt;&lt; it-&gt;first &lt;&lt; &quot; &quot; &lt;&lt; it-&gt;second &lt;&lt; endl;
	    }
	
	    return 0;
	}
</pre>
<br />

##[C. Misha and Forest][E]
[E]: http://codeforces.com/contest/501/problem/C "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一个无环且没有平行边的图，统计每个节点的所连边的个数和节点编号的异或(XOR)和。根据每个节点的所连边的个数和节点编号的异或和，还原图。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这个图就是树，所以从所连边数是1的节点开始入手，并把这个边从记录的信息中删除(两个点都要删除)，即：degree要减1，s要异或这个节点的值。记录一下边的信息输出就可以了。由于数据量大，不建议用c++的输入输出。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cstdio&gt;
	#include&lt;cstring&gt;
	#include&lt;cmath&gt;
	#include&lt;vector&gt;
	#include&lt;algorithm&gt;
	using namespace std;
	
	struct Node{
	    int from;
	    int deg;
	    int s;
	    Node(){from=0;deg=0; s=0;}
	    inline bool operator &lt; (const Node &amp;a) const{
	        if(deg!=a.deg)
	            return deg&lt;a.deg;
	        else return s&lt;a.s;
	    }
	}info[(1&lt;&lt;16)+9];
	int n;
	
	vector&lt;int&gt; g[(1&lt;&lt;16)+9];
	int mp[(1&lt;&lt;16)+9];
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	    while(scanf(&quot;%d&quot;, &amp;n)!=EOF){
	        for(int i=0; i&lt;n; ++i)
	            g[i].clear();
	
	        for(int i=0,deg,s; i&lt;n; ++i){
	            scanf(&quot;%d %d&quot;, °, &amp;s);
	            info[i].from = i;
	            info[i].deg = deg;
	            info[i].s = s;
	        }
	        sort(info,info+n);
	        for(int i=0; i&lt;n; ++i){
	            mp[info[i].from] = i;
	        }
	        int ans=0;
	        bool flg=true;
	        while(true){
	            flg = true;
	            for(int i=0; i&lt;n; ++i){
	                if(info[i].deg == 1){
	                    g[info[i].from].push_back(info[i].s);
	                    info[i].deg = 0;
	                    ans++;
	                    int id = mp[info[i].s];
	                    info[id].deg--;
	                    info[id].s = info[id].s ^ info[i].from;
	                    flg= false;
	                }
	            }
	            if(flg)
	                break;
	        }
	        printf(&quot;%d\n&quot;,ans);
	        for(int i=0; i&lt;n; ++i){
	            for(int j=0; j&lt;g[i].size(); ++j){
	                printf(&quot;%d %d\n&quot;,i,g[i][j]);
	            }
	        }
	    }
	    return 0;
	}
</pre>
<br />

