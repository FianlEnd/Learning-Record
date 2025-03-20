# **其他**
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

