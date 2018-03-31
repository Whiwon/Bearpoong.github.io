---
title:  "숫자야구"
categories: 
  - study
---

<div style="font-family: 'Lucida Grande', 'Segoe UI', 'Apple SD Gothic Neo', 'Malgun Gothic', 'Lucida Sans Unicode', Helvetica, Arial, sans-serif; font-size: 0.9em; overflow-x: hidden; overflow-y: auto; margin: 0px !important; padding: 5px 20px 26px !important; background-color: rgb(255, 255, 255);font-family: 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; padding: 20px;padding: 20px; color: rgb(34, 34, 34); font-size: 15px; font-family: 'Roboto Condensed', Tauri, 'Hiragino Sans GB', 'Microsoft YaHei', STHeiti, SimSun, 'Lucida Grande', 'Lucida Sans Unicode', 'Lucida Sans', 'Segoe UI', AppleSDGothicNeo-Medium, 'Malgun Gothic', Verdana, Tahoma, sans-serif; line-height: 1.6; -webkit-font-smoothing: antialiased; background: rgb(255, 255, 255);"><h2 id="숫자야구" style="clear: both;font-size: 1.8em; font-weight: bold; margin: 1.275em 0px 0.85em;margin-top: 0px;border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: rgb(230, 230, 230);"><a name="숫자야구" href="#숫자야구" style="text-decoration: none; vertical-align: baseline;color: rgb(50, 105, 160);"></a>숫자야구</h2><p style="margin-top: 0px;margin: 1em 0px; word-wrap: break-word;">중복되지 않은 4자리 수를 설정해 놓으면<br style="clear: both;">컴퓨터가 해당 숫자를 예측하는 프로그램<br style="clear: both;">영어로 Bulls and Cows라고도 한다</p><p style="margin: 1em 0px; word-wrap: break-word;">query(설정해 놓은 숫자와 비교해 스트라이크, 볼을 유추하는 함수)를<br style="clear: both;">적게 사용할수록 좋다.</p><p style="margin: 1em 0px; word-wrap: break-word;"><strong>초기 주어진 코드</strong></p><pre style="border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); overflow: auto; padding: 0.5em;display: block; overflow-x: auto; padding: 0.5em; color: rgb(101, 123, 131); background: rgb(253, 246, 227);"><code class="cpp" data-origin="<pre><code class=&quot;cpp&quot;>#define _CRT_SECURE_NO_WARNINGS

#include &amp;lt;stdio.h&amp;gt;
#include &amp;lt;ctime&amp;gt;
#include &amp;lt;cstdlib&amp;gt;

#define N              4
#define MAX_QUERYCOUNT 1000000

static int digits[N];
static int digits_c[10];
int digits2[N];
int digits_c2[10];

static int T;

extern void doUserImplementation(int guess[]);

static int querycount;

// the value of limit_query will be changed in evaluation
static const int limit_query = 2520;

typedef struct {
    int strike;
    int ball;
} Result;

typedef struct{
    int first;
    int second;
    int third;
    int forth;
    bool ok;
}Pool;

static bool isValid(int guess[]) {
    int guess_c[10];

    for (int count = 0; count &amp;lt; 10; ++count) guess_c[count] = 0;
    for (int idx = 0; idx &amp;lt; N; ++idx) {
        if (guess[idx] &amp;lt; 0 || guess[idx] &amp;gt;= 10 || guess_c[guess[idx]] &amp;gt; 0) return false;
        guess_c[guess[idx]]++;
    }
    return true;
}

// API : return a result for comparison with digits[] and guess[]
Result query(int guess[]) {
    Result result;

    if (querycount &amp;gt;= MAX_QUERYCOUNT) {
        result.strike = -1;
        result.ball = -1;
        return result;
    }

    querycount++;

    if (!isValid(guess)) {
        result.strike = -1;
        result.ball = -1;
        return result;
    }

    result.strike = 0;
    result.ball = 0;

    for (int idx = 0; idx &amp;lt; N; ++idx)
        if (guess[idx] == digits[idx])
            result.strike++;
        else if (digits_c[guess[idx]] &amp;gt; 0)
            result.ball++;


    return result;
}



static void initialize() {      //get number in digits
    for (int count = 0; count &amp;lt; 10; ++count) digits_c[count] = 0;
    for (int idx = 0; idx &amp;lt; N; ++idx) {
        char c;
        do scanf(&quot;%c&quot;, &amp;amp;c); while (c &amp;lt; '0' || c &amp;gt; '9');
        digits[idx] = c - '0';
        digits_c[digits[idx]]++;        //how many in each number
    }

    querycount = 0;
}

