## 题目分析：

题目让我们求二叉树的最左下树结点的值，也就是最后一行左数第一个值。

### 解题思路（1）
树的题目我们很容易想到递归，或者遍历来求，因为基于树的一些问法，我们都可以变换到遍历树然后到达那个结点再操作。那么我首先想的是用中序遍历来做，我们维护一个最大深度和该深度的结点值，由于中序遍历遍历的顺序是左-根-右，所以每一行最左边的结点肯定最先遍历到，那么由于是新一行，那么当前深度肯定比之前的最大深度大，所以我们可以更新最大深度为当前深度，结点值result为当前结点值（深度比当前记录的深度大的时候，我们才进行更新，那么更新完的result就有可能是最终求的结果），这样在遍历到该行其他结点时就不会更新结果result了。那么最后的结果result就是我们要求的结果。

### 解题思路（2）：
这道题用层序遍历更直接一些，因为层序遍历时遍历完当前行所有结点之后才去下一行，那么我们再遍历每行第一个结点时更新结果result即可，根本不用维护最大深度了，参见代码参见solution513.cpp


### *下面举一个简单例子走一遍算法帮助理解:*
给出下面例子：   
1
/\
2  3
/
4
（1）首先我们可以判断root=*1,不为空(我用*1代表指向1结点的指针，用1代表这个结点的值)
那么1进入队列
（2）进入while(!q.empty())循环，首先赋值result=1,并得到size=1(size就是每一层的个数)
 (3)然后进入while(--size>0)，这相当于对每一层的节点进行遍历操作.1结点出队列，然后判断1结点的左孩子与右孩子。不为空进入队列
 (4)size此时为0，跳出来，因为这一层就1一个结点，然后继续取出2赋值给result.这相当于进行第二层最左边的结点孩子的值给了result，依次进行下去，最终得到的结果是7