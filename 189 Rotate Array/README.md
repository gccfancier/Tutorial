# 题目分析
题意要求我们将一个数组中的第三大的数进行返回。
如果数组中元素少于3个，那么返回最大的那个值。注意，相同元素只算一个。

### 解题思路（1）
记下最后一个数字，其他的数字向后移一位，最后把记下的数字放在开头，如此进行k次。这个解法空间复杂度为O(1)，时间复杂度O(kn)。

时间复杂度，最坏可能到0(n*n)级别，无法忍受

### 解题思路（2）
另设置一个vector，然后逐个元素添加进去，最后将这个vector赋值给nums。添加方式为将右边的k个元素添加进去，再将左边的n-k个元素添加进去。（注意k>vector长度的情况，一定要进行取余操作~）
空间复杂度为0(n)


###解题思路（3）
右旋k个数字有个等价操作，先将整个数组翻转，就是将前k个数字翻转，将剩下的数字也翻转此时数组与右旋k个数字的结果相同。这个解法空间复杂度为O(1)，时间复杂度为O(n)。代码见solution.cpp

一个例子说明一下算法3：
原数组为1，2，3，4，5 k=2
第一步先将原数组全部翻转 5,4,3,2,1
然后前k=2个数进行翻转 4,5,3,2,1
最后剩下的数进行翻转4,5,1,2,3
这样得到了我们的最终结果