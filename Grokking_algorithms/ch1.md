#### 二分查找

```python
// list为递增数列
def binary_search(list, item):
  low = 0
  high = len(list) - 1
  
  while low <= high:
    mid = (low + high) / 2 // 这里不严谨
    guess = list[mid]
    
    if (guess == item):
      return mid
    if (guess > item):
      high = mid - 1
    else:
      low = mid + 1
return None
```



```dart
// dart 
void main() {
  for (int i = 0; i < 5; i++) {
    print('hello ${i + 1}');
  }
  
  var array = [1,3,5,6,13,26,37];
  var result = binarySearch(array, 13);
  print(result);
}

int binarySearch(array, num) {
  print('binary Search');
  
  int low = 0;
  int high = array.length - 1;
  print(low.toString() + ',' + high.toString());
  
  while(low <= high) {
    // dart 特有语法取整
    int mid = ((low + high)~/2).toInt();
    var guess = array[mid];
    
    if (guess == num) {
      return mid;
    } else if (guess < num) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }
  return 0;
}
```



#### 大O运行时间

* 算法运行时间是从增速角度来度量，大O指出了算法运行时间的增速，从而可以比较算法的操作数
* 常见的大O运行时间
  * O(log n) 对数时间，二分查找
  * O(n) 线性时间， 简单查找
  * O(n* log n) 快速排序
  * O(n^2) 选择排序
  * O(n!) 旅行商问题

  