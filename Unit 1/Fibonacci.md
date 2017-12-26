#  斐波那契数列
- 斐波那契数列（Fibonacci sequence），又称黄金分割数列、因数学家列昂纳多·斐波那契（Leonardoda Fibonacci）以兔子繁殖为例子而引入，故又称为“兔子数列”，指的是这样一个数列：1、1、2、3、5、8、13、21、34、……在数学上，斐波纳契数列以如下被以递归的方法定义：F(0)=0，F(1)=1, F(n)=F(n-1)+F(n-2)（n>=2，n∈N*）在现代物理、准晶体结构、化学等领域，斐波纳契数列都有直接的应用，为此，美国数学会从1963起出版了以《斐波纳契数列季刊》为名的一份数学杂志，用于专门刊载这方面的研究成果

- 代码实现：
```C,C++
int fibonaccil(int n)//递归实现
{
    if(n==0||n==1)return n;
    else return (fibonaccil(n-2)+fibonaccil(n-1));
}
//实际测试中发现当N达到48就会发生溢出,所以如果要计算比较大的Fibonacci数列就需要用数组来模拟加法
int fibonaccil(int n)//递归转换为递推实现
{
    int fib0=1,fib1=1,fib=0;
    if(n<=1)return 1;
    for(int i=0;i<n-1;i++)
    {
        fib=fib0+fib1;
        fib0=fib1;
        fib1=fib;
    }
    return fib;
}
```

```python
#python3递归在实际的运行中效果极其差，我测试了一下Fibonacci(60),在我的PC机器上运行，CPU I7-6700HQ,运行超过12分钟也
#没有计算出结果
def fibonaccil(n):     #level 1：
    if(n==0 or n==1):
        return n
    return (fibonaccil(n-2)+fibonaccil(n-1))

def Fibonacci(n):      #level 10：
#python3递推实际测试Fibonacci(1000000) 用时17s，python存在长整形，内部实现是模拟数组类似，存储上限和内存有关系。
    fib0=1
    fib1=1
    if n<=1:
        return 1
    i=0
    while i<n-1:
        i+=1
        fib2=fib0+fib1
        fib0=fib1
        fib1=fib2
    return fib2
    
def fibonaccil(n):     #level 99：
#实际测试Fibonacci(1000000) 用时2s,emmm，性能max 参考博客 http://blog.csdn.net/ncafei/article/details/54176276
 lhm=[[0,1],[1,1]]
 rhm=[[0],[1]]
 em=[[1,0],[0,1]]
 #multiply two matrixes
 def matrix_mul(lhm,rhm):
  #initialize an empty matrix filled with zero
  result=[[0 for i in range(len(rhm[0]))]for j in range(len(rhm))]
  #multiply loop
  for i in range(len(lhm)):
   for j in range(len(rhm[0])):
    for k in range(len(rhm)):
     result[i][j]+=lhm[i][k]*rhm[k][j]
  return result
  
 def matrix_square(mat):
  return matrix_mul(mat,mat)
 #quick transform
 def fib_iter(mat,n):
  if not n:
   return em
  elif(n%2):
   return matrix_mul(mat,fib_iter(mat,n-1))
  else:
   return matrix_square(fib_iter(mat,n/2))
 return matrix_mul(fib_iter(lhm,n),rhm)[0][0]
 ```
 
