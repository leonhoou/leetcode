## ---快排递归

```
def partition(a, s, e):
    pivot = a[e]
    # i：待确定元素的位置
    i = s
    # j：从头到尾遍历每个元素
    for j in range(s, e):
        # 如果当前元素小，则把它放在i位置，i再+1
        if a[j] < pivot:
            a[i], a[j] = a[j], a[i]
            i += 1
    # 最后i的位置留给a[e]
    a[i], a[e] = a[e], a[i]
    return i

def quickSort1(arr, s, e):
    # 只有s<e的时候才有必要排序
    if s < e:
        idx = partition(arr, s, e)
        quickSort1(arr, s, idx-1)
        quickSort1(arr, idx+1, e)
```

## ---快排非递归
#### 重点：栈 存储排序的start和end
```
def quickSort2(arr, s, e):
    stack = []
    stack.append(s)
    stack.append(e)
    while stack:
        end = stack.pop()
        start = stack.pop()
        if start < end:
            pivot = arr[end]
            i = start
            for j in range(start, end):
                if arr[j] < pivot:
                    arr[i], arr[j] = arr[j], arr[i]
                    i += 1
            arr[i], arr[end] = arr[end], arr[i]
        '''stack.append(start)
        stack.append(i-1)
        stack.append(i+1)
        stack.append(end)'''
        stack.extend([start, i-1, i+1, end])
```
