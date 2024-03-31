## 树的旋转

<img src="../images/AVL(1).png">

从这个操作图中可以看出，当树进行旋转时，子节点的子树和连接到父节点上，然后父节点会转到子节点空出来的子节点的位置，所以可以看出这个操作是有三步(以左旋为例)：

1.子节点（B）的右子树连接到父节点（A）对应的位置

2.将父节点（A）连接到子节点(B)的对应位置

3.将子节点（现在的父节点，就是B）连接到之前父节点在祖先节点对应的位置（图中没有画出这步）

这样这个树的旋转操作就做好了。接下来会给出这个树的旋转的代码：
### 树的左旋
```
Tree LLretation(Tree top){
    Tree a=top->left;
    top->left=a->right;
    a->right->head=top;
    a->right=top;
    a->head=top->head;
    top->head=a;
    top->height=max(Gheight(top->left),Gheight(top->right))+1;
    a->height=max(Gheight(a->left),top->height)+1;
    //printf("1 ");
    return a;
}
```
### 树的右旋
```
Tree RRretation(Tree top){
    Tree a=top->right;
    top->right=a->left;
    a->left->head=top;
    a->left=top;
    a->head=top->head;
    top->head=a;
    top->height=max(Gheight(top->left),Gheight(top->right))+1;
    a->height=max(top->height,Gheight(a->right))+1;
    return a;
}
```

## AVL树
现在我们就可以说一下AVL树的定义了。

首先AVL树定义了一个平衡因子（balance factor,简称BF），就是用一个节点的左子树的高度减去右子树的高度：可以写成一下公式：

BF(node)=height(node->left)-height(node->right)

AVL树的定义要求这个树的每一个节点都是平衡的，就是每一个节点的左子树和右子树的高度差的绝对值至多为1(BF(node)=0，1，-1)。所以当插入一个新的节点导致节点左右不平衡时就会出现以下四种情况：

1.RRretation
<img src="../images/AVL(2).png">
进行一次右旋即可。

2.LLretation

<img src="../images/AVL(3).png">

进行一次左旋即可。

3.LRretation

<img src="../images/AVL(4).png">

这个情况需要进行一次左旋和一次右旋操作。
```
Tree LRretation(Tree top){
    top->left=RRretation(top->left);
    return LLretation(top);
}
```
4.RLretation

<img src="../images/AVL(5).png">
这个情况需要进行一次右旋和一次左旋操作。
```
Tree RLretation(Tree top){
    top->right=LLretation(top->right);
    return RRretation(top);
}
```

### 时间复杂度分析

首先我们需要知道建立一个高为h的AVL树所需要的最小的节点数（这个为什么呢？应该比较好理解吧）设它的节点数为Nh

Nh=Nh-1+Nh-2+1 (h>=2,N0=0,N1=1)

本算式可以看到它的递归关系是和斐波那契数列相似。
<img src="../images/AVL(6).png">
所以说这个算法的时间复杂度为O(logN)

## Splay tree( 拓展树 )

在我看来，这个算法就是纯纯为了提高搜索效率的算法，所以在我们看来就是直接将这次搜索到的东西放到开头就可以了，但是这个会出现如下的问题：
<img src="../images/splay(1).png">
所以不能只是一味的将搜到的节点放到第一个。

### 查找

Splay tree算法就出现了，它的核心想法就是将节点所处状况进行分类(x为我们想要找到的节点，p为它的父节点，如果它存在祖先节点，就假设G为它的祖先节点)：

1.不存在祖先节点：直接用一次左旋或者一次右旋

2.Zig-zag：进行两次不同的旋转

3.Zig-zig：进行两次相同的左（右）旋
<img src="../images/splay(2).png">
(这个算法就是在查找时进行的，所以在插入时没有)

```
Tree find(Tree top,elementtype a){
    if(top->data>a) find(top->right,a);
    if(top->data<a) find(top->left,a);
    while(top->head){
        if(top->data==a){
            if(top->head==top->head->head->left&&top==top->head->right){
                top=LRrotation(top->head->head);
            }else if(top->head==top->head->head->left&&top==top->head->left){
                LLrotation(top->head->head);
                top=LLrotation(top->head);
            }else{
                if(top==top->head->left){
                    top=LLrotation(top->head);
                }else{
                    top=RRrotation(top->head);
                }
            }
        }
    }
    return top;
}
```

### 删除

删除的时候其实就是先要这个节点，所以就按照查找的方式来将这个节点放到根节点，但是之后应该怎么搞呢？

<img src="../images/splay(3).png">

## Amortized Analysis(摊还分析)

如果你仔细阅读了我的这篇文章的话，你会发现我并没有分析拓展树的时间复杂度，是我忘了吗？

你说的对，但是我只是想留到现在再来进行分析。由于我们无法严格的限制每次操作的时间复杂度，所以我们无法通过累和的方式得到这个算法的综合时间复杂度，所以我们可以适当放宽对于时间复杂度的限制，即可以通过累计多次操作之后获得过累计的时间复杂度，从而可以算出平均每次操作的时间复杂度。
<img src="../images/amortize(1).png">

### aggregate analysis

这个方法我们需要假设一个前提：所有的操作的时间复杂度不会超过它的最坏情况，我们可以用最坏的情况进行估算其总体的时间复杂度，然后使用均摊的思想计算出其每一步的均摊时间代价。

### accounting method

这个方法我们同样是需要假设一个前提：我们假设一个所有的步骤的均摊时间复杂度，并且保证每一次操作之后我们假设的时间复杂度是始终大于实际时间复杂度的。

理解的话可以以stack模型为例进行理解。

### potential method

这个方法是从上面的一个方法衍生出来的。将假设的时间复杂度和真实的时间复杂度做差得出的即是二者之间的gap，这个东西我们可以类比于物理上的定义以真实的时间复杂度为零基准线，那么这个gap就是假设的时间复杂度的势能值，这个势能值是始终大于零的。这个势能值是自己定义的，比如stack例子中我们就可以定义stack的大小为一个势能值。

## 注释
由于本文中需要写一些代码和公式，需要到一个树的定义，现给出本文中的定义：
```
// the following is the definition of the tree nodes
typedef struct node* Tree;
struct node{
    int data;
    Tree left;
    Tree right;
    int height;
    int balance;
    Tree parent;
};
```
