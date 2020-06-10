# Python布尔

### 布尔表示两值之一：True或False。

## 布尔值

在编程中，您通常需要知道表达式是True还是False。

您可以计算Python中的任何表达式，并获得两个答案之一，即True或False。

比较两个值时，将对表达式求值，python返回布尔值答案：

### 实例

```python
print(8 > 7)  # True
print(8 == 7)  # False
print(8 < 7)  # False
```

<u>当在if语句中运行条件时，Python返回True或False：</u>

### 实例

根据条件是对还是错，打印一条消息：

```python
a = 200
b = 33

if b > a:
    print("b is greater than a")
else:
    print("b is not greater than a")  # b is not greater than a
```

## <u>评估值和变量</u>

<u>bool()函数可让您评估任何值，并为您返回True或False。</u>

### 实例

评估字符串和数字：

```python
print(bool("Hello"))  # True
print(bool(10))  # True
```

### 实例

评估两个变量：

```python
x = "Hello"
y = 10

print(bool(x))  # True
print(bool(y))  # True
```

## 大多数值都为True

==如果有某种内容，则几乎所有值都将评估为True。==

除空字符串外，任何字符串均为True。

除0外，任何数字均为True。

除空列表外，任何列表、元组、集合和字典均为True。

### 实例

下例将返回True:

```python
bool("abc")  # True
bool(123)  # True
bool(["apple", "cherry", "banana"])  # True
```

## 某些值为False

实际上，除空值（例如()、[]、{}、""、数字0和值None）外，没有多少值会被评估为Flase。当然，值False的计算结果为False。

### 实例

下例会返回False:

```python
bool(False)
bool(None)
bool(0)
bool("")
bool(())
bool([])
bool({})
```

在这种情况下，一个值或对象的计算结果为False,即如果对象由带有`__len__`函数的类生成的，且该函数返回0或False：

### 实例

```python
class myclass():
    def __len__(self):
        return 0
    
myobj = myclass()
print(bool(myobj))  # False
```

## 函数可返回布尔

Python还有很多返回布尔值的内置函数，例如`isinstance()`函数，该函数可用于确定对象是否具有某种数据类型：

### 实例

检查对象是否是整数：

```python
x = 200
print(isinstance(x, int))  # True
```





