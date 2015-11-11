转载请注明出处，谢谢
http://blog.csdn.net/wyBluewind/article/details/47682783

codeforces 上写的题解 by  Endagorion：http://codeforces.com/blog/entry/15208


**写在前面：第一次写博客，也是第一次写题解，写的不好请各路高手指导。**


<br/>
##[A. Minimum Difficulty][A]
[A]: http://codeforces.com/contest/496/problem/A "题目链接"

题意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;简单题。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;找一下挨着的差的最大值，然后间隔为2时最大的最小即可。详细见代码。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cmath&gt;
	using namespace std;
	
	int n,d1,d2,ans;
	int a[1009];
	
	int main()
	{
		while(cin &gt;&gt; n){
			d1=d2=-1;
			for(int i=0; i&lt;n; ++i)
				cin &gt;&gt; a[i];
			for(int i=1; i&lt;n; ++i)
				d1=max(a[i]-a[i-1],d1);
			ans=100000;
			for(int i=2; i&lt;n; ++i){
				d2 = max(a[i]-a[i-2],d1);
				ans=min(ans,d2);
			}
			cout &lt;&lt; ans &lt;&lt; endl;
		}
		return 0;
	}
</pre>
<br/>

##[B. Secret Combination][B]
[B]: http://codeforces.com/contest/496/problem/B "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;有一个n位的数字组合锁，锁上有两个按钮可以改变显示的数字。第一个按钮是将n位数字每一位都加一(9 会变成0)，第二个按钮将所有位右移一位(最后一位变成第一位)。按下第一个按钮：579 会变成 680 ， 再按下第二个按钮 680 会变成 068。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;需要找到可以显示出的最小的数，前导零会被忽略。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;肯定是前导0越多数越小。所以第一位一定是0，然后找出每一位在第一位且变成0时的显示的数字大小，然后比较即可。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;string&gt;
	#include&lt;fstream&gt;
	using namespace std;
	
	int n,len;
	string s,ans,temp;
	
	int main(){
	//    ifstream cin;
	//    cin.open(&quot;in.txt&quot;);
	
	    while(cin &gt;&gt; n){
	        cin &gt;&gt; s;
	        len =s.size();
	        temp = s + s; ans=s;
	        for(int i=0; i&lt;len; ++i){
	            int t = 10-(temp[i]-'0');
	            s=&quot;&quot;;
	            for(int j=i; j&lt;i+len; ++j){
	                s += (char)(((temp[j]-'0')+t)%10 + '0');
	            }
	            if(ans&gt;s)
	                ans = s;
	        }
	        cout &lt;&lt; ans &lt;&lt; endl;
	    }
	    return 0;
	}
</pre>
<br/>

##[C. Removing Columns][C]
[C]: http://codeforces.com/contest/496/problem/C "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一个由小写英文字母组成的n×m的表格，你可以删除表格中的某一列。如果一个表格从上到下满足按字典序递增(可以相同)，则它就是一个`‘good table’`，问最少删除几列可以变成`‘good table’`

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;从简单的入手就一行行的比较，如果不满足要求就把这列标记为删除，注意这列删除了可能会影响前面比较完的结果，比如
aab
aba
aaa
第三行和第二行比较时，删除第二列之后会影响到第二行和第一行的比较结果。所以每次删除一列之后，都要从第一行重新比较。此时我们需要记录一下每一行和前一行在哪一列比较出的结果，每次从这个标记列开始比较就好了，不用每次都从第一列开始比较。最后统计一下删除的列就行了。

这个时间复杂度，因为最多有m次重新比较，每次比较的代价就是n×m的， 所以就是O(m×n×m)。[我也不知道对不对，有错误的话请告诉我，我改正，谢谢了]

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;fstream&gt;
	#include&lt;cstring&gt;
	using namespace std;
	
	int n,m;
	bool is[105];
	int flg[109];
	char grid[105][105];
	
	
	int main()
	{
	//    ifstream cin;
	//    cin.open(&quot;in.txt&quot;);
	
	    while(cin &gt;&gt; n &gt;&gt; m){
	        for(int i=0; i&lt;n; ++i){
	            for(int j=0; j&lt;m; ++j){
	                cin &gt;&gt; grid[i][j];
	            }
	        }
	        memset(is,true,sizeof(is));
	        memset(flg,0,sizeof(flg));
	
	        for(int i=1; i&lt;n; ++i){
	            for(int j=flg[i]; j&lt;m; ++j){
	                if(is[j]){
	                    if(grid[i][j] &lt; grid[i-1][j]){
	                        is[j]=false;
	                        i=0;
	                        break;
	                    }
	                    else if(grid[i][j] == grid[i-1][j]){
	                        flg[i]=j;
	                    }
	                    else{
	                        flg[i]=j;
	                        break;
	                    }
	                }
	            }
	        }
	
	        int ans=0;
	        for(int i=0; i&lt;m; ++i)
	            if(!is[i])
	                ans++;
	        cout &lt;&lt; ans &lt;&lt; endl;
	
	    }
	    return 0;
	}
