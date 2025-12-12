# 二叉树 Binary Tree

## 1.树的基本概念


![82a0684323c0ef28ffd04dd99ed97984.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeCxpOmu2m2UxFPObOmr9DJpgrKxndgACNBsAAm312FXD3N1I__8CnjYE.png)

`节点的度`：一个节点含有的子树的个数称为该节点的度； 如上图：A的为6，D为1，E为2，F为3等等

`叶节点或终端节点`：度为0的节点称为叶节点； 如上图：B、C、H、I…等节点为叶节点

`非终端节点或分支节点`：度不为0的节点； 如上图：D、E、F、G…等节点为分支节点

`双亲节点或父节点`：若一个节点含有子节点，则这个节点称为其子节点的父节点； 如上图：A是B的父节点，A都是BCDEFG的父节点

`孩子节点或子节点`：一个节点含有的子树的根节点称为该节点的子节点； 如上图：B是A的孩子节点，BCDEFG都是A的子节点

`兄弟节点`：具有相同父节点的节点互称为兄弟节点； 如上图：B、C、D、E、F、G是兄弟节点

`树的度`：一棵树中，最大的节点的度称为树的度； 如上图：树的度为6

`节点的层次`：从根开始定义起，根为第1层，根的子节点为第2层，以此类推；

`树的高度或深度`：树中节点的最大层次； 如上图：树的高度为4

`堂兄弟节点`：双亲在同一层的节点互为堂兄弟；如上图：H、I互为兄弟节点

`节点的祖先`：从根到该节点所经分支上的所有节点；如上图：A是所有节点的祖先
自己是否是自己的祖先需要看题目给的条件。

`子孙`：以某节点为根的子树中任一节点都称为该节点的子孙。如上图：所有节点都是A的子孙

`森林`：由m（m>0）棵互不相交的树的集合称为森林；
并查集就是一棵森林

## 2.二叉树

### 2.1.二叉树的基本概念

![78be8795f593285fc5844ada2fce6b3d.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeIVpOm8j0yjM272M-YLO6fmCC72ovgAClRsAAm312FVuxIJY2vA1YDYE.png)

二叉树是树的子集(即二叉树是特殊的树)。<br/>
树（Tree）：是 n（n≥0）个节点的有限集合，有且仅有一个根节点，其余节点可分为若干个互不相交的子树。对节点的子节点数量没有上限，一个节点可以有 0、1、2… 甚至多个子节点。<br/>
二叉树（Binary Tree）：是树的特殊形式，严格限制每个节点的子节点数量最多为 2 个，并且明确区分左子节点和右子节点（顺序不可颠倒）<br/>

它是由节点组成的。每个节点包含三个部分：一个数据域，以及两个指向其他节点的指针，分别代表左子树和右子树。如果一个节点的左子树和右子树都为空，那么这个节点被称为叶节点。（对于指针、节点的对应关系疑惑的等下文解释）

所以树的所有概念都可以放在二叉树上。要辨别是否满足二叉树很简单，所有结点数量均<=2个的就是了<br/>

<note>新增概念</note>
若是二叉树的情况下，我们就可以用左节点右节点去称呼子节点了。如4和5是2的子节点，且4是2的左子节点，5是2的右子节点。

![ScreenShot_2025-12-11_152049_703.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeMRpOnDoXBlsviXzK_9aSQrsm0FaNAAC1xsAAm312FVXrhbFk2vA4DYE.png)

题中有时也称左子树右子树，就是指该节点左下侧的所有节点集合，右子树亦然。


![fbc53e7467d9240a7daa50cbdd6565bd.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeMxpOnGnOvzuMj0w94d_ZrWy6AKR7wAC4xsAAm312FUSsSXejL_1TTYE.png)

我们通过上述二叉树的规律也易得，所有二叉树均由上图的5种情况所构成。

节点(Node):
```C++
typedef struct Node {
    int data;           // 数据域
    struct Node* left;  // 左子树指针
    struct Node* right; // 右子树指针
} Node;
```

度(Degree)
```C++
int degree(Node* node) {
    if (node == NULL) return 0;
    int degree = 0;
    if (node->left != NULL) degree++;
    if (node->right != NULL) degree++;
    return degree;
}
```

高度和深度 (Height and Depth)<br/>
高度是指从某节点到其最远叶子节点的最长路径上的边数。树的高度是其根节点的高度。深度是指从根节点到某节点的路径上的边数。
```C++
int height(Node* node) {
    if (node == NULL) return -1; // 空树的高度定义为-1
    int leftHeight = height(node->left);
    int rightHeight = height(node->right);
    return max(leftHeight, rightHeight) + 1;
}

int depth(Node* node, Node* target, int level) {
    if (node == NULL) return -1;
    if (node == target) return level;
    int leftDepth = depth(node->left, target, level + 1);
    if (leftDepth != -1) return leftDepth;
    return depth(node->right, target, level + 1);
}
```

### 2.2.特殊的二叉树

![8a12c4086be5cd46c4e16d21940f8a6d~tplv-be4g95zd3a-image.jpeg](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeNVpOnJGEFtEjEV5q1hmBkx_2cSVXQAC6hsAAm312FUOc6wtUcP_eDYE.jpeg)

满二叉树：一个二叉树，如果每一个层的结点数都达到最大值，则这个二叉树就是满二叉树。也就是说，如果一个二叉树的层数为K，且结点总数是2^k - 1 ，则它就是满二叉树。

