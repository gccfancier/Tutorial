### 题意
**中文描述**  
给定n个非负的整数a1, a2, ..., an, 每个整数代表一个点(i, ai).在(i, 0)到(i, ai)之间画一条线段.找出两条线段，它们与x轴共同围成一个容器，求容器最多能包含的水量.  
注意: 不可以倾斜容器，并且n至少是2  
**题意分析**  
就是找出在1-n之间的对应位置上的数与(n-1)的乘积的最大值

### 题解
**算法及复杂度(19ms)**  
这道题刚开始看的时候可能感觉比较像是一道动态规划的题目，原因是本题是最大化问题.但是仔细看了一下之后，发现所求的最大值只与容器两端的高度和两个下标之间的距离有关（如果还和中间的高度有关就比较复杂了）.既然问题被简单化了，试着去推一下题目的规律所在.  
假如从起始位置开始，两个下标分别是0和n-1，这个时候容器的装水量是n-1乘以两端的最小的高度.如果这个状态不是装水量最大的状态，下一个状态肯定会缩短底边的宽度，不妨设左右下标为left和right, 这时有三种调节的情况: 一个是left坐标增加，一个是right坐标减小，另一个是前两者同时发生.如果盲目改变left或者right并不能保证在后续过程一定能知道最大的乘积，不妨思考一下: 底边是缩小的，只有对高进行增加，才可以找到更大的面积，所以只有两种调节情况:　一个是对left和right对应高度的较小值调整(调整到对应位置)，另一种是left和right均进行调整(这种方法没有规律可循，暂时摒弃).这样，得出的结论就是: <b>每次对left或者right对应的高度较小的进行调整，如果left小就left++，如果right小，就right--，前提是保证有意义.</b>可以看出，这是一种类似贪心的思想，每次选择可能使结果达到一个更好的值，如果选择改变另一个下标，只能使结果更差.  
时间复杂度: O(n), n表示序列的长度.  
代码参见同文件夹下solution.cpp.  

### 算法正确性
**算法正确性证明**  
初始状态如图1.虚线及两个边圈起来的部分就是初始状态所选定的装水量，也就是初始的面积.  
![1](https://cloud.githubusercontent.com/assets/16068384/23757535/1765efce-0522-11e7-91e0-0223eb52f90a.png)  
根据在题解部分提到的策略，每次修改left和right对应高度较小的位置增加或者减少，这个算法每次固定较大的高，对较小的高进行收缩性质的搜索，直到找到的高比固定的高更大，如图2.  
![2](https://cloud.githubusercontent.com/assets/16068384/23757536/17692432-0522-11e7-936e-478e9eb03d41.png)  
可以证明，如果存在更大的结果，那么结果一定存在于新找到的这个范围中如图2.证明过程如下: 反证法,如果更大的结果不存在与图2所示的区域中，则最大的结果如图3所示，或者比图3面积更小.   
![3](https://cloud.githubusercontent.com/assets/16068384/23757797/c09f738a-0522-11e7-9469-73533d58faa9.png)  
容易看出，图三结果比起始的面积小，没有继续搜索的必要.所以这种假设是不正确的.  
因此，总的算法思路就是，每次把可能得到最大值的确切位置持续缩小到一个范围之内，不断重复，最后得到所有可能的结果，更新最大面积.  
**简单举个例子**  

    ```
    //输入数组
    nums = [6, 19, 18, 2], maxArea = 2 * 3 = 6
    //固定left, right --
    nums = [6, 19, 18], maxArea = max (6 * 2, maxArea) = 12
    // 固定right, left ++
    nums = [19, 18], maxArea = max(18 * 1, maxArea) = 18
    ```
