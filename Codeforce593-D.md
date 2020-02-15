#Codeforce593-D

@(3.Codeforce)


1.又是图形路径搜索题，应该说最害怕的就是这种题，搜索一直学得不好，就拿这题拿来好好学一下吧
2.题目理解还是挺明白的，所有节点(除障碍节点外)都要经过一次，数组肯定是少不了的；
3.所有节点只能经过一次，不能重复经过，所以貌似和遍历图的算法有一点不太一样，再想想；
4.所以是不是应该再开一个同样大小的数组，对其进行标记每个位置，是已经走过还是有障碍亦或是还没走过？貌似这个方法有点笨拙，能不能改进？
5.好想看答案，不行，再想想；

###6.vector< > 容器真鸡儿好用！！！抓紧好好多学学STL
总的来说还是多看Codeforce上别人的优秀代码！！！

	 vector<vector<int> > a(10, vector<int>(5));   
     //创建一个10行5列的int型二维数组 相当于a[10][5];
	 //注意最外面的一层尖括号，之间有空格；先记住格式；

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 1e5 + 24;
typedef long long LL;
LL n, m, k, x, y, A, M, a, b, c, d;
vector<LL> p[N], q[N];	 //等价于 <=> vector<vector<LL> > p,q;
//本质都是二维数组，但是有一些细节不同，再查查；参考如下：
//https://blog.csdn.net/u013068755/article/details/70198924
int main() {
    scanf("%lld%lld%lld", &n, &m, &k);
    for (int i = 1; i <= k; i++) {
        scanf("%lld%lld", &x, &y);
        p[x].push_back(y), q[y].push_back(x);//这里不需要分号吗？？？
    }
    A = 1, x = y = 1;
    M = m - b;
    for (auto u : p[x])
        if (u > y) M = min(M, u - 1);
    A += M - y, a = x, y = M;
    while (1) {
        M = n - c;
        for (auto u : q[y])    //!!!!!!!
            if (u > x) M = min(M, u - 1);
        if (M == x) break;
        A += M - x, b = m - y + 1, x = M;
 
        M = d + 1;
        for (auto u : p[x])
            if (u < y) M = max(M, u + 1);
        if (M == y) break;
        A += y - M, c = n - x + 1, y = M;
 
        M = a + 1;
        for (auto u : q[y])
            if (u < x) M = max(M, u + 1);
        if (M == x) break;
        A += x - M, d = y, x = M;
 
        M = m - b;
        for (auto u : p[x])
            if (u > y) M = min(M, u - 1);
        if (M == y) break;
        A += M - y, a = x, y = M;
    }
    if (A == n * m - k)
        puts("Yes");
    else
        puts("No");
 
    return 0;
}
```

````cpp

