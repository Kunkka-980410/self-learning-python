## 定义一个函数

```python
def sum_1(a,b):     #sum是python内置函数，不要写重名，a,b是形式参数
  return a+b       #return返回对参数的处理了过程和结果

result =sum_1(a,b)    #设置一个变量接受返回值，这里填写的a，b是有实际值的实参
print(result)
```
----
### 参数顺序
**实参顺序与形参必须一致**

```python
def power(x,n)  #不把n填进去的时候，一般默认为2，这叫缺省参数或者默认参数
  return x**n
a = power(4,3)
b = power(5,3)
print(b)
print(a)
```
**默认参数一般会为了方便不需要手动输入**
例如 `int(16,[这里默认十进制，不需要填])`
如果想将int里的数值转换成八进制，可以这样写`int(16,8)`
