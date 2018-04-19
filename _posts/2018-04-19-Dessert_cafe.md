---
title:  "Dessert cafe - SW Expert Academy"
categories: 
  - study
  - SW Expert Academy
---
<div style="font-family: 'Lucida Grande', 'Segoe UI', 'Apple SD Gothic Neo', 'Malgun Gothic', 'Lucida Sans Unicode', Helvetica, Arial, sans-serif; font-size: 0.9em; overflow-x: hidden; overflow-y: auto; margin: 0px !important; padding: 5px 20px 26px !important; background-color: rgb(255, 255, 255);font-family: 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; padding: 20px;padding: 20px; color: rgb(34, 34, 34); font-size: 15px; font-family: 'Roboto Condensed', Tauri, 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; line-height: 1.6; -webkit-font-smoothing: antialiased; background: rgb(255, 255, 255);"><h3 id="디저트-카페" style="clear: both;font-size: 1.6em; font-weight: bold; margin: 1.125em 0px 0.75em;margin-top: 0px;"><a name="디저트-카페" href="#디저트-카페" style="text-decoration: none; vertical-align: baseline;color: rgb(50, 105, 160);"></a>디저트 카페</h3><p style="margin-top: 0px;margin: 1em 0px; word-wrap: break-word;">SW Expert Academy 2105 문제<br style="clear: both;">-링크<br style="clear: both;"><a href="https://www.swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5VwAr6APYDFAWu&amp;categoryId=AV5VwAr6APYDFAWu&amp;categoryType=CODE" style="text-decoration: none; vertical-align: baseline;color: rgb(50, 105, 160);">https://www.swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5VwAr6APYDFAWu&amp;categoryId=AV5VwAr6APYDFAWu&amp;categoryType=CODE</a></p><pre style="border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); overflow: auto; padding: 0.5em;display: block; overflow-x: auto; padding: 0.5em; color: rgb(101, 123, 131); background: rgb(253, 246, 227);"><code class="cpp" data-origin="<pre><code class=&quot;cpp&quot;>#include &amp;lt;iostream&amp;gt;
#include &amp;lt;stdio.h&amp;gt;
#include &amp;lt;string.h&amp;gt;


using namespace std;
int map[21][21];
int value[101] = {0};
int visit[21][21] = {0};
int N;
int px, py , max_l;

struct Go{
    int x=0;
    int y=0;
};
Go go[4];

//0-&amp;gt; 좌하 , 1-&amp;gt; 좌하,우하 , 2-&amp;gt; 우하,우상 , 3-&amp;gt; 우상,좌상,4-&amp;gt;좌상

void dfs(int y, int x, int sta, int length){
    int next_y,next_x;
   // printf(&quot;%d %d ---&amp;gt; %d , sta:%d\n&quot;,y,x,length,sta);


    value[map[y][x]] = 1;
    visit[y][x] = 1;
    if((y==py)&amp;amp;&amp;amp;(x==px)&amp;amp;&amp;amp;(length&amp;gt;3)){
        max_l = max(max_l,length);
       // printf(&quot;now -&amp;gt; %d max -&amp;gt; %d\n&quot;,length, max_l);
        value[map[y][x]] = 0;
        visit[y][x] = 0;
        return;

    }


    //범위 , 이미 방문한 곳인지 , 똑같은 번호인지
    for(int i=0;i&amp;lt;2;i++){
        next_y = y+go[sta+i].y;
        next_x = x+go[sta+i].x;
        if(sta+i&amp;gt;3)
            continue;
        if(next_y&amp;lt;py)
            continue;

        if((next_y&amp;gt;=0)&amp;amp;&amp;amp;(next_y&amp;lt;N)&amp;amp;&amp;amp;(next_x&amp;gt;=0)&amp;amp;&amp;amp;(next_x&amp;lt;N)){
            int v = map[next_y][next_x];
            if(sta+i==3){
                if((next_y==py)&amp;amp;&amp;amp;(next_x==px)){
                    max_l = max(max_l,length+1);
                    // printf(&quot;now -&amp;gt; %d max -&amp;gt; %d\n&quot;,length+1, max_l);
                    value[map[y][x]] = 0;
                    visit[y][x] = 0;
                    return;
                }else{
                    if((visit[next_y][next_x]==0)&amp;amp;&amp;amp;(value[v]==0)){
                        dfs(next_y,next_x,sta+i,length+1);

                    }

                }
            }else if((visit[next_y][next_x]==0)&amp;amp;&amp;amp;(value[v]==0)){
                dfs(next_y,next_x,sta+i,length+1);
            }


        }
    }
    value[map[y][x]] = 0;
    visit[y][x] = 0;

}


