# 数组增强

## 新增数组API
### 静态方法

- Array.of(...args): 使用指定的数组项创建一个新数组
- Array.from(arg): 通过给定的类数组 或 可迭代对象 创建一个新的数组。

```javascript
const arr1 = Array.of(3, 4, 5, 6);
console.log(arr1)

// 输出：
// [3,4,5,6]

const arr2 = Array.from([5, 6, 7, 8]);
console.log(arr2)

// 输出：
// [5,6,7,8]
```
### 实例方法

- find(callback): 用于查找满足条件的第一个元素
- findIndex(callback)：用于查找满足条件的第一个元素的下标
- fill(data)：用指定的数据填充满数组所有的内容
- copyWithin(target, start?, end?): 在数组内部完成复制
    - target：开始改变数组位置
    - start？：复制的开始位置（默认为0）
    - end？：复制的结束位置
```javascript

const arr = [1,2,3,4,5,6,7,8];
const str = arr.find(item=>item>2);
console.log(str)

// 输出
// 3

const arr = [1,2,3,4,5,6,7,8];
const str1 = arr.findIndex(item=>!(item%2))
console.log(str1)

// 输出
// 1

const arr = [1, 2, 3, 4, 5, 6, 7, 8];
arr.copyWithin(3);
console.log(arr);

// 输出：
// [1, 2, 3, 1,2,3,4,5]

const arr1 = [1, 2, 3, 4, 5, 6, 7, 8];
arr1.copyWithin(3, 2);
console.log(arr1)

// 输出：
// [1, 2, 3, 3, 4, 5, 6, 7]

const arr2 = [1, 2, 3, 4, 5, 6, 7, 8];
arr2.copyWithin(3, 1, 6);
console.log(arr2)

// 输出：
// [1, 2, 3, 2, 3, 4, 5, 6]
```
- includes(data)：判断数组中是否包含某个值，使用Object.is匹配