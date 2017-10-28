```#include<iostream>
#include<queue>
using namespace std;
typedef struct node//定义一个node结构
{
  char data;
  struct node *leftchild;//node的左右孩子分别是这种结构的指针
  struct node *rightchild;

}bintreenode,*bintree;//声明这种结构的对象和指针，指针用于下面申请新的对象内存
//利用前序遍历的方法创建树
void createbintree(bintree &T)//参数是struct的指针
{
  char c;
  cin>>c;
  if(c=='#')
    T=NULL;//如果输入为#,则说明这个地方不是结点了，指针域赋值为空
  else
  {
    T=new bintreenode;//如果输入的数据符合要求，则用指针申请内存
    T->data=c;
    createbintree(T->leftchild);//递归创建左子树
    createbintree(T->rightchild);//递归创建右子树，根据堆栈的原理只有左子树都创建好了才会创建右
子树
  }
}
//层次遍历函数
void leveltraverse(bintree root)//参数为树的根结点的指针，递归调用时则为对应子树的根结点指针
{
  if(root==NULL)
    return;
  queue<bintree> que;//que是队列对象，里面的成员类型为结构指针
  que.push(root);//先将根结点入队，成为队列的第一个元素
  while(!que.empty())//队列非空时，将会进行循环，按层次讲队列元素输出
  {
    root=que.front();//用root记录队列的第一个元素
    que.pop();//将队列的第一个元素弹出
    cout<<root->data<<" ";//将每次新队列的第一个元素打印出来，实现按层依次输出
    if(root->leftchild!=NULL)
      que.push(root->leftchild);//左孩子入队
    if(root->rightchild!=NULL)
      que.push(root->rightchild);//右孩子入队
  }
  }
int main()
{
  bintree q;
  cout<<"请按前序遍历的方式输入一棵树："<<endl;
  cout<<"比如：输入一棵只有两层的树，第一层为a,第二层为b,c;则应这样输入：ab##c##然后按enter结束
即可"<<endl;
  createbintree(q);
  cout<<"按层遍历的结果如下："<<endl;
  leveltraverse(q);
  cout<<endl;
}```


                                                                             1,1          顶端
