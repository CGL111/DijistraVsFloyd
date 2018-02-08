# DijistraVsFloyd
Dijistra: 用于计算单源 x最短路径
已知数据weight[] e[][]//e的值 1 or 0 weight 每个V的权重
需要的结果：最短路径的个数、最短路径中权重和最大的
1D array Dis[] 记录单源到各个顶点的最短距离 初始是Dis[x]==0 其余INF or 从e中获取值
1D num[] 记录路径个数 if e[][]!=INF num[] = 1 else num[] = 0;
1D w[] 记录权重之和 初始值w[x] = weight[x] 其余为0
1D book[] 记录节点的访问情况 初始是-1
循环n-1次 {???
前期：
每次从上次的Dis找出u 使得min(Dis[u]);
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

