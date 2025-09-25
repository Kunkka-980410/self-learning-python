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
