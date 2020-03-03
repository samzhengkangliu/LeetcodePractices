
# Data Structures & Algorithms

## BFS
Sample code:
```
def BFS(graph, s):
	queue = []
	queue.append(s)
	seen = {} 
	seen.add(s)
	while (len(queue) > 0):
		vertex = queue.pop(0)
		nodes = graph[vertex]
		for w in nodes:
			if w not in seen:
				queue.append(w)
				seen.add(w)
			
```
创建每个点的映射：
```
def shortestDistance(graph,s):
	queue=[]
	queue.append(s)
	visited={}
	visited.add(s)
	parent={s : None}
	
	while (len(queue) > 0):
		vertex = queue.pop(0)
		nodes = graph[vertex]
		for w in nodes:
			if w not in visited:
				queue.append(w)
				visited.add(w)
				parent[w] = vertex
		return parent
# 返回从某个点到另外一个点的最短路径
# v = somepoint
# while v!= None:
#   v = parent[v]
```

## DFS
Sample code:
```
def DFS(graph, s):
	stack= []
	stack.append(s)
	seen = set() 
	seen.add(s)
	while (len(stack) > 0):
		vertex = stack.pop()
		nodes = graph[vertex]
		for w in nodes:
			if w not in seen:
				stack.append(w)
				seen.add(w)
```

