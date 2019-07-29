---
title: C++字符统计算法
tags:
  - C++
  - 字符统计
id: 8
categories:
  - C++ / Visual C++
  - 算法、
date: '2015-06-14T18:02:08.000Z'
---

# C++字符统计算法

首先说说思路:假设我们有一个待统计字符串**ibuf**.现在要统计其中每个字符出现的次数.

首先我们需要确定的是这个字符串有多少个不同的字符.以便建立统计缓存.

所以我们遍历整个**ibuf**\(假设其长度为**ilen**\),将其中的字符无重复的放入临时字符串**differList**\(假设其长度为**llen**\).

根据**differList**字符串的长度建立相应的统计缓存数组.统计缓存数组如下:

* int \*count = new int\[llen\];

  再经过第二次遍历,统计**ibuf**中的所有字符出现次数.

最后,输出结果…..

————————————————–

本文章源代码如下:

/_/ 字符统计算法. 该算法可以用来统计在一个字符串中各个字符的出现次数. by Kanch @2015-2-6_ /

## include

## include

## include

using namespace std;

int main\(int argc, char argv\[\]\) { string ibuf = "", obuf = "",differList=""; int ilen = 0,\*count,llen;

cout &lt;&lt; "请输入数据,程序将会统计字符出现次数!-输入 EXIT 退出程序." &lt;&lt; endl; cin &gt;&gt; ibuf; while \(ibuf != "EXIT" && ibuf != "exit"\) { //开始统计 if \(ibuf.length\(\)&lt;=0\) { cout &lt;&lt; "没有检测到任何数据请重新输入!-输入 EXIT 退出程序." &lt;&lt; endl; continue; } else if \(ibuf.length\(\) &gt; 0\) { ilen = ibuf.length\(\); for \(int i = 0; i &lt; ilen; i++\) //这个循环用来统计有多少个不同的字符 { if \(differList.find\(ibuf\[i\]\) &lt; 0 \|\| differList.find\(ibuf\[i\]\) &gt;= differList.length\(\)\) { differList += ibuf\[i\]; } } llen = differList.length\(\); //这里来确定需要循环多少次.有多少个不同的字符就循环多少次 count = new int\[llen\]; //为每个待统计字符分配统计空间.顺序与differList里面的一样. for \(int e = 0; e &lt; llen; e++\) { count\[e\] = 0; }

//下面开始统计 /\*法一 for \(int i = 0; i &lt; len; i++\) //这是最笨的方法 {

for \(int t = 0; t &lt; ibuf.GetLength\(\); t++\) //这个用来逐个统计每个字符出现的次数; { if \(differList\[i\] == ibuf\[t\]\) { count\[i\] += 1; } } } _/ /_法二\*/ for \(int i = 0; i &lt; ilen; i++\) //个人比较喜欢这个方法. { count\[differList.find\(ibuf\[i\]\)\] += 1; }

//算法结束,下面输出结果 cout &lt;&lt; "===========================结果=============================" &lt;&lt; endl &lt;&lt; "共"&lt;&lt; ilen &lt;&lt; "个字符." &lt;&lt; "其中有" &lt;&lt; llen &lt;&lt; "不相同字符." &lt; for \(int i = 0; i &lt; llen; i++\) { cout &lt;&lt; " " &lt;&lt; differList\[i\] &lt;&lt; "t " &lt;&lt; count\[i\] &lt;&lt;endl; } } cin.clear\(\); differList = ""; cout &lt;&lt; "请输入数据,程序将会统计字符出现次数!-输入 EXIT 退出程序." &lt;&lt; endl; cin &gt;&gt; ibuf; delete \[\] count;

}

return 0; }&lt;/pre&gt;  