</pre>
<br />

##[D. Tennis Game][D]
[D]: http://codeforces.com/contest/496/problem/D "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Petya和Gena打乒乓球，一场比赛有很多局，每局有多次发球。每赢一次发球得1分，每局先赢t分的人赢了这局，下局重新记分，先赢s局的人赢得比赛。现在有一系列记录每次发球的胜者，但是不知道t和s，需要找出满足这个记录的所有t和s。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;对于这种找满足要求的数的，我觉得就是枚举。直接枚举一定会超时，O(n^2)需要优化。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这题先枚举t，然后找满足的s，当然对于固定的t最多只有一个s与之对应。当一局结束后，向后找t个1和t个2，哪个先出现这局就是他赢了。可以利用二分查找来找t个1和t个2，这样就可以优化到O(nlogn)了（我之前用二分搜索实现的但是TLE了 >_<  ，后来用了一个机智的方法用O(1)的时间代替了二分查找）。
注意几个问题：若1和2的个数都不满足t个，那么就说明不满足要求，还有赢最后一局的人一定是最后的赢家（之前在这wa了）。

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cstring&gt;
	#include&lt;cstdio&gt;
	#include&lt;fstream&gt;
	#include&lt;utility&gt;
	#include&lt;algorithm&gt;
	#include&lt;vector&gt;
	using namespace std;
	
	const int MAXN = 1000000;
	
	int n;
	int a[100009][2], pos[100009][2];
	struct P{
	    int s;
	    int t;
	}res[100009];
	int num=0;
	bool cmp(const P &amp;a1, const P &amp;a2){
	    if(a1.s!=a2.s)
	        return a1.s&lt;a2.s;
	    else return a1.t&lt;a2.t;
	}
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	
	    while(scanf(&quot;%d&quot;,&amp;n)!=EOF){
	        memset(a,0,sizeof(a));
	        for(int i=1,t; i&lt;=n; ++i){
	            scanf(&quot;%d&quot;, &amp;t);
	            if(t==1){
	                a[i][0]=a[i-1][0]+1;
	                a[i][1]=a[i-1][1];
	                pos[a[i][0]][0]=i;
	            }
	            else{
	                a[i][1]=a[i-1][1]+1;
	                a[i][0]=a[i-1][0];
	                pos[a[i][1]][1]=i;
	            }
	        }
	
	        int a1=0,a2=0;
	        num=0;
	        for(int i=1; i&lt;=n; ++i){
	            int j=0; a1=a2=0; int last=-1;
	            while(j&lt;n){
	                if(a[j][0]+i &lt;= a[n][0] &amp;&amp; a[j][1]+i &lt;= a[n][1]){
	                    int k1 = pos[a[j][0]+i][0];
	                    int k2 = pos[a[j][1]+i][1];
	                    if(k1&lt;k2)
	                        a1++,j=k1,last=1;
	                    else if(k2&lt;k1)
	                        a2++,j=k2,last=2;
	                    else break;
	                }
	                else if(a[j][0]+i &lt;= a[n][0] &amp;&amp; a[j][1]+i &gt; a[n][1]){
	                    a1++,j=pos[a[j][0]+i][0];last=1;
	                }
	                else if(a[j][0]+i &gt; a[n][0] &amp;&amp; a[j][1]+i &lt;= a[n][1]){
	                    a2++,j=pos[a[j][1]+i][1]; last=2;
	                }
	                else
	                    break;
	            }
	            if(j==n &amp;&amp; a1!=a2){
	                if(a1&gt;a2 &amp;&amp; last==1){
	                    res[num].s=a1,res[num++].t=i;
	                }
	                if(a2&gt;a1 &amp;&amp; last==2){
	                    res[num].s=a2, res[num++].t=i;
	                }
	            }
	        }
	        sort(res,res+num,cmp);
	        int len = num;
	        printf(&quot;%d\n&quot;,len);
	        for(int i=0; i&lt;len; ++i){
	            printf(&quot;%d %d\n&quot;,res[i].s,res[i].t);
	        }
	    }
	    return 0;
	}
