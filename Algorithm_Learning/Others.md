# **其他**
***
## **小记**
```
//multiset<int> s和集合区别是可以有重复值
//int a=stoi("123")
//string的一些操作，如starts_with()
//递归的灵活使用
https://leetcode.cn/problems/binary-tree-right-side-view/solutions/2015061/ru-he-ling-huo-yun-yong-di-gui-lai-kan-s-r1nc/?envType=study-plan-v2&envId=top-100-liked
```
***
## **欧拉法检索素数**

```
vector<int> mark(n+1,1);
set<int> primes;
for(int i = 2; i <= n; i++) {
    if(mark[i]){
        primes.insert(i);
    }
    for(auto m:primes){
        if(i*m > n) break;
        mark[i*m] = 0;
        if(i%m == 0) break;
    }
}
```
***
## **辗转相除求最大公约数**

```
int Fac(int a, int b)
{
	int d = 1;
	while (d)
	{
		d = a % b;
		a = b;
		b = d;
	}
	return a;
}
```
***
## **一个贪心的解法以及一个位运算的解法**
```
for (auto x : nums) {
    multi_bits |= x & or_sum;
    or_sum |= x;
}//找出重复的位上1
for (auto x : nums) {
    res = max(res, (or_sum ^ x) | (1ll * x << k) | multi_bits);
}//除x外的或值，但是有可能把重复的1或也变成0,所以再或上之前找到的重复位
https://leetcode.cn/problems/maximum-or/description/
(注意一下方法)
```
***
## **判断一个含左右括号的字符串是否有效**
```
//子序列和子串意思不一样
//含有可以改变的字符，从左到右，是左括号就加一，右括号就减一，不确定就加一和减一
//数学归纳法得出每次结果集合都是连续的偶数或奇数
//然后每次只看结果的最大和最小，最后结果最小是0则满足题意
https://leetcode.cn/problems/check-if-a-parentheses-string-can-be-valid/description/
```
***

## **使所有字符相等的最小成本**
```
(思路想到就很简单)
https://leetcode.cn/problems/minimum-cost-to-make-all-characters-equal/description
```
***

## **前缀和数组的表示方法**
```
//例如s[r]−s[l]就能表示r到l中1的数目（s[n]统计0到n的1数目）
```
***