static bool check(int guess[]) {        //if guess is not same with digits
    for (int idx = 0; idx &amp;lt; N; ++idx)
        if (guess[idx] != digits[idx]) return false;
    return true;
}

int main() {
    int total_score = 0;
    int total_querycount = 0;;

    // freopen(&quot;sample_input.txt&quot;, &quot;r&quot;, stdin);
    setbuf(stdout, NULL);

    scanf(&quot;%d&quot;, &amp;amp;T);

    for (int testcase = 1; testcase &amp;lt;= T; ++testcase) {
        initialize();

        int guess[N];

        doUserImplementation(guess);        //have to update quess


        if (!check(guess)) querycount = MAX_QUERYCOUNT; // if check is false, update querycount = 100000000

        if (querycount &amp;lt;= limit_query) total_score++;   // limit = 2520 (not max count) score ++;

        printf(&quot;#%d %d\n&quot;, testcase, querycount);

        total_querycount += querycount;
    }
    if (total_querycount &amp;gt; MAX_QUERYCOUNT) total_querycount = MAX_QUERYCOUNT;
    printf(&quot;total score = %d\ntotal query = %d\n&quot;, total_score * 100 / T, total_querycount);
    return 0;
}

void doUserImplementation(int guess[]) {


}
</code></pre>" style="border: 0px; display: block;font-family: Consolas, Inconsolata, Courier, monospace; font-weight: bold; white-space: pre; margin: 0px;border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); padding: 0px 5px; margin: 0px 2px;font-size: 1em; letter-spacing: -1px; font-weight: bold;"><span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">define</span> _CRT_SECURE_NO_WARNINGS</span>

<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;stdio.h&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;ctime&gt;</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">include</span> &lt;cstdlib&gt;</span>

<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">define</span> N              4</span>
<span class="hljs-preprocessor" style="color: rgb(203, 75, 22);">#<span class="hljs-keyword" style="color: rgb(133, 153, 0);color: rgb(203, 75, 22);">define</span> MAX_QUERYCOUNT 1000000</span>

<span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> digits[N];
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> digits_c[<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>];
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> digits2[N];
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> digits_c2[<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>];

<span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> T;

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">extern</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">doUserImplementation</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess[])</span></span>;

<span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> querycount;

<span class="hljs-comment" style="color: rgb(147, 161, 161);">// the value of limit_query will be changed in evaluation</span>
<span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">const</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> limit_query = <span class="hljs-number" style="color: rgb(42, 161, 152);">2520</span>;

<span class="hljs-keyword" style="color: rgb(133, 153, 0);">typedef</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">struct</span> {
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> strike;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> ball;
} Result;

<span class="hljs-keyword" style="color: rgb(133, 153, 0);">typedef</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">struct</span>{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> first;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> second;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> third;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> forth;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">bool</span> ok;
}Pool;

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">bool</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">isValid</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess[])</span> </span>{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess_c[<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>];

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> count = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; count &lt; <span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>; ++count) guess_c[count] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> idx = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; idx &lt; N; ++idx) {
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (guess[idx] &lt; <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span> || guess[idx] &gt;= <span class="hljs-number" style="color: rgb(42, 161, 152);">10</span> || guess_c[guess[idx]] &gt; <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>) <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">false</span>;
        guess_c[guess[idx]]++;
    }
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">true</span>;
}

<span class="hljs-comment" style="color: rgb(147, 161, 161);">// API : return a result for comparison with digits[] and guess[]</span>
<span class="hljs-function">Result <span class="hljs-title" style="color: rgb(38, 139, 210);">query</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess[])</span> </span>{
    Result result;

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (querycount &gt;= MAX_QUERYCOUNT) {
        result.strike = -<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
        result.ball = -<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> result;
    }

    querycount++;

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (!isValid(guess)) {
        result.strike = -<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
        result.ball = -<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>;
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> result;
    }

    result.strike = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    result.ball = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> idx = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; idx &lt; N; ++idx)
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (guess[idx] == digits[idx])
            result.strike++;
        <span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">if</span> <span class="hljs-params">(digits_c[guess[idx]] &gt; 0)</span>
            result.ball++</span>;


    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> result;
}



