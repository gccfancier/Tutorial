# 题目分析
题目意思是给定数组中只有0，1，2三种元素，让我们返回新的数组，里面元素已经排好序。

### 解题思路（1）
一开始我题目没看懂，后来才发现整个数组中只有0,1,2三种数字，进行排序，如果可以用sort一句话就可以了，但是很不幸，说了不允许用sort，那么我们需要自己排序，很简单冒泡0(n2)或者快排（一般0（nlogn）），就可以了

### 解题思路（2）
因为它的所有数字只有三种，那么我们可以利用这个特性就是用0(n)的复杂度即可,扫描一遍，然后分别记录0,1,2的个数，然后在扫描一遍依次填充即可，但是这扫描了俩次，时间复杂度为0(n)

### 解题思路（3）
有什么办法只扫描一遍吗，那就是用三个指针来辅助，一个指向0位置的尾部，一个指向2的开始，一个用来扫描数组，详细见代码


