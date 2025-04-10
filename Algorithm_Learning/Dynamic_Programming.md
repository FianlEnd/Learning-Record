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