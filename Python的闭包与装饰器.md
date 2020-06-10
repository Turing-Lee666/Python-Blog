# 闭包

内部函数对外部函数作用域里变量的引用

闭包内的闭包函数（内部函数）私有化了变量，完成了数据的封装，类似于面向对象

```python
def func():  # 外部函数
    a = 1  # 外部函数作用域里的变量
    print("this is func.")
    def func1(num):  # 内部函数
        print("this is func1")
        print(num + a)
    return func1  # 返回func1函数本身
      
var = func()  # var = func1  
# var()  # 调用func1函数  
var(3)  # 4
```

函数内的变量（属性），都是有生命周期的，生命周期都是在函数执行期间

```python
# 作用域
def func():
    a = 1
    
func()
print(a)  # 函数内的东西只有在函数运行期间他才会存活
```

怎么去实现一个闭包函数？

```python
mylist = [1, 2, 3, 4, 5]

def func(obj):
    print('func:', obj)
    def func1():
        obj[0] += 1  # 列表索引可以修改对应位置上的值
        print('func1:', obj)
    return func1  # 让外部函数返回内部函数即可  这就是一个闭包

# 调用func()，传入一个列表mylist，返回函数func1  即var = func1，这样var就成了一个函数
var = func(mylist)  
# 调用var函数
var()  
var()
var()
# var: obj  print('func1:', obj)


```

作用域

装饰器，语法糖 @

# 装饰器

装饰器所存在的意义：不影响原有函数的功能，还能添加新的功能

```python
# 在执行func的时候，首先会执行func1中的内容
@func1  # 这算是装饰器函数
def func():
    print('aaa')
```

一般常见于当拿到了第三方$API$，人家的$API$是不允许修改的。如果觉得这个$API$写的特别简陋，需要添加某些功能，那么就可以使用装饰器

装饰器基于闭包

普通装饰器

```python
def func1(func):  # 函数func1接收的参数是一个函数func  这里的func函数其实就是下面的myprint函数  外部闭包函数的参数是被装饰的函数对象
    def func2():
        print('aaabbb')
        return func()  # 返回了外部函数接收的被装饰函数myprint的调用
    return func2  

# return func  # 返回了函数对象
# return func()  # 返回的是一个函数调用，其实真正意义上返回的是函数执行完成之后的结果
# 1. func1(myprint) --> func2
# 2. func2() --> print('aaabbb')  return func()
@func1  # @func1 <==> func1(myprint)()  # 接收被装饰的函数作为参数，而且还要继续调用一次  有两个函数调用
def myprint():
    print('你好，我是print')

 myprint()  # 执行func1(myprint)()     
```
装饰器函数带参数：多一层包装来接收装饰器的参数
```python
# 构建一个装饰器
def arg_func(sex):
    def func1(b_func):  # 传的是装饰器装饰的函数man或者woman
        def func2():
            if sex == 'man':
                print('你不可以生娃')
            if sex == 'woman':
                print('你可以生娃')
            return b_func()
        return func2  # 让外部函数返回内部函数即可  这就是一个闭包
    return func1

# arg_func(sex='man') --> func1
# arg_func(sex='man')(man) --> func1(man) --> func2
# arg_func(sex='man')(man)() --> func1(man)() --> func2() -->man()
@arg_func(sex='man')
def man():
    print('好好上班。')
    
@arg_func(sex='woman')    
def woman():
    print('好好上班。')
    
# arg_func(sex='man') --> func1
# arg_func(sex='man')(man) --> func1(man) --> func2
# arg_func(sex='man')(man)() --> func1(man)() --> func2() -->man()
man()  
woman()  
```

被装饰的函数带参数：只需要在最内部函数传入参数即可

```python
# 先写出来一个装饰器
def func1(func):  # 外部装饰器函数func1接收mysum作为参数传递进来
    def func2(x, y):  # x, y就是func的参数  mysum的参数会被内部真正的这个闭包函数所接收到
        print(x, y)
        x += 5
        y += 5
        return func(x, y)  # 在内部函数调用被装饰的函数
    return func2

@func1
def mysum(a, b):  # a = a + 5  b = b + 5
    print(a + b)
```



