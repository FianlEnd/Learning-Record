# **动态规划**
***
## **01背包问题**

状态转移方程：f[i][j] = max(f[i - 1][j], f[i - 1][j - w[i]] + v[j])

简化后代码：
```
for (int i = 1; i <= n; i++)
{
    for (int j = V; j >= 0; j--)
    {
        if (j >= w[i])
        {
            f[i][j] = max(f[i - 1][j], f[i - 1][j - w[i]] + v[i]);
        }
        else
        {
            f[i][j] = f[i - 1][j];
        }
    }
}
```
***
## ** Floyd-Warshall算法**
```
//求图中任意两点间的最短距离
for (int k = 0; k < n; k++) {         // 允许中转城市 k
    for (int i = 0; i < n; i++) {     // 遍历所有起点 i
        for (int j = 0; j < n; j++) { // 遍历所有终点 j
            if (dist[i][k] + dist[k][j] < dist[i][j]) {
                dist[i][j] = dist[i][k] + dist[k][j]; // 更新最短距离
            }
        }
    }
}（共享电车问题pta 7-5）
```
***
## **最长公共子序列**
```
int main() {
    int n;
    cin >> n;
    vector<int> P1(n + 1), P2(n + 1);
    vector<int> pos(n + 1); // pos[x] 表示x在P1中的位置（1-based）
    for (int i = 1; i <= n; ++i) {
        cin >> P1[i];
        pos[P1[i]] = i;
    }
    for (int i = 1; i <= n; ++i) {
        cin >> P2[i];
    }
    vector<int> B;
    for (int i = 1; i <= n; ++i) {
        B.push_back(pos[P2[i]]);
    }
    vector<int> lis;
    for (int num : B) {
        auto it = lower_bound(lis.begin(), lis.end(), num);
        if (it == lis.end()) {
            lis.push_back(num);
        } else {
            *it = num;
        }
    }
    cout << lis.size() << endl;
    return 0;
}
```
