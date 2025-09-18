正则表达式（Regular Expression）是一种用于匹配字符串模式的强大工具，尤其在文本处理、数据清洗、日志分析等场景中非常有用。Python 中通过内置的 re 模块来使用正则表达式。

🧠 正则表达式的核心概念
正则表达式是一种小型语言，用来描述字符串的结构。你可以用它来：
检查字符串是否符合某种格式（如邮箱、手机号）
提取字符串中的特定内容（如日期、数字）
替换或分割字符串中的内容

✅ 常用语法速查表

|表达式|	含义| |
|:---|:---|:---|
|.|	匹配任意字符（除换行符）|
|\d|	匹配数字（0-9）|
|\w|	匹配字母、数字或下划线|
|\s|	匹配空白字符（空格、换行等）|
|^|	匹配字符串开头|
|$|	匹配字符串结尾|
|*|	匹配前一个字符零次或多次|
|+|	匹配前一个字符一次或多次|
|?|	匹配前一个字符零次或一次|
|{n}|	匹配前一个字符恰好 n 次|
|{n,m}|	匹配前一个字符 n 到 m 次|
|[]|	匹配字符集合，如 [abc] 匹配 a、b 或 c|
|[^...]|	匹配不在集合中的字符|
|`|	`|	或操作，如 `cat	dog` 匹配 cat 或 dog|
|()|	分组，提取匹配内容|


```python
import re
# 匹配手机号
pattern = r"^1[3-9]\d{9}$"
phone = "13812345678"
print(re.match(pattern, phone))  # 输出：<re.Match object...>

# 提取所有数字
text = "价格是：￥88，折扣后是￥66"
numbers = re.findall(r"\d+", text)
print(numbers)  # 输出：['88', '66']

# 替换邮箱域名
email = "user@example.com"
new_email = re.sub(r"@.*", "@newdomain.com", email)
print(new_email)  # 输出：user@newdomain.com
```


---
用
```text
"Donor1_IVD1_AF"	"Donor1_IVD1_NP"	"Donor1_IVD2_AF"	"Donor1_IVD2_NP"	"Donor2_IVD1_AF"	"Donor2_IVD1_NP"	"Donor2_IVD2_AF"	"Donor2_IVD2_NP"	"Donor3_IVD1_AF"	"Donor3_IVD1_NP"	"Donor3_IVD2_AF"	"Donor3_IVD2_NP"	"Donor4_IVD1_AF"	"Donor4_IVD1_NP"	"Donor4_IVD2_AF"	"Donor4_IVD2_NP"	"Donor5_IVD1_AF"	"Donor5_IVD1_NP"	"Donor5_IVD2_AF"	"Donor5_IVD2_NP"	"Donor6_IVD1_AF"	"Donor6_IVD1_NP"	"Donor6_IVD2_AF"	"Donor6_IVD2_NP"	"Donor7_IVD1_AF"	"Donor7_IVD1_NP"	"Donor8_IVD1_AF"	"Donor8_IVD1_NP"	"Donor9_IVD1_AF"	"Donor9_IVD1_NP"	"Donor11_IVD1_AF"	"Donor11_IVD1_NP"	"Donor70_IVD1_NP"	"Donor70_IVD1_AF"	"Donor81_IVD1_AF"	"Donor81_IVD1_NP"	"Donor100_IVD1_NP"	"Donor100_IVD1_AF"	"Donor106_IVD1_NP"	"Donor106_IVD1_AF"	"Donor136_IVD1_NP"	"Donor136_IVD1_AF"	"Donor147_IVD1_NP"	"Donor147_IVD1_AF"	"Donor172_IVD1_NP"	"Donor172_IVD1_AF"	"Donor246_IVD1_NP"	"Donor246_IVD1_AF"
```

