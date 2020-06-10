# Python3 字典 items() 方法

Python 字典 items() 方法==以列表返回可遍历的(键, 值) 元组数组。==

`dict.items()`

例1.

```python
#!/usr/bin/python3
 
dict = {'Name': 'Runoob', 'Age': 7}
 
print ("Value : %s" %  dict.items())  # Value : dict_items([('Name', 'Runoob'), ('Age', 7)])
```

例2. 遍历例子：

```python
dict = {'Name': 'Runoob', 'Age': 7}
for i,j in dict.items():  # for i, j in dict_items([('Name', 'Runoob'),('Age', 7)]):
    print(i, ":\t", j)
    # Name :   Runoob
    # Age :    7
      
```

例3. 将字典的 key 和 value 组成一个新的列表：

```python
d={1:"a",2:"b",3:"c"}
result=[]
for k,v in d.items():  # for k,v in dict_items([(1,"a"),(2,"b"),(3,"c")]):
    result.append(k)  # [1] [1,"a",2] [1,"a",2,"b",3]
    result.append(v)  # [1,"a"] [1,"a",2,"b"] [1,"a",2,"b",3,"c"]

print(result)  # [1, 'a', 2, 'b', 3, 'c']
```

