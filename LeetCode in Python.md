# 简单

### 1 两数之和

> 给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

函数中的 `:` 与 `->` 是一种注释，冒号说明输入参数的类型，箭头说明输出结果的类型，仅仅只是为了阅读方便，并不会强制变量转型。

#### 暴力穷举

首先尝试暴力求解：对每个数做减法，判断差值是否存在于列表内。

`注意返回的下标不能相等，保证取出两个整数。`

~~~python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            if target-nums[i] in nums and i != nums.index(target-nums[i]):
                return [i,nums.index(target-nums[i])]
~~~

**复杂度分析**

- 时间复杂度：
- 空间复杂度：

#### 穷举优化

在穷举的基础之上，不需要每次都从 nums 全部查找一遍，只需要从 num1 的之前或之后找就可以了，为了节省时间，这里以在后面的列表中寻找为例。

`列表的 index 方法有三个参数，list.index(x[, start[, end]])，后面两个可选参数指定查找范围，避免重复使用同一元素`

~~~python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            if target-nums[i] in nums[i+1:]:
                return [i,nums.index(target-nums[i],i+1)]
~~~

复杂度分析



#### Hash

使用字典模拟哈希表进行快速查询，通过一遍哈希表，能够在哈希表中快速定位已走过的第二个数。相比于暴力穷举，哈希表、不是每一次循环都对所有的列表元素进行搜索，而是只关注添加过的字典元素，只有当 num1 被添加后，随着搜索范围的扩大，在 num2 的循环内，才能完成问题的求解。

`字典（HashMap）相比于列表，在访问速度上确实有着不可比拟的优越性`

`enumerate 方法返回一个由包含元素下标和列表元素的二元数组构成的列表，该方法在此类解题方法中广泛运用`

~~~python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
            for i,num in enumerate(nums):
                if target-num not in hashmap:
                    hashmap[num] = i
                else:
                    return [hashmap[target-num],i]
~~~

其精简版本如下

`添加哈希表元素放在循环指令的最后一步，避免了自身相加的情况`

~~~python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i,num in enumerate(nums):
            if (target-num) in hashmap:
                return [i,hashmap[target-num]]
            hashmap[num] = i
~~~

复杂度分析：

