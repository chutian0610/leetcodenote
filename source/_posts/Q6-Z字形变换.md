---
title: Q6.Z字形变换
date: 2019-09-13 16:59:51
mathjax: false
---
# Q6.Z字形变换

## 问题描述

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。比如输入字符串为 `LEETCODEISHIRING`行数为 3 时，排列如下：

```text
L   C   I   R
E T O E S I I G
E   D   H   N
```

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。请你实现这个将字符串进行指定行数变换的函数：

```java
string convert(string s, int numRows);
```

示例 1:

* 输入: s = "LEETCODEISHIRING", numRows = 3
* 输出: "LCIRETOESIIGEDHN"

示例 2:

* 输入: s = "LEETCODEISHIRING", numRows = 4
* 输出: "LDREOEIIECIHNTSG"

```text
L     D     R
E   O E   I I
E C   I H   N
T     S     G
```

## 思路

这道题目初一看是道数学题，于是我决定找找规律:

```text
L     D     R
E   O E   I I
E C   I H   N
T     S     G
```
n=4，i从0开始

* 第0行是`2(n-1)*i`
* 第k行是 `2(n−1)*i+k` 和 `2(n−1)*i-k`
* 第n-1行是`2(n-1)*i+n-1`

```java
public class Solution {
    public String convert(String s, int numRows) {
        if(numRows == 1){return s;}
        int len = s.length();
        StringBuffer sb = new StringBuffer();
        int cyclecount = 2*numRows-2;
        for(int i = 0;i<numRows;i++){
            if(i ==0 || i== numRows-1){
                int begin = i;
                while(begin<len){
                    sb.append(s.charAt(begin));
                    begin = begin + cyclecount;
                }
            }else{
                int begin1 = i;
                int begin2 = cyclecount -i;
                while(begin1<len){
                    sb.append(s.charAt(begin1));
                    if (begin2<len){
                        sb.append(s.charAt(begin2));
                    }
                    begin1 = begin1+cyclecount;
                    begin2 = begin2+cyclecount;
                }
            }
        }
        return sb.toString();
        
    }
}
```