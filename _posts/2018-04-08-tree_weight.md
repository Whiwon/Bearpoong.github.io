---
title:  "트리의 가중치"
categories: 
  - study
---

<div style="font-family: 'Lucida Grande', 'Segoe UI', 'Apple SD Gothic Neo', 'Malgun Gothic', 'Lucida Sans Unicode', Helvetica, Arial, sans-serif; font-size: 0.9em; overflow-x: hidden; overflow-y: auto; margin: 0px !important; padding: 5px 20px 26px !important; background-color: rgb(255, 255, 255);font-family: 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; padding: 20px;padding: 20px; color: rgb(34, 34, 34); font-size: 15px; font-family: 'Roboto Condensed', Tauri, 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; line-height: 1.6; -webkit-font-smoothing: antialiased; background: rgb(255, 255, 255);"><h3 id="트리의-가중치" style="clear: both;font-size: 1.6em; font-weight: bold; margin: 1.125em 0px 0.75em;margin-top: 0px;"><a name="트리의-가중치" href="#트리의-가중치" style="text-decoration: none; vertical-align: baseline;color: rgb(50, 105, 160);"></a>트리의 가중치</h3><p style="margin-top: 0px;margin: 1em 0px; word-wrap: break-word;">백준의 1289번 문제</p><p style="margin: 1em 0px; word-wrap: break-word;">자식 - 부모<br style="clear: both;">자식 - 부모 -자식의 경우를 생각해야 한다</p><pre style="border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); overflow: auto; padding: 0.5em;display: block; overflow-x: auto; padding: 0.5em; color: rgb(101, 123, 131); background: rgb(253, 246, 227);"><code class="cpp" data-origin="<pre><code class=&quot;cpp&quot;>#include &amp;lt;iostream&amp;gt;
#include &amp;lt;string&amp;gt;
#include &amp;lt;cstdlib&amp;gt;
#include &amp;lt;stdio.h&amp;gt;
#include &amp;lt;string.h&amp;gt;
#include &amp;lt;algorithm&amp;gt;
#include &amp;lt;vector&amp;gt;


using namespace std;

#define MAX_SIZE 100000
#define mod 1000000007

struct Node{
    int num = 0;
    int weight = 0;
};
vector&amp;lt;Node&amp;gt; node[100001];
int result;
int dfs(int v, int p){

    int sum=1;
    int total;
    for(int i=0;i&amp;lt;node[v].size();i++){
        if(node[v][i].num==p)       //부모랑 연결된건 다시 체크 안하도록
            continue;

        //자식을 부모로 하는 노드 다 구하고 자식에서 현재 부모로 연결되는 가중치 곱함
        total =(long long)dfs(node[v][i].num,v)*node[v][i].weight%mod;


        //이전까지의 자식 애들 * 새로운 자식 가중치
        result = (result + (long long)total*sum)%mod;

        //돌면서 자식애들 다 더함 자식-부모-자식 생각
        //처음에 +1은 자식-부모 로 끝나는 경우 
        sum = (sum + total)%mod;

        cout&amp;lt;&amp;lt;node[v][i].num&amp;lt;&amp;lt;&quot;/&quot;&amp;lt;&amp;lt;p&amp;lt;&amp;lt;&quot;////&quot;;
        printf(&quot;%ld / %ld / %ld \n&quot;,total,result,sum);

    }
    return sum;

}

int main(){

    int N;
    cin&amp;gt;&amp;gt;N;
    for(int test_case = 0;test_case&amp;lt;N-1;test_case++){
        int A,B,W;
        Node temp_node;
        cin&amp;gt;&amp;gt;A&amp;gt;&amp;gt;B&amp;gt;&amp;gt;W;
        temp_node.num = B;
        temp_node.weight = W;
        node[A].push_back(temp_node);
        temp_node.num = A;
        node[B].push_back(temp_node);

    }
    dfs(1,-1);
    cout&amp;lt;&amp;lt;result;

    return 0;
}
</code></pre>" style="border: 0px; display: block;font-family: Consolas, Inconsolata, Courier, monospace; font-weight: bold; white-space: pre; margin: 0px;border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); padding: 0px 5px; margin: 0px 2px;font-size: 1em; letter-spacing: -1px; font-weight: bold;"><span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;iostream&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;string&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;cstdlib&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;stdio.h&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;string.h&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;algorithm&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;vector&gt;</span>


<span class="hljs-keyword" style="color: rgb(133, 153, 0);">using</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">namespace</span> <span class="hljs-built_in" style="color: rgb(38, 139, 210);">std</span>;

<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">define</span> MAX_SIZE 100000</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">define</span> mod 1000000007</span>

<span class="hljs-keyword" style="color: rgb(133, 153, 0);">struct</span> Node{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> num = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> weight = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
};
<span class="hljs-built_in" style="color: rgb(38, 139, 210);">vector</span>&lt;Node&gt; node[<span class="hljs-number" style="color: rgb(42, 161, 152);">100001</span>];
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> result;
<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">dfs</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> v, <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> p)</span></span>{

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> sum=<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> total;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;node[v].size();i++){
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(node[v][i].num==p)       <span class="hljs-comment" style="color: rgb(147, 161, 161);">//부모랑 연결된건 다시 체크 안하도록</span>
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">continue</span>;

        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//자식을 부모로 하는 노드 다 구하고 자식에서 현재 부모로 연결되는 가중치 곱함</span>
        total =(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">long</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">long</span>)dfs(node[v][i].num,v)*node[v][i].weight%mod;


        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//이전까지의 자식 애들 * 새로운 자식 가중치</span>
        result = (result + (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">long</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">long</span>)total*sum)%mod;

        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//돌면서 자식애들 다 더함 자식-부모-자식 생각</span>
        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//처음에 +1은 자식-부모 로 끝나는 경우 </span>
        sum = (sum + total)%mod;

        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">cout</span>&lt;&lt;node[v][i].num&lt;&lt;<span class="hljs-string" style="color: rgb(42, 161, 152);">"/"</span>&lt;&lt;p&lt;&lt;<span class="hljs-string" style="color: rgb(42, 161, 152);">"////"</span>;
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%ld / %ld / %ld \n"</span>,total,result,sum);

    }
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> sum;

}

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">main</span><span class="hljs-params">()</span></span>{

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> N;
    <span class="hljs-built_in" style="color: rgb(38, 139, 210);">cin</span>&gt;&gt;N;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> test_case = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;test_case&lt;N-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;test_case++){
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> A,B,W;
        Node temp_node;
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">cin</span>&gt;&gt;A&gt;&gt;B&gt;&gt;W;
        temp_node.num = B;
        temp_node.weight = W;
        node[A].push_back(temp_node);
        temp_node.num = A;
        node[B].push_back(temp_node);

    }
    dfs(<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>,-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>);
    <span class="hljs-built_in" style="color: rgb(38, 139, 210);">cout</span>&lt;&lt;result;

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
}
</code></pre><p style="margin: 1em 0px; word-wrap: break-word;">구조체 Node를 벡터를 이용하여 구현하였다<br style="clear: both;">pair로도 구현이 가능한데 이쪽이 조금 더 편한 느낌<br style="clear: both;">초기에 데이터를 저장할때 Node를 생성한 뒤 넣어야 한다</p></div>