int main()
{
    freopen(&quot;input.txt&quot;,&quot;r&quot;,stdin);
    freopen(&quot;out.txt&quot;,&quot;w&quot;,stdout);

    go[0].x=-1;
    go[0].y=1;
    go[1].x=1;
    go[1].y=1;
    go[2].x=1;
    go[2].y=-1;
    go[3].x=-1;
    go[3].y=-1;

    int t = 0;
    scanf(&quot;%d&quot;,&amp;amp;t);

    for(int test_case = 0; test_case&amp;lt;t; test_case++){


        memset(map,0,sizeof(map));
        memset(value,0,sizeof(value));
        max_l = 0;
        scanf(&quot;%d&quot;,&amp;amp;N);
        for(int i=0;i&amp;lt;N;i++){
            for(int j=0;j&amp;lt;N;j++){
                scanf(&quot;%d&quot;,&amp;amp;map[i][j]);
            }
        }

        for(int i=0;i&amp;lt;N;i++){
            for(int j=0;j&amp;lt;N;j++){
                py = i;
                px = j;
                dfs(i,j,0 , 0);
            }
        }
        if(max_l==0)
            max_l = -1;
        printf(&quot;#%d %d\n&quot;,test_case+1,max_l);

    }
    fclose(stdin);
    fclose(stdout);
    return 0;
}
</code></pre>" style="border: 0px; display: block;font-family: Consolas, Inconsolata, Courier, monospace; font-weight: bold; white-space: pre; margin: 0px;border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); padding: 0px 5px; margin: 0px 2px;font-size: 1em; letter-spacing: -1px; font-weight: bold;"><span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;iostream&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;stdio.h&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;string.h&gt;</span>


<span class="hljs-keyword" style="color: rgb(133, 153, 0);">using</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">namespace</span> <span class="hljs-built_in" style="color: rgb(38, 139, 210);">std</span>;
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> <span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>[<span class="hljs-number" style="color: rgb(42, 161, 152);">21</span>][<span class="hljs-number" style="color: rgb(42, 161, 152);">21</span>];
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> value[<span class="hljs-number" style="color: rgb(42, 161, 152);">101</span>] = {<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>};
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> visit[<span class="hljs-number" style="color: rgb(42, 161, 152);">21</span>][<span class="hljs-number" style="color: rgb(42, 161, 152);">21</span>] = {<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>};
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> N;
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> px, py , max_l;

<span class="hljs-keyword" style="color: rgb(133, 153, 0);">struct</span> Go{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> x=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> y=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
};
Go go[<span class="hljs-number" style="color: rgb(42, 161, 152);">4</span>];

