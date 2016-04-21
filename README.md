# data-structures-and-algorithms

#include<stdio.h>
#include<stdlib.h>
#define M 50
#define MAXNUM 10000
typedef struct enode     //边节点
{
	int adjacent;        //存储顶点序号
	int cost;            //权
	struct enode *next;  // 指向下一个
}enode;
typedef struct hnode    // 头结点
{
	int Llink;
	int Rlink;
	int father;
	int dist;	
	enode *firstarc;    
}hnode;

int n,m;

hnode L[M];
void init()
{
	int s,v;
	enode *p;	//开边节点
	
	for(v<0;v<=n;v++)
	{
		L[v].dist=MAXNUM;//无穷大的数
		L[v].father=s;
		L[v].Llink=v-1;
		L[v].Rlink=v+1;
		L[v].firstarc=NULL;
	}
	L[0].Llink=n;
	L[n].Rlink=0;
	for(int j=0;j<m;j++)
	{
		int a,b;
		
		printf("输入边两个结点： ");
		scanf("%d%d",&a,&b);
		p=(enode*)malloc(sizeof(enode));
		p->adjacent=b;          //边节点编号
		p->next=L[a].firstarc;  //链接 插入到前一个前面
		L[a].firstarc=p;        
	}
	
	printf("输入源点：");
	scanf("%d",&s);

	L[L[s].Llink].Rlink=L[s].Rlink;
	L[L[s].Rlink].Llink=L[s].Llink;
	p=L[s].firstarc;
	while(p);
	{
		v=p->adjacent;
		L[v].dist=p->cost;
		p=p->next;
	}
}
int main()
{
	printf("输入顶点数和边数");
	while(scanf("%d%d",&n,&m)!=EOF&&(n||m))
	{
		init();
	}
	return 0;
}
