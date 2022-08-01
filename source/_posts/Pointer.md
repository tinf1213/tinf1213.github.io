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

<h2> 實裝例swap </h2>

<h3> 1. int </h3>

```cpp
#include <bits/stdc++.h>
 using  namespace std;

 void swap_int(int a, int b){
    swap(a, b);
    cout << "In function:" << endl;
    cout << " a = " << endl;
    cout << " b = " << endl;
    }
 int main(){
    int a = 1 ;
    int b = 2 ;
    swap_int(a, b);
    cout << "In main:" << endl;
    cout << " a = " << a << endl;
    cout << " b = " << b << endl;
    return  0 ;
}
```

<h4>output</h4>

```
in function:
 a = 2
 b = 1
in main:
 a = 1
 b = 2
```

>交換失敗，原因是a,b在main及function中為兩獨立區域變數，不互相干擾。

---

<h3> 2. *int </h3>


```cpp
#include <bits/stdc++.h>
using  namespace std;

void swap_value_ptr(int *ptra, int *ptrb){
    swap(*ptra, *ptrb);
}

int main(){
    int a = 1 ;
    int b = 2 ;
    cout << "Before swap:" << endl;
    cout << " a = " << a << endl;
    cout << " b = " << b << endl;
    cout << " &a = " << &a << endl;
    cout << " &b = " << &b << endl;
    swap_value_ptr(&a, &b);
    cout << "After swap:" << endl;
    cout << " a = " << a << endl;
    cout << " b = " << b << endl;
    cout << " &a = " << &a << endl;
    cout << " &b = " << &b << endl;
    return  0 ;
}
```
>將a,b記憶體位置傳入function，並交換兩記憶體內value

<h4> output</h4>

```
Before swap:
 a = 1
 b = 2
 &a = 0x7ffcdb13f900
 &b = 0x7ffcdb13f904
After swap:
 a = 2
 b = 1
 &a = 0x7ffcdb13f900
 &b = 0x7ffcdb13f904
```

>從output可以看出a,b變數之記憶體維持而變數value交換。

---


<h3> 3. &int </h3>

```cpp
#include <bits/stdc++.h>
using  namespace std;

void swap_ref(int &refa, int &refb){
    swap(refa, refb);
}

int main(){
    int a = 1 ;
    int b = 2 ;
    cout << "Before swap:" << endl;
    cout << " a = " << a << endl;
    cout << " b = " << b << endl;
    cout << " &a = " << &a << endl;
    cout << " &b = " << &b << endl;
    swap_ref(a, b);
    cout << "After swap:" << endl;
    cout << " a = " << a << endl;
    cout << " b = " << b << endl;
    cout << " &a = " << &a << endl;
    cout << " &b = " << &b << endl;
    return  0 ;
}
```

>原理同上一個，改用引用方式調換value

<h4>output</h4>

```
Before swap:
 a = 1
 b = 2
 &a = 0x7ffd068869c0
 &b = 0x7ffd068869c4
1
After swap:
 a = 2
 b = 1
 &a = 0x7ffd068869c0
 &b = 0x7ffd068869c4
```

>從output可以看出a,b變數之記憶體維持而變數value交換。







參考資料： <a href = "https://www.cnblogs.com/alephsoul-alephsoul/archive/2012/10/10/2719192.html" target = "_blank" style = "text-decoration:none;color:blue;"> [C++基礎]019_指針和引用（int*、int&、int*&、int&*、int**）</a>, <a href = "https://www.geeksforgeeks.org/pointers-vs-references-cpp/" target = "_blank" style = "text-decoration:none;color:blue;"> Pointers vs References in C++</a>