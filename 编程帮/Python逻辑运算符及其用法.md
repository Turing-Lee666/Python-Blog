# 打脸某些Python教程

有些不负责任的Python教程说：Python逻辑运算符用于操作bool类型的表达式，执行结果也是bool类型，这两点其实都是错误的！

Python逻辑运算符可以用来操作任何类型的表达式，不管表达式是不是bool类型；同时，逻辑运算的结果也不一定是bool类型，它也可以是任意类型。请看下面的例子：

```python
print(100 and 200)
print(45 and 0)
print("" or "http://c.biancheng.net/python/")
print(18.5 or "http://c.biancheng.net/python/")
```

运行结果：

```python
200
0
"http://c.biancheng.net/python/"
18.5
```

你看，本例中 and 和or 运算符操作的都不是bool类型表达式，操作的结果也不是bool值。

# 逻辑运算符的本质

**在Python中，and 和 or不一定会计算右边表达式的值，有时只计算左边表达式的值就能得到最终结果。**

**另外，and 和 or 运算符会将其中一个表达式的值作为最终结果，而不是将True或者False作为最终结果。**

以上两点极其重要，了解这两点不会让你在使用逻辑运算的过程中产生疑惑。

对于and运算符，两边的值都为真时最终结果才为真，但是只要其中有一个值为假，那么最终结果就是假，所以Python按照下面的规则执行and运算：

* 如果左边表达式的值为假，那么就不用计算右边表达式的值了，因为不管右边表达式的值是什么，都不会影响最终结果，最终结果都是假，此时and会把左边表达式的值作为最终结果。
* 如果左边表达式的值为真，那么最终值是不能确定的，and 会继续计算右边表达式的值，并将右边表达式的值作为最终结果。

对于or运算符，情况是类似的，两边的值都为假时最终结果才为假，只要其中有一个值为真，那么最终结果就是真，所以Python按照下面的规则执行or运算：

* 如果左边表达式的值为真，那么就不用计算右边表达式的值了，因为不管右边表达式的值是什么，都不会影响最终结果，最终结果都是真，此时or会把左边表达式值作为最终结果。
* 如果左边表达式的值为假，那么最终值是不能确定的，or会继续计算右边表达式的值，并将右边表达式的值作为最终结果。

使用代码验证上面的结论：

```python
url = "http://c.biancheng.net/cplus"

print("----False and xxx----")
print(False and url)  # False
print("----True and xxx----")
print(True and url)  # "http://c.biancheng.net/cplus"
print("----False or xxx----")
print(False or url)  # "http://c.biancheng.net/cplus"
print("----True or xxx----")
print(True or url)  # True
```

运行结果：

```python
----False and xxx----
False
----True and xxx----
http://c.biancheng.net/cplus
----False or xxx----
http://c.biancheng.net/cplus
----True or xxx----
True
```

第4行代码中，and左边的值为假，不需要再执行右边的表达式了，所以url没有任何输出。

第6行代码中，and左边的值为真，还需要执行右边的表达式才能得到最终的结果，所以url输出了一个网址。

第8、10行代码也是类似的。