# python3 deque 双向队列创建与使用方法分析

> 这篇文章主要介绍了python3 deque 双向队列创建与使用方法，结合实例形式分析了python3 deque双向队列创建、添加、清空、拷贝等相关操作技巧与使用注意事项。

本文实例讲述了python3 deque 双向队列创建与使用方法。具体如下：

## 创建双向队列

```python
import collections
d = collections.deque()
```

## append(往右边添加一个元素)

```python
import collections
d = collections.deque()
d.append(1)
d.append(2)
print(d)  

# 输出： deque([1, 2])
```

## appendleft(往左边添加一个元素)

```python
import collections
d = collections.deque()
d.append(1)
d.appendleft(2)
print(d)

# 输出：deque([2, 1])
```

## clear(清空队列)

```python
import collections
d = collections.deque()
d.append(1)
d.clear()
print(d)

# 输出：deque([])
```

## copy(浅拷贝)

```python
import collections
d = collections.deque()
d.append(1)
new_d = d.copy()
print(new_d)

# 输出： deque([1])
```

## count(返回指定元素的出现次数)

```python
import collections
d = collections.deque()
d.append(1)
d.append(1)
print(d.count(1))

# 输出：2
```

## extend(从队列右边扩展一个列表的元素)

```pythhon
import collections
d = collections.deque()
d.append(1)
d.extend([3, 4, 5])
print(d)

# 输出：deque([1, 3, 4, 5])
```

## extendleft(从队列左边扩展一个列表的元素)

```python
import collections
d = collections.deque()
d.append(1)
d.extendleft([3, 4, 5])
print(d)

# 输出：deque([5, 4, 3, 1])
```

## index(查找某个元素的索引位置)

```python
import collections
d = collections.deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
print(d)
print(d.index('e'))
print(d.index('c', 0, 3))  # 指定查找区间

# 输出：deque(['a', 'b', 'c', 'd', 'e'])
#       4
#       2
```

## insert(在指定位置插入元素)

```python
import collections
d = collections.deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
d.insert(2, 'z')
print(d)

# 输出：deque(['a', 'b', 'z', 'c', 'd', 'e'])
```

## pop(获取最右边一个元素，并在队列中删除)

```python
import collections
d = collections.deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
x = d.pop()
print(x, d)

# 输出：e deque(['a', 'b', 'c', 'd'])
```

## popleft(获取最左边一个元素，并在队列中删除)

```python
import collections
d = collections.deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
x = d.popleft()
print(x, d)

# 输出： a deque(['b', 'c', 'd', 'e'])
```

## remove(删除指定元素)

```python
import collections
d = collections.deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
d.remove('c')
print(d)

# 输出： deque(['a', 'b', 'd', 'e'])
```

## reverse(队列反转)

```python
import collections
d = collections.deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
d.reverse()
print(d)
# 输出： deque(['e', 'd', 'c', 'b', 'a'])


```

## rotate(把右边元素放到左边)

```python
immport collections
d = collections.deque()
d.extend(['a', 'b', 'c', 'd', 'e'])
d.rotate(2)  # 指定次数，默认1次
print(d)

# 输出：deque(['d', 'e', 'a', 'b', 'c'])
```

