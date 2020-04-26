#### 选择排序

```python
def findSmallest(arr):
  smallest = arr[0]
  smallest_index = 0
  
  for i in range(1, len(arr)):
    if arr[i] < smallest:
      smallest = arr[i]
      smallest_index = i
    return smallest_index

def selectionSort(arr)：
	newArr = []
  for i in range(len(arr)):
    smallest = findSmallest(arr)
    newArr.append(arr.pop(smallest))
  return newArr

print(selectionSort([5,3,6,2,10]))
```

* 选择排序的时间复杂度是 O(n^2),  实际的执行次数依次为 n、n-1、n-2，总和0.5n^2, 但计算时间复杂度时通常忽略常数项