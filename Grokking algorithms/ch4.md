#### 快速排序 

##### D&C 

* divider and conquer  分而治之
* 找出基线条件与递归条件
  * 涉及数组的递归函数，基线条件通常是数组为空或只包含一个元素

```python
def quickSort(array):
  if len(array) < 2:
  	return array
  else:
    pivot = array[0]
    less = [i for i in array[1:] if i<= pivot]
    high = [i for i in array[1:] if i>pivot]
    
    return quickSort(less) + [pivot] + quickSort[high]
print quickSort([10,2,5,3])
```

##### 时间复杂度

最坏情况 O(n^2), 平均O(n*logn)  logN为层数