![21e36981dca3303a02571946159bc68d~tplv-be4g95zd3a-image.jpeg](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeNZpOnJlUoKtRyb38muuwK1DyjKiggAC6xsAAm312FV1m8fzSMjzTzYE.jpeg)

完全二叉树：完全二叉树是效率很高的数据结构，完全二叉树是由满二叉树而引出来的。对于深度为K的，有n个结点的二叉树，当且仅当其每一个结点都与深度为K的满二叉树中编号从1至n的结点一一对应时称之为完全二叉树。

要注意的是满二叉树是一种特殊的完全二叉树。

![v2-2b57e62bf9460ad81d52bd588c448e46_1440w.jpg](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeOppOnP9UPsd3MyKOi1q1BIq_085pQAC-xsAAm312FV9HwYg4Wwg5zYE.jpg)

要会判别是否属于完全二叉树，上图能理解就说明能知道是不是完全二叉树了。

### 2.3.二叉树的性质

![1475571-20190513204544289-1444996969.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeTBpOnos_rW2b07aW-Kyl8ynnnn7JgACRhwAAm312FU68xB2tj1a8TYE.png)

上图均可用数学去推理。

### 2.4.二叉树用代码如何表示

#### 2.4.1 二叉树的数组存储方式

![1475571-20190513204715802-335272765.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeVZpOnu87si6J23FUcG6ukypGoHylAACaRwAAm312FXcMUjAWeQTSDYE.png)

遇到空子树，应在编号时假定有此子树进行编号，而在顺序存储时当作有此子树那样把位置留出来。这样才能反映二叉树结点之间的相互关系，由其存储位置找到它的父结点、子女、兄弟结点的位置。但这样做有可能会消耗大量的存储空间。例如：单支二叉树，会浪费很多空间。

![1475571-20190513204730862-213431924 (1).png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeaJpOoRrsYUu4ZS37ds6J2wFx7otwgACtBwAAm312FWY2HvVLUa99TYE.png)

如果根节点编号是从1开始有有以下结论：<br/>
中间节点一定在倒数第二层，最后一个节点的数就是总节点的个数，总结点数除2就是中间节点的数的个数，父节点的节点数*2<总节点个数，当前节点一定有两个孩子，如果=就只有一个孩子，如果<就没有一个孩子。


#### 2.4.2.二叉树的链表存储方式

![1475571-20190513204755452-1436072926.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMeaNpOoSuMdi4Wnnqqz0AAV8f3JH8txIAArUcAAJt9dhVbZdAdjU1ryY2BA.png)

### 2.5.二叉树的遍历

记忆诀窍：先记住原始的“左右”，然后前(序)、中(序)、后(序)是针对“中”这个字来说的，前序就是中字在前面，形成中左右.

```C++
        A
       / \
      B   C
     / \ / \
    D  E F  G
```

以上面二叉树为例，前序结果：ABDECFG; 中序结果：DBEACFG; 后序结果：DEBFGCA;

#### 2.5.1.前序遍历(Preorder Traversal)

遍历的顺序为中左右.

前序遍历是一种深度优先的遍历方法，它首先访问根节点，然后递归地访问左子树，最后访问右子树。这种遍历方法的一个典型应用是打印一个结构化的文档。

```C++
void preorderTraversal(struct TreeNode* root) {
    if (root == NULL) return;
    printf("%d ", root->val);  // 访问根节点
    preorderTraversal(root->left);  // 递归访问左子树
    preorderTraversal(root->right);  // 递归访问右子树
}
```

#### 2.5.2.中序遍历(Inorder Traversal)

遍历的顺序为左中右

中序遍历首先递归地访问左子树，然后访问根节点，最后访问右子树。对于二叉搜索树，中序遍历的结果是`按照升序排列`的。

```C++
void inorderTraversal(struct TreeNode* root) {
    if (root == NULL) return;
    inorderTraversal(root->left);  // 递归访问左子树
    printf("%d ", root->val);  // 访问根节点
    inorderTraversal(root->right);  // 递归访问右子树
}
```

#### 2.5.3.后序遍历(PostOrder Traversal)

遍历的顺序为左右中；

后序遍历先递归地访问左子树，然后访问右子树，最后访问根节点。这种遍历方法`常用于树的删除操作`。

```C++
void postorderTraversal(struct TreeNode* root) {
    if (root == NULL) return;
    postorderTraversal(root->left);  // 递归访问左子树
    postorderTraversal(root->right);  // 递归访问右子树
    printf("%d ", root->val);  // 访问根节点
}
```

#### 2.5.4.层次遍历(Level Order Traversal)

层序遍历从根节点开始，逐层访问树中的每个节点。这通常通过使用队列来实现。

```C++
void levelOrderTraversal(struct TreeNode* root) {
    if (root == NULL) return;
    struct Queue* queue = createQueue();  // 创建一个队列
    enqueue(queue, root);  // 将根节点入队
    while (!isQueueEmpty(queue)) {
        struct TreeNode* node = dequeue(queue);  // 出队一个节点
        printf("%d ", node->val);  // 访问当前节点
        if (node->left != NULL) enqueue(queue, node->left);  // 左子节点入队
        if (node->right != NULL) enqueue(queue, node->right);  // 右子节点入队
    }
    deleteQueue(queue);  // 删除队列
}
```

这段代码使用了一个队列来实现层序遍历。首先将根节点入队，然后在循环中反复出队节点并将其子节点入队，直到队列为空。