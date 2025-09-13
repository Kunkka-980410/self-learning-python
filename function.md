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
a = power(4)
b = power(5,3)
print(b)
print(a)
```
**默认参数一般会为了方便不需要手动输入**
例如
```python
int(16,[这里默认十进制，不需要填])
int(16,8) #如果想将int里的数值转换成八进制，可以这样写
```
### 可变参数 
```python
a = [1,4,5,6,7,8,3]
result = 0
for i in a:
  result += i
print(result)

将他用函数封装
def total(a):
  result = 0
  for i in a:
    result += i
return result

result = total([1,4,5,6,7,8,3])
print(result)
```

上述代码可改为可变参数
```python
a = [1,4,5,6,7,8,3]
result = 0
for i in a:
  result += i
print(result)

将他用函数封装
def total(*a):   #在a前面加个*号，就默认为可变参数，可以对a变成tuple进行处理
  result = 0
  for i in a:
    result += i
return result

result = total(1,4,5,6,7,8) #这里不填入list，直接填入tuple并且少写了一个3
print(result)

```
