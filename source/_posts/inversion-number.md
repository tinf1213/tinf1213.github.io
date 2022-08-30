---
title: Inversion number
date: 2022-08-24 19:09:05
tags:
    - CS
    - algorithm
    - Bit
---

<center>
Inversion Number algorithm Note
</center>

<!--more-->

<h3> 転倒数的意義 </h3>

簡單來說就是泡泡排序的交換次數
但為什麼不直接實做排序再計算次數呢？
泡泡搜尋法的最差複雜度為 O(N^2）而使用Bit計算可以達到 O(NlogN)

<h3> 分析泡泡排序法的交換次數 </h3>

<h4> 1. 如何判斷一個數字會交換的次數？ </h4>

泡泡搜尋法的交換規則為左邊的值大於右邊的值即發生交換。

<h4> 2. 計算總交換次數 </h4>

由此可以得知總交換次數為所有數字之現在位置的左邊大於自己值的個數總和。
>相對位置在Ai左邊而值大於Ai之數後簡稱前置大數。

<h3> 實現計算所有前置大數的原理(與計數排序法counting sort類似) </h3>

<a href="https://atcoder.jp/contests/chokudai_S001/tasks/chokudai_S001_j" target="_blank" style="text-decoration:none;color:blue;">例題1: Atcoder s001_j</a>

<a href="https://atcoder.jp/contests/abc264/editorial/4582" target="_blank" style="text-decoration:none;color:blue;">例題2: Atcoder abc264_d</a>

<h4> 1. BIT內以A的值為index紀錄出現過數字。</h4>

|index|1  |2  |3  |4  |5  |6  |7  |8  |9  |
|-----|---|---|---|---|---|---|---|---|---|
|A:   |8  |3  |6  |5  |2  |4  |1  |9  |7  |
|BIT: |   |   |   |   |   |   |   |   |   |

|index|1  |2  |3  |4  |5  |6  |7  |8  |9  |
|-----|---|---|---|---|---|---|---|---|---|
|A:   |(8)|3  |6  |5  |2  |4  |1  |9  |7  |
|BIT: |   |   |   |   |   |   |   |1  |   |

|index|1  |2  |3  |4  |5  |6  |7  |8  |9  |
|-----|---|---|---|---|---|---|---|---|---|
|A:   |8  |(3)|6  |5  |2  |4  |1  |9  |7  |
|BIT: |   |   |1  |   |   |   |   |1  |   |

|index|1  |2  |3  |4  |5  |6  |7  |8  |9  |
|-----|---|---|---|---|---|---|---|---|---|
|A:   |8  |3  |(6)|5  |2  |4  |1  |9  |7  |
|BIT: |   |   |1  |   |   |1  |   |1  |   |

|index|1  |2  |3  |4  |5  |6  |7  |8  |9  |
|-----|---|---|---|---|---|---|---|---|---|
|A:   |8  |3  |6  |5  |(2)|4  |1  |9  |7  |
|BIT: |   |   |1  |   |1  |1  |   |1  |   |

|index|1  |2  |3  |4  |5  |6  |7  |8  |9  |
|-----|---|---|---|---|---|---|---|---|---|
|A:   |8  |3  |6  |5  |2  |(4)|1  |9  |7  |
|BIT: |   |1  |1  |   |1  |1  |   |1  |   |

以此推計算到第六格也就是4的位置得到BIT為011011010，BIT的特性使我們可以快速加總出前綴合，而我們現在要判斷4的前置大數，透過加總BIT中1~4號位可以得出前置小數為2，在用前置數字的數量減去前置小數即可獲得前置大數的數量。關鍵： 做到第幾位就算到第幾位。

```cpp
#include<bits/stdc++.h>
using namespace std;
#define io ios_base::sync_with_stdio(0), cin.tie(0);
typedef long long int ll;
 
int n;
 
struct BIT{
    private:
        vector<int> bit;
    public:
        BIT(void){
            bit.resize(n+1);
        }
        int sumup(int x){
            int temp = 0;
            for(int i=x;i>0;i-=i&-i){
                temp += bit[i];
            }
            return temp;
        }
 
        void update(int y){
            for(int i=y;i<=n;i+=i&-i) bit[i]++;
        }
};
 
signed main(){
    cin >> n;
    vector<int> data(n);
    for(int i=0;i<n;i++) cin >> data[i];
    BIT b;
    ll ans = 0;
    for(int i=0;i<n;i++){
        ans += i - b.sumup(data[i]);
        b.update(data[i]);
    }
    cout << ans << endl;
 
    return 0;
}
```

參考資料： <a href = "https://scrapbox.io/pocala-kyopro/%E8%BB%A2%E5%80%92%E6%95%B0" target = "_blank" style = "text-decoration:none;color:blue;"> 転倒数</a>