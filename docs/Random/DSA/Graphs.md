## BFS
Time Complexity - O(N.M)
- Multi-path Problems
	- multiple monsters chasing paths.
	- Solve it in O(NM).
	- Create A E<sub>super</sub> and do bfs for all start nodes
- In Code, whnever pushing to queue, mark the node visited.

## Topological Ordering
- Property of DAG's
- prefer BFS ([[Kahn's Algo]])

If want a lexicographically smallest topo array
	- use a priority_queue instead of a queue.
	- insert negetive of the value of node.
	- when popping take the negetive again.

### Shortest path

![[Pasted image 20230508132217.png]]


![[Pasted image 20230509104619.png]]
1. Finding distance between nodes with some a cost to move between same value and b value between adjancent values.


![[Pasted image 20230509110304.png]]
2. Given a String , in how many bit flips can be reach end string such that we do not encounter any of the banned string in the path.



## Overview
- unweighted
	- BFS(1) - Single Source shortest path.
```c++
q.push(st);
dis[inf];
while(!q.empty())
{
	x= q.front();
	q.pop();
	for(auto x: g[x]){
		if(dist[v]>dis[x]+1)
			dis[v]=dis[x]+1;
			q.push(v);
	}
}
```


## o-1 BFS 
	- Use a dequee
	- while pushing, if cost is 0 push front, else push back.
 
### Problems
1. ![[Pasted image 20230510134024.png]]
Min No, of Bridges to build so that all components are connected.
![[Pasted image 20230510134843.png]]

- [[Dijkstra's Algo]]
	- -ve cycle exists - Galat ans.
	- -ve edge - TLE
	- use a priority queue instead of queue.
```cpp
	if (vis[x]==1) continue;
	vis[x]=1;	 
```
after popping from queue, this is necessary to remove redundant node and edges.


- [[Bellman Ford]]
	- SSSP in negetive cycles.


### All Pair Shortest Path

- [[Floyd Warshall's Algorithm]]
	- Need Adjacency Matrix
```python
for k in (1,n)
	for i in (1,n)
		for j in (1,n)
			dist[i][j]= min(dist[i][j],dist[i][k]+dist[k][j])
```



