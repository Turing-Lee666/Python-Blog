# 函数

==函数==是组织好的、可重复使用的、用来实现单一或相关联功能的代码段。

* 函数代码块以def关键词开头，后接函数标识符名称和圆括号()
* 任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数
* 函数的第一行语句可以选择性地使用文档字符串——用于存放函数说明
* 函数内容以冒号起始，并且缩进
* Return[expression]结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回None

## 函数的定义：

```python
def test0():
    "函数_文档字符串"
    print('函数内部')
    
print(test0.__doc__)  # 函数_文档字符串
```

若采用默认参数定义函数，调用函数时，缺省参数的值如果没有传入，则被认为是默认值：

```python
def test1(arg1='参数一', arg2='参数二'):
    print('arg1:' + arg1)
    print('arg2:' + arg2)
    
test1()  # arg1:参数一  arg2:参数二

# 默认情况下，参数值和参数名称是按函数声明中定义的顺序匹配起来的
test1('ice', 'cream')  # arg1:ice  arg2:cream
test1(arg2='cream', arg1='ice')  # arg1:ice  arg2:cream

```

==不定长参数。== 加了星号(*)的变量名会存放所有未命名的变量参数。选择不多传参数也可：

```python
def test2(*args, param):
    print(len(args))  # 4
    for arg in args:  # (1, 2, 3, 4) 
        print(arg)  # 1, 2, 3, 4 
    print(param)  # 'This is param'
    
test2(1, 2, 3, 4, param='This is param')


def test3(param, *args):
    print(param)  # 'This is param'
    print(len(args))  # 4
    for arg in args:  # (1, 2, 3, 4)
        print(arg)  #   1  2  3  4
        
# 默认情况下，参数值和参数名称是按函数声明中定义的顺序匹配起来的
test3('This is param', 1, 2, 3, 4)
```

<u>所有参数（自变量）在Python里都是按引用传递。</u>如果在函数里修改了参数，那么在调用这个函数的函数里，原始的参数也被改变了

```python
def test4(mylist):
    print(mylist)
    mylist.clear()
    print(mylist)
    
mylist = [1, 2, 3, 4]
test4(mylist)
print(mylist)

# 输出：
# [1, 2, 3, 4]
# []
# []
```

return语句[表达式]退出函数，选择性地向调用方返回一个表达式。不带参数值的return语句返回None

```python
def test5():
    return (1, 2, 3, 4)

def test6():
    return 1, 2, 3, 4

def test7():
    return [1, 2, 3, 4]

result = test5()
print(result)  # (1, 2, 3, 4)

result = test6()
print(result)  # (1, 2, 3, 4)

result = test7()
print(result)  # [1, 2, 3, 4]
```

**内部函数**。函数体内可以再定义函数：

```python
def outerFunc():
    print('Outer Function')
    def innerFunc():
        print('Inner Function')
    innerFunc()
    
outerFunc()

# 输出：
# Outer Function
# Inner Function
```



## 函数变量作用域

定义在函数内部的变量拥有一个**局部作用域**，定义在函数外的拥有**全局作用域**。

**局部变量**只能在其被声明的**函数内部访问**，而**全局变量**可以在**整个程序范围内访问**。调用函数时，所有在函数内声明的变量名称都将被加入到作用域中

```python
temp = 'ice cream'

def test8():
    "全局变量可以在整个程序范围访问"
    print(temp)
    
def test9():
    inner_temp = 'ice'
    print(inner_temp)
    
    
print(temp)  # 'ice cream'
test8()  # 'ice cream'
test9()  # 'ice'


# 局部变量只能在其被声明的函数内部访问
print(inner_temp)  # 报错 name 'inner_temp' is not defined

```



**注意**：UnboundLocalError: local variable 'xxx' referenced before assignment

字面意思：局部变量赋值前被引用
原因：局部变量与全局变量同名

**问题所在**

在python的函数中和全局同名的变量，如果你有**修改**变量的值就会变成**局部变量**，在修改之前对该变量的引用自然就会出现没定义这样的错误了，如果确定要引用全局变量，并且要对它修改，必须加上global关键字。

