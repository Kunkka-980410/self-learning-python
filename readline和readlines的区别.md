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
