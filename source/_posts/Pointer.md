---
title: Pointer&Reference
date: 2022-07-30 10:58:23
tags:
    - CS
    - C++
---

<center>
Cpp Operation Note
</center>

<!--more-->

---

> <p>不同於Python及Java, c++同時支援Pointer及Reference。<p>

---

<h2>名詞解釋</h2>

>1. Value (值): 記憶體內儲存的變數
2. Pointer (指標): 存儲變數之記憶體的絕對位置
*Pointer會另開記憶體存取地址。
3. Reference (引用): 調出變數所存在記憶體之絕對位置
*Reference導向所附記憶體位置，不另開記憶體。
4. 操作符 (&): 取變數所在之記憶體絕對位置。
5. 操作符 (*): 對記憶體位置取出值。



---

<h2> 初始化 </h2>

1. Pointer初始化:

```cpp

int a = 5;
int *ptr = &a;

//or

int *ptr;
ptr = &a;

//ptr = 0x------------;
//*ptr = 5;
```

2. Reference初始化:

```cpp
int a = 5;
int &ref = a;

//but

int &ref;
ref = a; // This operation is incorrect.

int *ptr = &a;

//ref = *ptr = 5;
//&ref = ptr = 0x------------;
```

3. 重新附值:

```cpp
int a = 3;
int b = 5;
int *ptr;

ptr = &a;
ptr = &b;
```

>Pointer可以重新附值

```cpp
int a = 3;
int b = 5;

int &ref = a;
int &ref = b;//This wil throw an error of "multiple declaration is not allowed"
```

>Reference不可被重新附值及宣告

---

<h2> 實裝例 </h2>

1. 







參考資料： <a href = "https://www.cnblogs.com/alephsoul-alephsoul/archive/2012/10/10/2719192.html" target = "_blank" style = "text-decoration:none;color:blue;"> [C++基礎]019_指針和引用（int*、int&、int*&、int&*、int**）</a>, <a href = "https://www.geeksforgeeks.org/pointers-vs-references-cpp/" target = "_blank" style = "text-decoration:none;color:blue;"> Pointers vs References in C++</a>