<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">initialize</span><span class="hljs-params">()</span> </span>{      <span class="hljs-comment" style="color: rgb(147, 161, 161);">//get number in digits</span>
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> count = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; count &lt; <span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>; ++count) digits_c[count] = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> idx = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; idx &lt; N; ++idx) {
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">char</span> c;
        <span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">do</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">scanf</span><span class="hljs-params">("%c", &amp;c)</span></span>; <span class="hljs-keyword" style="color: rgb(133, 153, 0);">while</span> (c &lt; <span class="hljs-string" style="color: rgb(42, 161, 152);">'0'</span> || c &gt; <span class="hljs-string" style="color: rgb(42, 161, 152);">'9'</span>);
        digits[idx] = c - <span class="hljs-string" style="color: rgb(42, 161, 152);">'0'</span>;
        digits_c[digits[idx]]++;        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//how many in each number</span>
    }

    querycount = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
}

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">static</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">bool</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">check</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess[])</span> </span>{        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//if guess is not same with digits</span>
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> idx = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; idx &lt; N; ++idx)
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (guess[idx] != digits[idx]) <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">false</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">true</span>;
}

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">main</span><span class="hljs-params">()</span> </span>{
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> total_score = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> total_querycount = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;;

    <span class="hljs-comment" style="color: rgb(147, 161, 161);">// freopen("sample_input.txt", "r", stdin);</span>
    setbuf(stdout, NULL);

    <span class="hljs-built_in" style="color: rgb(38, 139, 210);">scanf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d"</span>, &amp;T);

    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> testcase = <span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>; testcase &lt;= T; ++testcase) {
        initialize();

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess[N];

        doUserImplementation(guess);        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//have to update quess</span>


        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (!check(guess)) querycount = MAX_QUERYCOUNT; <span class="hljs-comment" style="color: rgb(147, 161, 161);">// if check is false, update querycount = 100000000</span>

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (querycount &lt;= limit_query) total_score++;   <span class="hljs-comment" style="color: rgb(147, 161, 161);">// limit = 2520 (not max count) score ++;</span>

        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"#%d %d\n"</span>, testcase, querycount);

        total_querycount += querycount;
    }
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span> (total_querycount &gt; MAX_QUERYCOUNT) total_querycount = MAX_QUERYCOUNT;
    <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"total score = %d\ntotal query = %d\n"</span>, total_score * <span class="hljs-number" style="color: rgb(42, 161, 152);">100</span> / T, total_querycount);
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span> <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
}

