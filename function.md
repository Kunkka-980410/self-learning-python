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

---
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

---
### 在字典里操作可变参数

```python
def f(**kwargs):  # 接收任意数量的关键字参数，打包成一个字典
    for k, v in kwargs.items():  # 遍历字典的键值对
        print(k, v)

d = {'name': 'xiaoming', 'age': 18}
f(**d)  # 使用 ** 解包字典为关键字参数传入函数

```

---
## 全局变量和局部变量

🌍 全局变量（Global Variable）
定义位置：函数外部 作用范围：整个程序都可以访问 生命周期：从定义开始直到程序结束

示例：
```python
x = 10  # 全局变量

def show():
    print(x)  # 可以访问全局变量

show()  # 输出：10
```

🧪 局部变量（Local Variable）
定义位置：函数内部 作用范围：只在函数内部有效 生命周期：函数调用开始到结束

示例：
```python
def show():
    y = 5  # 局部变量
    print(y)

show()  # 输出：5
print(y)  # 报错：NameError，因为 y 是局部变量
```

⚠️ 注意事项：变量冲突与修改
1. 局部变量覆盖全局变量
```python
x = 10

def show():
    x = 5  # 局部变量，覆盖了全局变量
    print(x)

show()  # 输出：5
print(x)  # 输出：10（全局变量没变）
```
2. 在函数中修改全局变量：使用 global

```python
x = 10

def modify():
    global x
    x = 20

modify()
print(x)  # 输出：20
```

🧠 进阶：嵌套函数中的 nonlocal
用于修改外层函数的局部变量：
```python
def outer():
    x = 5
    def inner():
        nonlocal x
        x = 10
    inner()
    print(x)  # 输出：10

outer() #输出10
```
