# python3入门之堆（heapq）

> 堆是一个二叉树，其中每个父节点的值都小于或等于其所有子节点的值。整个堆的最小元素总是位于二叉树的根节点。python的heapq模块提供了对堆的支持。
>
> 堆数据结构最重要的特征是heap[0]永远是最小的元素

**`heapq.heappush(heap, item)`**

注：heap为定义堆，item增加的元素。将 *item* 的值加入 *heap* 中，保持堆的不变性。

```python
import heapq
h = []
heapq.heappush(h, 2)
h  # [2]
```

**`heapq.heapify(list)`**

注：将列表转换为堆。将list转换成堆，原地，线性时间内。

```python
list = [1, 2, 3, 5, 1, 5, 8, 9, 6]
heapq.heapify(list)
list  # [1, 1, 3, 5, 2, 5, 8, 9, 6]
```

**`heapq.heappop(heap)`**

注：删除最小值，因为堆的特征是heap[0]永远是最小的元素，所以一般都是删除第一个元素。弹出并返回 *heap* 的最小的元素，保持堆的不变性。如果堆为空，抛出 IndexError 。使用 heap[0] ，可以只访问最小的元素而不弹出它。

```python
list  # 这是个堆，注意一下
# [1, 1, 3, 5, 2, 5, 8, 9, 6]
heapq.heappop(list)
# 1
list  # 自动调整成新堆
# [1, 2, 3, 5, 6, 5, 8, 9]
```

**`heapq.heapreplace(heap.item)`**

注：返回并且pop堆顶最小值，推入新的item值并调整堆。删除最小元素值，添加新的元素值。弹出并返回 *heap* 中最小的一项，同时推入新的 *item*。 堆的大小不变。 如果堆为空则引发 IndexError。

```python
list
# [1, 2, 3, 5, 6, 5, 8, 9]
heapq.heapreplace(list, 99)
# 1
list
# [2, 5, 3, 9, 6, 5, 8, 99]
```

**`heapq.heappushpop(heap, item)`**

注：将 *item* 放入堆中，然后弹出并返回 *heap* 的最小元素。该组合操作比先调用 heappush() 再调用 heappop() 运行起来更有效率。 heappushpop()，它的 push/pop 组合会返回两个值中较小的一个，将较大的值留在堆中。首先判断添加元素值与堆的第一个元素值对比，如果大，则删除第一个元素，然后添加新的元素值，购置不更改堆。

```python
list
# [2, 5, 3, 9, 6, 5, 8, 99]
heapq.heappushpop(list, 6)
# 2
list
# [3, 5, 5, 9, 6, 6, 8, 99]
heapq.heappushpop(list, 1)
# 1
list
# [3, 5, 5, 9, 6, 6, 8, 99]
```

**`heapq.merge(...)`**

注：将多个堆合并

```python
list
# [3, 5, 5, 9, 6, 6, 8, 99]
h
# [1000]
for i in heapq.merge(h, list):
    print(i, end=" ")
# 3 5 5 9 6 6 8 99 1000
    
```

**`heapq.nlargest(n, heap)`**

注：查询堆中的最大元素，n表示查询元素个数

```python
list
# [3, 5, 5, 9, 6, 6, 8, 99]
heapq.nlargest(3, list)
# [99, 9, 8]
```

**`heapq.nsmallest(n, heap)`**

注：查询堆中的最小元素，n表示查询元素的个数

```python
list
# [3, 5, 5, 9, 6, 6, 8, 99]
heapq.nsmallest(3, list)
# [3, 5, 5]

```

