📄 readline()：一行一行读
每次调用只读取文件的一行（包括换行符）。

返回的是一个字符串。

适合处理大文件，逐行读取，节省内存。

```python
with open('file.txt', 'r') as f:
    line1 = f.readline()
    line2 = f.readline()
```
📚 readlines()：一次性读所有行
一次性读取整个文件的所有行。

返回的是一个列表，每个元素是一行字符串。

适合小文件或需要一次性处理所有内容的场景。

```python
with open('file.txt', 'r') as f:
    lines = f.readlines()
    print(lines[0])  # 第一行
```
🧠 对比总结
|方法|	返回类型	|读取方式|	适合场景
|---|---|---|---
|readline()|	字符串|	一次一行	|大文件、逐行处理
|readlines()	|列表	|一次所有行	|小文件、整体处理

---
`writelines()` 是 Python 文件操作中的一个方法，用于一次性写入多个字符串行到文件中。它是 write() 的批量版本
🖋️ writelines() 的基本用法
```python
lines = ['Hello\n', 'World\n', 'Python\n']
with open('output.txt', 'w') as f:
    f.writelines(lines)
```
参数必须是可迭代对象（如列表、元组），其中每个元素是一个字符串。

不会自动添加换行符，你必须自己在每行末尾加` \n`，否则所有内容会连在一起

⚠️ 常见坑
```python
lines = ['Line 1', 'Line 2', 'Line 3']
f.writelines(lines)  # 会写成：Line 1Line 2Line 3（没有换行）
```
解决方法：

```python
f.writelines(line + '\n' for line in lines)
```

更直观一些：

```python
with open('output.txt', 'w') as f:
    for line in lines:
        f.write(line + '\n')
```
或者提前在列表中加好换行符。

---
在 Python 中，`open(file, mode='a')` 的 `mode='a'` 表示以追加模式（append）打开文件。具体含义如下：

📌 `mode='a'` 的特点
追加写入：不会清空原文件内容，而是把新内容写在文件末尾。

自动创建文件：如果文件不存在，会自动创建一个新文件。

写入位置固定：所有写入操作都从文件末尾开始，不能覆盖已有内容。

只写不可读：默认只能写，不能读。如果想读写同时进行，需要用 'a+' 模式。
🧪 示例代码
```python
with open('log.txt', 'a') as f:
    f.write('新的一行内容\n')
```
每次运行这段代码，都会在 log.txt 的末尾添加一行，而不会影响已有内容

---
为什么`head = next(i)`可以跳过表头
📌 head = next(i) 的含义

假设 i 是一个迭代器，比如：
```python
i = open('data.csv')  # 或者 i = iter(some_list)
```
那么 next(i) 会从迭代器中取出第一个元素，也就是文件的第一行（通常是表头），并赋值给变量 head。
🧠 对比其他写法
你也可以用 readlines() 或 pandas 来跳过表头，但 next() 的方式更轻量、适合处理大文件或流式数据。

```python
with open('data.csv') as f:
    head = next(f)  # 跳过表头
    for line in f:
        ...
```
它怎么知道i是第一行的
它“知道”是第一行，其实是因为迭代器的机制决定了这一点——不是它“识别”了表头，而是你第一次调用 `next(i)` 时，迭代器就从头开始取值。

🔁 理解迭代器的行为
假设你这样打开一个文件：

```python
i = open('data.csv')  # i 是一个文件对象，也是一个迭代器
```
此时，i 的内部指针指向文件的开头。当你调用：

```python
head = next(i)
```
你就是第一次从迭代器中取值，它自然返回的是第一行，也就是通常的表头。

🧠 为什么它不是“识别”表头？
`next(i)` 不具备判断“这是不是表头”的能力。

它只是顺序地取出迭代器中的下一个元素。

是你作为程序员知道第一行是表头，所以用 `next(i)` 把它取出来、跳过。

✅ 总结一句话：
`next(i)` 返回的是迭代器的第一个元素，因为迭代器从头开始；它不知道这是表头，是你知道。
