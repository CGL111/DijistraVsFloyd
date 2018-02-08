# DijistraVsFloyd
Dijistra: 用于计算单源 x最短路径
算法描述：将V分为两组 S U
          S为已经求出最短路径的顶点集合 
          U为确定最短路径的顶点集合
          按最短路径递增加入S中 此过程始终保持x到S中各顶点的最短路径长度都不大于x 到U中各顶点的最短路径的长度 
          S对应顶点是x到其最短路径的长度 U是x为源点只包括S中顶点为中间点的最短路径长度 ？？？
算法步骤：将V分为两组 S U 
a. S = {x} and U include other points
b. 寻找U中距离X最短的顶点u
c .以u 为中间点x到S中的任意一点的路径都不大于x到u再到S中任意一点的距离
d. 重复bc直到S包含所有的顶点
已知数据weight[] e[][]//e的值 1 or 0 weight 每个V的权重
需要的结果：最短路径的个数、最短路径中权重和最大的
1D array Dis[] 记录单源到各个顶点的最短距离 初始是Dis[x]==0 其余INF or 从e中获取值
1D num[] 记录路径个数 if e[][]!=INF num[] = 1 else num[] = 0;
1D w[] 记录权重之和 初始值w[x] = weight[x] 其余为0
1D book[] 记录节点的访问情况 初始是-1
循环n-1次 { 
前期：
每次从上次的Dis 未被访问过顶点中找出的u使得min(Dis[u]);
book[u]=1
更新：
枚举终点 j
if(!book[j]&&Dis[u]+e[u][j] < INF)
if Dis[u]+e[u][j] < Dis[j]:
 {
 Dis[j] = Dis[u]+e[u][j];
 num[j] = num[u];
 w[j] = w[u]+weight[j]
 }
if Dis[u]+e[u][j] == Dis[j]
 {
 num[j]+=num[u]
  if(w[u]+weight[j] > w[j])
  w[j] = w[u]+weight[j]
 } 
}
Floyd算法：
解决任意两点间最短路径 处理有向图或负权值得最短路径问题 也可计算有向图的传递闭包
算法思想：i,j两点之间的最短路径无非两种可能
1.从i直接到j
2.i 经过有限个中间节点到j
所以假设Dis(i,j)为i 到 j 最短路径 对于每一个节点K 有应有Dis(i,k)+Dis(k,j) >= Dis(i,j)
如果Dis(i,k)+Dis(k,j) < Dis(i,j)
则 Dis(i,j) = Dis(i,k)+Dis(k,j);//dis(i,k)，Dis(k,j)也可能经过的很多节点
//D[v][w] < D[v][k] + D[k][v]但更新之后大小关系变化的怎么办
 //存在K1使得  大小关系变化 即K1会更新 D[v][w]
所有节点都访问完Dis(i,j)便是最短路径
算法步骤：
2D 邻接矩阵 e 
2D path 以v2到v8为例，P[2][8] = 4，说明要经过顶点v4, 将4替换2，P[4][8] = 3, 说明经过v3, .......， 最终推导出最短路径为：v2->v4->v3->v6->v7->v8。
2D Dis  记录最短路径的长度
更新
枚举所有可能性
	for (int k = 0; k < n; k++) {
		for (int i = 0; i < n; i++) {
			for (int j = 0; j < n; j++) {
   if (A[i][k] + A[k][j] < A[i][j])
				{
					A[i][j] = A[i][k] + A[k][j];
					path[i][j] = k;
				}
      }
     }
   }
   每次第K行第K列以及对角线的数值都不会变vk->kw vw
