# 1042 Shuffling Machine (20 分)
## 题目大意：
### 模拟洗牌
牌序初始位置
[S1-S13 H1-H13 C1-C13 D1-D13 J1 J2]
按照给定的移动顺序重复k次
### 示例：
step|S3|	H5|	C1	|D13|	J2
:--:|:--:|:--:|:--:|:--:|:--:
初始  |4	|2	|5	|3	|1
i1->4| | | |S3|
i2->2| | H5| |S3|
i3->5| | H5| |S3|C1
i4->3| | H5|D13 |S3|C1
i5->1|J2 | H5|D13 |S3|C1
### 解题思路
牌面视为1-54 输出时转为SHDJ 花色为牌面/13 大小为牌面%13
#### 洗牌过程
设<br>
原始牌面数组cards[55]<br>
结果牌面数组 res[55]<br>
洗牌步骤order[55]<br>
访问标记数组bool visited[55]= {false}<br>
当前访问位置pos<br>
<pre><code>
for(k){
    for(i in 1-54){
        int pos=order[i]
        res[pos]=cards[i]
    }
    cards=res
}
</code></pre>
### AC代码：
<pre><code>
#include <iostream>
#include <stdlib.h>
#include <vector>
using namespace std;
int main()
{
    int k;
    char shape[6] = "SHCDJ";
    vector<int> cards;
    vector<int> res;
    vector<int> order;
    scanf("%d", &k);
    for (int i = 1; i <= 54; i++)
    {
        cards.push_back(i);
        res.push_back(0);
        int temp;
        scanf("%d", &temp);
        order.push_back(temp - 1);
    }
    while (k--)
    {
        for (int i = 0; i < 54; i++)
        {
            int pos = order[i];
            res[pos] = cards[i];
        }
        cards = res;
    }
    printf("%c%d", shape[(res[0] - 1) / 13], (res[0] - 1) % 13 + 1);
    for (int i = 1; i < 54; i++)
    {
        printf(" %c%d", shape[(res[i] - 1) / 13], (res[i] - 1) % 13 + 1);
    }
    printf("\n");
    system("pause");
    return 0;
}

</code></pre>