</pre>
<br />

##[E. Distributing Parts][E]
[E]: http://codeforces.com/contest/496/problem/E "题目链接"
题目大意：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;一个音乐播放器有m个单元，每个单元可以播放一首音乐，每个单元一个音量范围c,d，只可以播放该音量范围内的音乐，且最多可以放k首音乐，也可以不放任何音乐。现在有n首音乐，每首音乐也有个音量范围a,b，需要放到m个单元中。输出每首音乐用哪个单元播放。

思路：
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;这种一个范围需要放到另一个范围的题目，就是放到一起排序，然后处理。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;首先按照最小音量升序排序，如果相同那么单元放在前面。然后从前到后一个个处理，如果碰到单元就放到集合里，如果碰到音乐就在现在的集合中找一个最小的d，此时c一定大于a，就是我们要找的播放单元，同时k需要减1。如果单元的k为0，就从集合中删除。这个集合可以用c++中的set维护(需要了解一下set的实现方式和用到的数据结构)。复杂度O((n+m)log(n+m));

代码：
<pre name="code" class="cpp">
	#include&lt;iostream&gt;
	#include&lt;cstdio&gt;
	#include&lt;cstring&gt;
	#include&lt;algorithm&gt;
	#include&lt;set&gt;
	using namespace std;
	
	struct Node{
	    int id,beg,en,flg,k;
	    Node(){beg=0;en=0;flg=0;k=0;}
	    inline bool operator &lt; (const Node &amp;a) const {
	        if(beg != a.beg)
	            return beg&lt;a.beg;
	        else return flg&gt;a.flg;
	    }
	}all[100009*2];
	
	bool cmp1(const Node &amp;a, const Node &amp;b){
	    if(a.beg != b.beg)
	        return a.beg&lt;b.beg;
	    else return a.flg&gt;b.flg;
	}
	
	struct cmp2{
	    bool operator ()(const Node &amp;a, const Node &amp;b){
	        return a.en&lt;b.en;
	    }
	};
	
	multiset&lt;Node, cmp2&gt; sets;
	multiset&lt;Node, cmp2&gt;::iterator it;
	
	int n,m;
	int ans[100009];
	int used[100009];
	
	int main()
	{
	//    freopen(&quot;in.txt&quot;,&quot;r&quot;,stdin);
	    while(cin &gt;&gt; n ){
	        for(int i=1,s,e; i&lt;=n; ++i){
	            Node temp;
	            cin &gt;&gt; s &gt;&gt; e;
	            temp.beg = s;
	            temp.en = e;
	            temp.flg = 0;
	            temp.id = i;
	            all[i] = temp;
	        }
	        cin &gt;&gt; m;
	        for(int i=1,s,e,k; i&lt;=m; ++i){
	            Node temp;
	            cin &gt;&gt; s &gt;&gt; e &gt;&gt; k;
	            temp.beg = s;
	            temp.en = e;
	            temp.flg = 1;
	            temp.k = k;
	            temp.id = i;
	            all[i+n] = temp;
	        }
	        sort(all+1, all+1+n+m, cmp1);
	
	        bool flgs = true;
	        memset(used,0,sizeof(used));
	        memset(ans,0,sizeof(ans));
	        for(int i=1; i&lt;=n+m; ++i){
	            if(all[i].flg==1){
	                sets.insert(all[i]);
	            }
	            else{
	                it = sets.lower_bound(all[i]);
	                if(it != sets.end()){
	                    ans[all[i].id] = it-&gt;id;
	                    used[it-&gt;id]++;
	                    if(it-&gt;k == used[it-&gt;id] ){
	                        sets.erase(it);
	                    }
	                }
	                else{
	                    flgs=false;
	                    break;
	                }
	            }
	        }
	        if(flgs){
	            printf(&quot;YES\n%d&quot;, ans[1]);
	            for(int i=2; i&lt;=n; ++i)
	                printf(&quot; %d&quot;,ans[i]);
	            printf(&quot;\n&quot;);
	        }
	        else printf(&quot;NO\n&quot;);
	    }
	    return 0;
	}
</pre>
<br />