<span class="hljs-comment" style="color: rgb(147, 161, 161);">//0-&gt; 좌하 , 1-&gt; 좌하,우하 , 2-&gt; 우하,우상 , 3-&gt; 우상,좌상,4-&gt;좌상</span>

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">dfs</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> y, <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> x, <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> sta, <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> length)</span></span>{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> next_y,next_x;
   <span class="hljs-comment" style="color: rgb(147, 161, 161);">// printf("%d %d ---&gt; %d , sta:%d\n",y,x,length,sta);</span>


    value[<span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>[y][x]] = <span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    visit[y][x] = <span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>((y==py)&amp;&amp;(x==px)&amp;&amp;(length&gt;<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>)){
        max_l = max(max_l,length);
       <span class="hljs-comment" style="color: rgb(147, 161, 161);">// printf("now -&gt; %d max -&gt; %d\n",length, max_l);</span>
        value[<span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>[y][x]] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
        visit[y][x] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span>;

    }


    <span class="hljs-comment" style="color: rgb(147, 161, 161);">//범위 , 이미 방문한 곳인지 , 똑같은 번호인지</span>
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;<span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>;i++){
        next_y = y+go[sta+i].y;
        next_x = x+go[sta+i].x;
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(sta+i&gt;<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>)
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">continue</span>;
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(next_y&lt;py)
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">continue</span>;

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>((next_y&gt;=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>)&amp;&amp;(next_y&lt;N)&amp;&amp;(next_x&gt;=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>)&amp;&amp;(next_x&lt;N)){
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> v = <span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>[next_y][next_x];
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(sta+i==<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>){
                <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>((next_y==py)&amp;&amp;(next_x==px)){
                    max_l = max(max_l,length+<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>);
                    <span class="hljs-comment" style="color: rgb(147, 161, 161);">// printf("now -&gt; %d max -&gt; %d\n",length+1, max_l);</span>
                    value[<span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>[y][x]] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
                    visit[y][x] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
                    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span>;
                }<span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span>{
                    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>((visit[next_y][next_x]==<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>)&amp;&amp;(value[v]==<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>)){
                        dfs(next_y,next_x,sta+i,length+<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>);

                    }

                }
            }<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">if</span><span class="hljs-params">((visit[next_y][next_x]==0)</span>&amp;&amp;<span class="hljs-params">(value[v]==0)</span>)</span>{
                dfs(next_y,next_x,sta+i,length+<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>);
            }


        }
    }
    value[<span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>[y][x]] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    visit[y][x] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;

}


<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">main</span><span class="hljs-params">()</span>
</span>{
    freopen(<span class="hljs-string" style="color: rgb(42, 161, 152);">"input.txt"</span>,<span class="hljs-string" style="color: rgb(42, 161, 152);">"r"</span>,stdin);
    freopen(<span class="hljs-string" style="color: rgb(42, 161, 152);">"out.txt"</span>,<span class="hljs-string" style="color: rgb(42, 161, 152);">"w"</span>,stdout);

    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>].x=-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>].y=<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>].x=<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>].y=<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>].x=<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>].y=-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>].x=-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
    go[<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>].y=-<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> t = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-built_in" style="color: rgb(38, 139, 210);">scanf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d"</span>,&amp;t);

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> test_case = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; test_case&lt;t; test_case++){


        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">memset</span>(<span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>,<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>,<span class="hljs-keyword" style="color: rgb(133, 153, 0);">sizeof</span>(<span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>));
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">memset</span>(value,<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>,<span class="hljs-keyword" style="color: rgb(133, 153, 0);">sizeof</span>(value));
        max_l = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">scanf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d"</span>,&amp;N);
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;N;i++){
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> j=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;j&lt;N;j++){
                <span class="hljs-built_in" style="color: rgb(38, 139, 210);">scanf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d"</span>,&amp;<span class="hljs-built_in" style="color: rgb(38, 139, 210);">map</span>[i][j]);
            }
        }

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;N;i++){
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> j=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;j&lt;N;j++){
                py = i;
                px = j;
                dfs(i,j,<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span> , <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>);
            }
        }
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(max_l==<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>)
            max_l = -<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"#%d %d\n"</span>,test_case+<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>,max_l);

    }
    fclose(stdin);
    fclose(stdout);
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
}
</code></pre><p style="margin: 1em 0px; word-wrap: break-word;">다음에 이동할 방향을 status로 나누어서 해결<br style="clear: both;">탐색 안하는 점을 걸러내면 더 시간을 줄일수 있을 듯</p><p style="margin: 1em 0px; word-wrap: break-word;">return을 중간에 해줘서 더 탐색 해야 하는 곳을 탐색 안하고<br style="clear: both;">종료하는 문제가 있었음<br style="clear: both;">—&gt; 탐색 중간이 아니라 마지막 점에 도착하였을 시에 return을 하도록 해주자</p></div>