来替换
```text
"GSM1725780"	"GSM1725781"	"GSM1725782"	"GSM1725783"	"GSM1725784"	"GSM1725785"	"GSM1725786"	"GSM1725787"	"GSM1725788"	"GSM1725789"	"GSM1725790"	"GSM1725791"	"GSM1725792"	"GSM1725793"	"GSM1725794"	"GSM1725795"	"GSM1725796"	"GSM1725797"	"GSM1725798"	"GSM1725799"	"GSM1725800"	"GSM1725801"	"GSM1725802"	"GSM1725803"	"GSM1725804"	"GSM1725805"	"GSM1725806"	"GSM1725807"	"GSM1725808"	"GSM1725809"	"GSM1725810"	"GSM1725811"	"GSM1725812"	"GSM1725813"	"GSM1725814"	"GSM1725815"	"GSM1725816"	"GSM1725817"	"GSM1725818"	"GSM1725819"	"GSM1725820"	"GSM1725821"	"GSM1725822"	"GSM1725823"	"GSM1725824"	"GSM1725825"	"GSM1725826"	"GSM1725827"
```
并且在每个双引号之间加逗号，避免被pd识别成一维数组，无法替换更名
```python
import re

input_string = '''"Donor1_IVD1_AF" "Donor1_IVD1_NP" "Donor1_IVD2_AF" "Donor1_IVD2_NP" "Donor2_IVD1_AF" "Donor2_IVD1_NP" "Donor2_IVD2_AF" "Donor2_IVD2_NP" "Donor3_IVD1_AF" "Donor3_IVD1_NP" "Donor3_IVD2_AF" "Donor3_IVD2_NP" "Donor4_IVD1_AF" "Donor4_IVD1_NP" "Donor4_IVD2_AF" "Donor4_IVD2_NP" "Donor5_IVD1_AF" "Donor5_IVD1_NP" "Donor5_IVD2_AF" "Donor5_IVD2_NP" "Donor6_IVD1_AF" "Donor6_IVD1_NP" "Donor6_IVD2_AF" "Donor6_IVD2_NP" "Donor7_IVD1_AF" "Donor7_IVD1_NP" "Donor8_IVD1_AF" "Donor8_IVD1_NP" "Donor9_IVD1_AF" "Donor9_IVD1_NP" "Donor11_IVD1_AF" "Donor11_IVD1_NP" "Donor70_IVD1_NP" "Donor70_IVD1_AF" "Donor81_IVD1_AF" "Donor81_IVD1_NP" "Donor100_IVD1_NP" "Donor100_IVD1_AF" "Donor106_IVD1_NP" "Donor106_IVD1_AF" "Donor136_IVD1_NP" "Donor136_IVD1_AF" "Donor147_IVD1_NP" "Donor147_IVD1_AF" "Donor172_IVD1_NP" "Donor172_IVD1_AF" "Donor246_IVD1_NP" "Donor246_IVD1_AF"'''

# 使用三引号 '''...''' 是为了方便写多行字符串

# 提取所有列名
column_names = re.findall(r'"([^"]*)"', input_string)

# 生成带逗号的列表
result_with_commas = ', '.join([f'"{name}"' for name in column_names])

print(result_with_commas)
```
✅ 步骤二：重命名表达矩阵的列
如果你的表达矩阵 df 当前列数与 column_names 长度一致，可以直接替换：

```python
df.columns = column_names
```

---
🔍 代码逐行解析
1️⃣
```python
import re
```
导入 Python 的正则表达式模块 re，这是处理字符串模式匹配的标准库。

2️⃣ 
```python
input_string = '''...'''
```
这是你的原始字符串，包含多个样本名，每个样本名都被双引号包裹，并用制表符或空格分隔。使用三引号 '''...''' 是为了方便写多行字符串。

3️⃣
```python
column_names = re.findall(r'"([^"]*)"', input_string)

```
这是核心正则表达式部分，解释如下：

✅ 正则表达式：r'"([^"]*)"'
r"..."：表示这是一个原始字符串，避免反斜杠被 Python 解释。

"([^"]*)"：

外层的双引号 " 是匹配你原始字符串中的引号。

[^"]* 是一个字符类，表示匹配任意数量的非双引号字符。

(...) 是一个捕获组，表示我们只想提取引号内的内容。

✅ 举例说明：
对于 "Donor1_IVD1_AF"，这个表达式会提取出 Donor1_IVD1_AF，去掉引号。

最终 column_names 是一个列表，像这样：

```python
['Donor1_IVD1_AF', 'Donor1_IVD1_NP', 'Donor1_IVD2_AF', ...]
```

4️⃣
```python
result_with_commas = ', '.join([f'"{name}"' for name in column_names])

```
这一步是格式化输出：

把每个列名重新加上双引号（用 f'"{name}"'）

然后用逗号和空格连接起来，形成一行合法的 Python 列表格式

输出结果是：

```python
"Donor1_IVD1_AF", "Donor1_IVD1_NP", "Donor1_IVD2_AF", ...
```
5️⃣ 
```python
print(result_with_commas)
```
打印出你格式化后的列名字符串，可以直接复制到代码中作为 df.columns = [...] 使用。