<span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">doUserImplementation</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess[])</span> </span>{


}
</code></pre><p style="margin: 1em 0px; word-wrap: break-word;">여기에서 doUserImplementation() 함수를 설정</p><p style="margin: 1em 0px; word-wrap: break-word;">-구조체를 이용하여 중복되지 않는 4자리 수 1234~9876까지의 숫자를 저장<br style="clear: both;">-랜덤한 숫자와 query()를 해서 strike,ball 유추<br style="clear: both;">-위에서 query()한 숫자와 같은 결과가 나오는 숫자만 남긴다 -&gt; 위의 숫자만 알고 있기 때문(원 숫자는 모름)<br style="clear: both;">-해당 작업을 반복하여 숫자를 유추</p><pre style="border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); overflow: auto; padding: 0.5em;display: block; overflow-x: auto; padding: 0.5em; color: rgb(101, 123, 131); background: rgb(253, 246, 227);"><code class="cpp" data-origin="<pre><code class=&quot;cpp&quot;>void doUserImplementation(int guess[]) {



    Pool pool[6000];
    int k=0;
    for(int i=123;i&amp;lt;9999;i++){

        int a,b,c,d,t;

        if(i&amp;lt;1000){
            t = i;
            d=t%10;
            t=t/10;
            c=t%10;
            t=t/10;
            b=t%10;
            a=0;

            if((a!=b)&amp;amp;&amp;amp;(a!=c)&amp;amp;&amp;amp;(a!=d)&amp;amp;&amp;amp;(b!=c)&amp;amp;&amp;amp;(b!=d)&amp;amp;&amp;amp;(c!=d)){
                pool[k].first=a;
                pool[k].second=b;
                pool[k].third=c;
                pool[k].forth=d;
                pool[k].ok=true;
                k++;
            }else{
                pool[k].ok=false;
            }

        }else{
            t = i;
            d=t%10;
            t=t/10;
            c=t%10;
            t=t/10;
            b=t%10;
            t=t/10;
            a=t%10;

            if((a!=b)&amp;amp;&amp;amp;(a!=c)&amp;amp;&amp;amp;(a!=d)&amp;amp;&amp;amp;(b!=c)&amp;amp;&amp;amp;(b!=d)&amp;amp;&amp;amp;(c!=d)){
                pool[k].first=a;
                pool[k].second=b;
                pool[k].third=c;
                pool[k].forth=d;
                pool[k].ok=true;
                k++;
            }else{
                pool[k].ok=false;
            }
        }
    }


    srand((unsigned int)time(NULL));
    for(int i=0;i&amp;lt;N;i++){
        int t = 0;
        t = rand() % 10;

        for(int k=0;k&amp;lt;i;k++){
            if(t == guess[k])
                t=999;
        }
        if(t&amp;lt;10){
            guess[i]=t;
        }else{
            i--;
        }
    }
    printf(&quot;First random : &quot;);
    for(int i=0;i&amp;lt;N;i++)
        printf(&quot;%d&quot;,guess[i]);
    printf(&quot;\n&quot;);


    int pool_guess[N];


    int tt=0;
    int s,b=0;
    while(tt&amp;lt;20){
        tt++;
        Result check_1,check_2;

        check_1 = query(guess);
        printf(&quot;%d%d%d%d\n&quot;,guess[0],guess[1],guess[2],guess[3]);
        printf(&quot;b : %d / s : %d\n&quot;,check_1.ball,check_1.strike);

        if(check_1.strike==4){
            return;
        }

        for(int i=0;i&amp;lt;10;i++){
           digits_c2[i]=0;

        }
        for (int idx = 0; idx &amp;lt; N; ++idx) {

            digits2[idx] = guess[idx];
            digits_c2[digits2[idx]]++;        //how many in each number
        }


        for(int i=0;i&amp;lt;sizeof(pool)/sizeof(Pool);i++){
            if(pool[i].ok==true){
                pool_guess[0]=pool[i].first;
                pool_guess[1]=pool[i].second;
                pool_guess[2]=pool[i].third;
                pool_guess[3]=pool[i].forth;

                check_2 = query2(pool_guess);


                if((check_1.ball==check_2.ball)&amp;amp;&amp;amp;(check_1.strike==check_2.strike)){
                    pool[i].ok=true;
                }else{
                    pool[i].ok=false;
                }
            }
        }

        for(int i=0;i&amp;lt;sizeof(pool)/sizeof(Pool);i++){

            if(pool[i].ok==true){

                guess[0]=pool[i].first;
                guess[1]=pool[i].second;
                guess[2]=pool[i].third;
                guess[3]=pool[i].forth;


                break;
            }
        }
    }
}
</code></pre>" style="border: 0px; display: block;font-family: Consolas, Inconsolata, Courier, monospace; font-weight: bold; white-space: pre; margin: 0px;border-top-left-radius: 3px; border-top-right-radius: 3px; border-bottom-right-radius: 3px; border-bottom-left-radius: 3px; word-wrap: break-word; border: 1px solid rgb(204, 204, 204); padding: 0px 5px; margin: 0px 2px;font-size: 1em; letter-spacing: -1px; font-weight: bold;"><span class="hljs-function"><span class="hljs-keyword" style="color: rgb(133, 153, 0);">void</span> <span class="hljs-title" style="color: rgb(38, 139, 210);">doUserImplementation</span><span class="hljs-params">(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> guess[])</span> </span>{



    Pool pool[<span class="hljs-number" style="color: rgb(42, 161, 152);">6000</span>];
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> k=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">123</span>;i&lt;<span class="hljs-number" style="color: rgb(42, 161, 152);">9999</span>;i++){

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> a,b,c,d,t;

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(i&lt;<span class="hljs-number" style="color: rgb(42, 161, 152);">1000</span>){
            t = i;
            d=t%<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            t=t/<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            c=t%<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            t=t/<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            b=t%<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            a=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;

            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>((a!=b)&amp;&amp;(a!=c)&amp;&amp;(a!=d)&amp;&amp;(b!=c)&amp;&amp;(b!=d)&amp;&amp;(c!=d)){
                pool[k].first=a;
                pool[k].second=b;
                pool[k].third=c;
                pool[k].forth=d;
                pool[k].ok=<span class="hljs-keyword" style="color: rgb(133, 153, 0);">true</span>;
                k++;
            }<span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span>{
                pool[k].ok=<span class="hljs-keyword" style="color: rgb(133, 153, 0);">false</span>;
            }

        }<span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span>{
            t = i;
            d=t%<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            t=t/<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            c=t%<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            t=t/<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            b=t%<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            t=t/<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;
            a=t%<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;

            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>((a!=b)&amp;&amp;(a!=c)&amp;&amp;(a!=d)&amp;&amp;(b!=c)&amp;&amp;(b!=d)&amp;&amp;(c!=d)){
                pool[k].first=a;
                pool[k].second=b;
                pool[k].third=c;
                pool[k].forth=d;
                pool[k].ok=<span class="hljs-keyword" style="color: rgb(133, 153, 0);">true</span>;
                k++;
            }<span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span>{
                pool[k].ok=<span class="hljs-keyword" style="color: rgb(133, 153, 0);">false</span>;
            }
        }
    }


    srand((<span class="hljs-keyword" style="color: rgb(133, 153, 0);">unsigned</span> <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span>)time(NULL));
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;N;i++){
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> t = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
        t = rand() % <span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> k=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;k&lt;i;k++){
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(t == guess[k])
                t=<span class="hljs-number" style="color: rgb(42, 161, 152);">999</span>;
        }
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(t&lt;<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>){
            guess[i]=t;
        }<span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span>{
            i--;
        }
    }
    <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"First random : "</span>);
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;N;i++)
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d"</span>,guess[i]);
    <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"\n"</span>);


    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> pool_guess[N];


    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> tt=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> s,b=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;
    <span class="hljs-keyword" style="color: rgb(133, 153, 0);">while</span>(tt&lt;<span class="hljs-number" style="color: rgb(42, 161, 152);">20</span>){
        tt++;
        Result check_1,check_2;

        check_1 = query(guess);
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"%d%d%d%d\n"</span>,guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>],guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>],guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>],guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>]);
        <span class="hljs-built_in" style="color: rgb(38, 139, 210);">printf</span>(<span class="hljs-string" style="color: rgb(42, 161, 152);">"b : %d / s : %d\n"</span>,check_1.ball,check_1.strike);

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(check_1.strike==<span class="hljs-number" style="color: rgb(42, 161, 152);">4</span>){
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">return</span>;
        }

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;<span class="hljs-number" style="color: rgb(42, 161, 152);">10</span>;i++){
           digits_c2[i]=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;

        }
        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span> (<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> idx = <span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>; idx &lt; N; ++idx) {

            digits2[idx] = guess[idx];
            digits_c2[digits2[idx]]++;        <span class="hljs-comment" style="color: rgb(147, 161, 161);">//how many in each number</span>
        }


        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;<span class="hljs-keyword" style="color: rgb(133, 153, 0);">sizeof</span>(pool)/<span class="hljs-keyword" style="color: rgb(133, 153, 0);">sizeof</span>(Pool);i++){
            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(pool[i].ok==<span class="hljs-keyword" style="color: rgb(133, 153, 0);">true</span>){
                pool_guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>]=pool[i].first;
                pool_guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>]=pool[i].second;
                pool_guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>]=pool[i].third;
                pool_guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>]=pool[i].forth;

                check_2 = query2(pool_guess);


                <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>((check_1.ball==check_2.ball)&amp;&amp;(check_1.strike==check_2.strike)){
                    pool[i].ok=<span class="hljs-keyword" style="color: rgb(133, 153, 0);">true</span>;
                }<span class="hljs-keyword" style="color: rgb(133, 153, 0);">else</span>{
                    pool[i].ok=<span class="hljs-keyword" style="color: rgb(133, 153, 0);">false</span>;
                }
            }
        }

        <span class="hljs-keyword" style="color: rgb(133, 153, 0);">for</span>(<span class="hljs-keyword" style="color: rgb(133, 153, 0);">int</span> i=<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>;i&lt;<span class="hljs-keyword" style="color: rgb(133, 153, 0);">sizeof</span>(pool)/<span class="hljs-keyword" style="color: rgb(133, 153, 0);">sizeof</span>(Pool);i++){

            <span class="hljs-keyword" style="color: rgb(133, 153, 0);">if</span>(pool[i].ok==<span class="hljs-keyword" style="color: rgb(133, 153, 0);">true</span>){

                guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">0</span>]=pool[i].first;
                guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">1</span>]=pool[i].second;
                guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">2</span>]=pool[i].third;
                guess[<span class="hljs-number" style="color: rgb(42, 161, 152);">3</span>]=pool[i].forth;


                <span class="hljs-keyword" style="color: rgb(133, 153, 0);">break</span>;
            }
        }
    }
}
</code></pre><p style="margin: 1em 0px; word-wrap: break-word;">초기에 숫자를 4 4 2로 나누어서 유추하는 방법도 생각 가능 -&gt; 그러나 query가 위 과정보다 더욱 많이 쓰인다</p></div>
