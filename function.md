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

---
### 匿名函数
匿名函数在 Python 中是通过 lambda 关键字创建的，它是一种没有名字的小型函数，通常用于一次性、简洁的操作，非常适合配合像 map()、filter()、sorted() 这样的函数使用
🧪 基本语法
```python
lambda 参数1, 参数2, ... : 表达式
```
参数可以有多个

表达式只能有一个（不能写多行逻辑）

返回值就是表达式的结果

✅ 示例讲解
1. 最简单的匿名函数
```python
f = lambda x: x + 1
print(f(5))  # 输出：6
```
2. 多参数
```python
add = lambda x, y: x + y
print(add(3, 4))  # 输出：7
```
3. 用在 map() 中
```python
nums = [1, 2, 3, 4]
squared = list(map(lambda x: x**2, nums))
print(squared)  # 输出：[1, 4, 9, 16]
```

关于map函数的一点说明
🧪 基本语法
```python
map(function, iterable)
```
function：你要应用的函数，可以是普通函数，也可以是匿名函数（lambda）

iterable：一个可迭代对象，比如列表、元组、集合等

返回值是一个 map 对象（迭代器），通常我们会用 list() 把它转换成列表。
**总的来说就是把 function 的处理结果 应用到 iterable 的每个元素上，并返回一个新的 迭代器对象。**


4. 用在 filter()中
```python
nums = [1, 2, 3, 4, 5]
even = list(filter(lambda x: x % 2 == 0, nums))
print(even)  # 输出：[2, 4]
```
5. 用在 sorted() 中自定义排序
```python
names = ['Tom', 'Alexander', 'Bob']
sorted_names = sorted(names, key=lambda x: len(x))
print(sorted_names)  # 输出：['Tom', 'Bob', 'Alexander']
```
⚠️ 注意事项
lambda 适合写简单逻辑，不推荐处理复杂流程。

如果逻辑太复杂，建议使用 def 定义普通函数，更清晰易维护。


---
### 递归函数
递归函数是编程中一种非常强大的技巧，它的核心思想是：函数自己调用自己，直到满足某个终止条件为止。听起来像“套娃”，但其实非常实用，尤其在处理分治问题、树结构、数学计算等场景时
🧠 什么是递归函数？
递归函数就是在函数内部调用自己本身的函数。它通常包含两个部分：

终止条件（Base Case）：防止无限调用，必须有！

递归调用（Recursive Case）：函数调用自身，逐步逼近终止条件。

✅ 示例：计算阶乘
```python
def factorial(n):
    if n == 1:         # 终止条件
        return 1
    else:
        return n * factorial(n - 1)  # 递归调用
```

调用 factorial(5) 的过程如下：

```代码
factorial(5)
→ 5 * factorial(4)
→ 5 * 4 * factorial(3)
→ 5 * 4 * 3 * factorial(2)
→ 5 * 4 * 3 * 2 * factorial(1)
→ 5 * 4 * 3 * 2 * 1 = 120
```

🧩 再看一个例子：斐波那契数列
```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
```
---
## 调用函数
基本调用方法
1. 无参数函数
```python
# 定义函数
def say_hello():
    print("你好！")

# 调用函数
say_hello()  # 输出: 你好！
```
2. 带参数函数
```python
# 定义函数
def greet(name):
    print(f"你好，{name}！")

# 调用函数
greet("小明")  # 输出: 你好，小明！
greet("小红")  # 输出: 你好，小红！
```
3. 带返回值的函数
```python
# 定义函数
def add(a, b):
    return a + b

# 调用函数并接收返回值
result = add(3, 5)
print(result)  # 输出: 8

# 或者直接使用返回值
print(add(10, 20))  # 输出: 30
```
完整的调用示例
```python
# 定义几个不同类型的函数
def show_info():
    print("=== 用户信息 ===")

def calculate_bmi(weight, height):
    """计算BMI指数"""
    bmi = weight / (height ** 2)
    return bmi

def create_email(username, domain="gmail.com"):
    """生成邮箱地址"""
    return f"{username}@{domain}"

# 调用函数
show_info()  # 调用无参数函数

bmi_result = calculate_bmi(70, 1.75)  # 调用带参数函数
print(f"您的BMI是: {bmi_result:.2f}")

email = create_email("zhangsan")  # 使用默认参数
print(f"邮箱: {email}")

email2 = create_email("lisi", "qq.com")  # 覆盖默认参数
print(f"邮箱: {email2}")
```
输出结果：

```text
=== 用户信息 ===
您的BMI是: 22.86
邮箱: zhangsan@gmail.com
邮箱: lisi@qq.com
```
---
常见调用方式
1. 位置参数调用
```python
def introduce(name, age, city):
    print(f"我叫{name}，今年{age}岁，来自{city}")

introduce("张三", 25, "北京")  # 参数按顺序传递
```
2. 关键字参数调用
```python
introduce(name="李四", age=30, city="上海")  # 明确指定参数名
introduce(age=28, city="广州", name="王五")  # 顺序可以打乱
```
3. 混合使用
```python
introduce("赵六", age=35, city="深圳")  # 位置参数必须在关键字参数之前
```
---
**重要注意事项**
函数必须先定义后调用

```python
# 错误示例
say_hello()  # NameError: name 'say_hello' is not defined

def say_hello():
    print("Hello!")
```
参数数量必须匹配

```python
def multiply(a, b):
    return a * b

# multiply(5)        # 错误：缺少1个参数
# multiply(1, 2, 3)  # 错误：多出1个参数
multiply(3, 4)       # 正确：返回12
```
函数名区分大小写

```python
def my_function():
    print("这是一个函数")

my_function()  # 正确
# My_Function()  # 错误：函数名大小写不匹配
```
实际应用示例
```python
# 游戏角色相关的函数
class Player:
    def __init__(self, name):
        self.name = name
        self.level = 1

def level_up(player):
    """角色升级"""
    player.level += 1
    print(f"{player.name} 升级了！当前等级: {player.level}")
    return player.level

def check_status(player):
    """检查角色状态"""
    print(f"角色: {player.name}")
    print(f"等级: {player.level}")

# 创建角色并调用函数
mia = Player("mia")
check_status(mia)  # 调用状态检查函数

new_level = level_up(mia)  # 调用升级函数
print(f"新等级: {new_level}")
```
总结：调用函数的基本语法就是 函数名(参数1, 参数2, ...)，根据函数定义时的参数要求来传递相应的参数即可。