```python
xxx = 23
def PrintFileName(strFileName): 
    if xxx == 23:
        print(strFileName)
        xxx = 24

PrintFileName("file")
'''
Traceback (most recent call last):
  File "C:\Users\Joey Lee\Desktop\test.py", line 7, in <module>
    PrintFileName("file")
  File "C:\Users\Joey Lee\Desktop\test.py", line 3, in PrintFileName
    if xxx == 23:
UnboundLocalError: local variable 'xxx' referenced before assignment
'''
```

改正方法一：<u>如果确定要引用全局变量，并且要对它修改，必须加上global关键字。</u>

```python
xxx = 23
def PrintFileName(strFileName): 
    if xxx == 23:
        global xxx
        print(strFileName)
        xxx = 24

PrintFileName("file")  
'''
SyntaxError: name 'xxx' is used prior to global declaration
语法错误：在全局声明之前使用名称“ xxx”
'''
```

```python
xxx = 23
def PrintFileName(strFileName): 
    global xxx
    if xxx == 23:  
        print(strFileName)
        xxx = 24

PrintFileName("file")  # file
print(xxx)  # 24
```

改正方法2：

```python
xxx = 23
def PrintFileName(strFileName): 
    if xxx == 23:
        print xxx

PrintFileName("file")
```

## Python闭包（画图有助理解）

如果在一个内部函数里，对在外部作用域（但不是全局作用域）的变量进行引用，那么内部函数就被认为是闭包（closure）。一个闭包就是你调用了一个函数A，这个函数A返回了一个函数B给你。这个返回的函数B就叫做闭包。你在调用函数A的时候传递的参数就是自由变量

当一个内嵌函数引用其外部作用域的变量，我们就会得到一个闭包。总结一下，创建一个闭包必须满足以下几点：

1. 必须有一个内嵌函数
2. 内嵌函数必须引用外部函数中的变量
3. <u>外部函数的返回值必须是内嵌函数</u>

```python
def A(x):
    def B():
        print(x)
    return B  <--

A(7)()  # 先调用A(7)得到的返回值是B函数，然后A(7)()就是调用B()  

'''结果：
7
'''
```

```python
def FuncX(x):
    def FuncY(y):
        return x * y
    return FuncY

tempFunc = FuncX(3)  # tempFunc是临时变量，更好理解  tempFunc就是FuncY函数
result = tempFunc(5)
print(result)  # 15

result = FuncX(3)(5)  # 先FuncX(3)，再FuncX(3)(5)
print(result)  # 15

```

## 匿名函数

Python使用lambda表达式来创建匿名函数

* lambda只是一个表达式，函数体比def简单很多
* lambda的主体是一个表达式，而不是一个代码块。仅仅能在lamdba表达式中封装有限的逻辑进去
* lambda函数拥有自己的名字空间，且不能访问自有参数列表之外或全局名字空间里的参数
* 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率

lambda函数的语法只包含一个语句：`lambda [arg1 [, arg2,......, argn]]:expression`

使用如下：

```python
square = lambda x: x**2
print(square(3))  # 9

sum = lambda x, y: x + y
print(sum(2, 3))  # 5
```

## 内置函数filter的使用：

`filter(function, iterable)`

function参数可传入None、函数、lamdba表达式，iterable参数传入一个可迭代对象。

若function参数为None：返回可迭代对象中所有不为False的元素

若function参数为函数或lambda表达式：返回 <u>将可迭代对象中的元素作为函数参数，函数返回值为True</u> 的元素 

```python
result = filter(None, [1, 0, False, True])  # 1, True
print(list(result))  # [1, True]

def odd(num):
    return num % 2  # %: 取模 - 返回除法的余数

result = filter(odd, range(10))  
# 0 % 2 = 0  1 % 2 = 1  2 % 2 = 0  3 % 2 = 1  4 % 2 = 0  5 % 2 = 1  ...  9 % 2 = 1
print(list(result))  # [1, 3, 5, 7, 9]
```

