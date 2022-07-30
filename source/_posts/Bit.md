---
title: Bit operation
date: 2022-07-27 17:15:13
tags: CS
---

<center>
Bit algorithm Note
</center>

<!--more-->


<h3> 建立二進位數字 </h3>

C++可支援0b字首建立二進位，C語言則否。

```cpp
int n = 0b1010111100011100; // 44828
```

<h3> Most Significant Bit / Least Significant Bit </h3>

最高有效位元（最左位元）、最低有效位元（最右位元）。簡稱MSB, LSB


<h2>Bitwise Operation</h2>

<h3> Bitwise shift</h3>

> 0101 << 1010; // 9 => 18
1010 >> 0101; // 18 => 9

---

<h3> Bitwise AND(&)</h3>

>0 & 0 = 0
1 & 0 = 0
0 & 1 = 0
1 & 1 = 1

用＆計算二進位數字中1的個數

```cpp
int count_bit_1(int n)
{
    int count = 0;
    for (; n; n>>=1) // n>>=1 刪掉n的最右位元。
        if (n & 1)
            count++;
    return count;
```

---

<h3> Bitwise OR(|) </h3>

>0 | 0 = 0
0 | 1 = 1
1 | 0 = 1
1 | 1 = 1

用｜強制將數字轉為1

```cpp
int mark_5th_bit(int n)
{
    return n | (1 << 4);
}
```

---

<h3> Bitwise XOR(^) </h3>

>0 ^ 0 = 0
0 ^ 1 = 1
1 ^ 0 = 1
1 ^ 1 = 0

用^顛倒位元

```cpp
int reverse_5th_bit(int n)
{
    return n ^ (1 << 4);
}
```

---

<h3> Bitwise NOT(~) </h3>

>~ 0 = 1
~ 1 = 0

Not 翻轉所有位元

---

<h3> 補充 </h3>
signed 變數沒有定義bit右移時的補充位元，因此在使用 >> 時容易出錯。
因此使用位元運算考慮使用usigned變數。



<h2> Bitwise tricks </h2>

<h3> 2的n次冪 </h3>
二進位數一次左移表示為十進位為乘2, 且運算度快於十進位數字乘以2。

```cpp
unsigned int  n = 5;
n <<= 2; // n * 2 ** 2 = 20;
n >>= 1; // n / 2 ** 1 = 2;
``` 
---

<h3> Bitset </h3>

一個 int 變數當作一個集合，一個位元當作一個元素。

參考資料： <a href = "https://web.ntnu.edu.tw/~algo/Bit.html" target = "_blank" style = "text-decoration:none;color:blue;"> Bit-演算法筆記</a>

