# Python格式化输出：%s和format()用法比较

1. Python格式化输出历史起源

   Python2.5之前，我们使用的是老式格式化输出：%s。从python3.0开始起(python2.6同期发布)，同时支持两个版本的格式化，多出来的一个新版本就是利用`format()`函数，进行格式化输出。

2. 为什么要学习python3支持的新式格式化输出呢？

   虽然老式的语法，兼容性很好，但是它的功能很少，很难完成复杂的任务，而`format()`函数进行格式化输出，功能更加强大，从下面的学习中你会慢慢体会到。

## 01 基本用法

```python
a = "%s张飞%s关羽%s刘备%s赵云"  % (1, 2, 3, 4)
print(a)  # 1张飞2关羽3刘备4赵云

b = "{}张飞{}关羽{}刘备{}赵云".fromat(1, 2, 3, 4)
print(b)  # 1张飞2关羽3刘备4赵云
```

1) `format()`支持位置格式化填充，%s不支持；

* 第一种方式：

  大括号{}中写的是`format()`传入值所对应的下标。

  ```python
  c = "{3}张飞{1}关羽{2}刘备{0}赵云".format(1, 2, 3, 4)
  print(c)  # 4张飞2关羽3刘备1赵云
  ```

  

* 第二种方式：

  大括号{}中的变量，和`format()`传入值是一一对应的。

  ```python
  def my_hobbies(fruit, ball, drink):
      hobbies = "我喜欢水果{fruit}，我也喜欢球类{ball}，我还喜欢饮料{drink}".format(ball=ball, fruit=fruit, drink=drink)
      return hobbies
  
  
  fruit = "apple"
  ball = "basketball"
  drink = "milk"
  print(my_hobbies(fruit, ball, drink))  # 我喜欢水果apple，我也喜欢球类basketball，我还喜欢饮料milk
  ```

  ```python
  fruit = "apple"
  ball = "basketball"
  drink = "milk"
  hobbies = "我喜欢水果{fruit}，我也喜欢球类{ball}，我还喜欢饮料{drink}".format(ball=ball, fruit=fruit, drink=drink)
  print(hobbies)  # 我喜欢水果apple，我也喜欢球类basketball，我还喜欢饮料milk
  ```

## 02 填充和对齐

1）填充（只能用一个字符进行填充）

1. 什么是填充？

   概念：当指定了字符串最终的长度，但是现有的字符串没有那么长，那么我们就用某种字符（填充字符）来填满至这个长度，这就是“填充”。

2. `%s`：实现填充功能；

   ```python
   a = "%s" % ("张飞")
   print(a)  # 张飞
   
   b = "%10s" % ("张飞")
   print(b)  # '        张飞'
   ```

3. `format()`：实现填充功能；

   ```python
   c = "{}".format("张飞")
   print(c)  # 张飞
   
   d = "{:10}".format("张飞")
   print(d)  # '张飞        ' 
   ```

   总结如下：通过上述案例结果呈现，当使用的是%s，进行字符串填充的时候，默认是在原字符串左侧进行填充；当使用的是`format()`，进行字符串填充的时候，默认是在原字符串右侧进行填充。这就是我们下面要讲述的“对齐”。

2）对齐

1. 什么是对齐？

   