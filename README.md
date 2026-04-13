##(PROBLEM 1) Minimum-Platforms GEEKS FOR GEEKS PROBLEM
class Solution:    
    def minPlatform(self, arr, dep):
        arr.sort()
        dep.sort()
        n=len(arr)
        c=0
        res=0
        j=0
        for i in range(n):
            while j<n and dep[j]<arr[i]:
                c-=1
                j+=1
            c+=1
            res=max(res,c)
        return res
        
## (PROBLEM 2) Aggressive Cows
class Solution:
    def aggressiveCows(self, stalls, k):
        stalls.sort()
        def caniplace(dist):
            last=stalls[0]
            c=1
            for i in range(1,len(stalls)):
                if stalls[i]-last>=dist:
                    c+=1
                    last=stalls[i]
                if c>=k:
                    return True
            return False
        l=1
        r=stalls[-1]-stalls[0]
        ans=0
        while l<=r:
            mid=(l+r)//2
            if caniplace(mid):
                ans=mid
                l=mid+1
            else:
                r=mid-1
        return ans

##(PROBLEM 3) Allocate Minimum Pages
class Solution:
    def findPages(self, arr, k):
        n=len(arr)
        if k>n:
            return -1
        def issafe(limit):
            stu=1
            pages=0
            for book in arr:
                if book+pages<=limit:
                    pages+=book
                else:
                    stu+=1
                    pages=book
                if stu>k:
                    return False
            return True
        low=max(arr)
        high=sum(arr)
        ans=high
        while low<=high:
            mid=(low+high)//2
            if issafe(mid):
                ans=mid
                high=mid-1
            else:
                low=mid+1
        return ans

##(PROBLEM 4) Rat in a Maze
class Solution:
    def ratInMaze(self, maze):
        n=len(maze)
        res=[]
        path=[]
        def bt(r,c):
            if r==n-1 and c==n-1:
                res.append("".join(path))
                return
            maze[r][c]=0
            if r+1<n and maze[r+1][c]==1:
                path.append('D')
                bt(r+1,c)
                path.pop()
            if c-1>=0 and maze[r][c-1]==1:
                path.append('L')
                bt(r,c-1)
                path.pop()
            if c+1<n and maze[r][c+1]==1:
                path.append('R')
                bt(r,c+1)
                path.pop()
            if r-1>=0 and maze[r-1][c]==1:
                path.append('U')
                bt(r-1,c)
                path.pop()
            maze[r][c]=1
        if maze[0][0]==1:
            bt(0,0)
        return res

##(PROBLEM 5) Count Subarrays with given XOR
class Solution:
    def subarrayXor(self, arr, k):
        ans = 0
        ps = 0
        freq = {0: 1}
        for num in arr:
            ps ^= num
            if ps ^ k in freq:
                ans += freq[ps ^ k]
            if ps in freq:
                freq[ps] += 1
            else:
                freq[ps] = 1
        return ans

##(PROBLEM 6) M-Coloring Problem
class Solution:
    def graphColoring(self, v, edges, m):
        graph=[[] for i in range(v)]
        for u,w in edges:
            graph[u].append(w)
            graph[w].append(u)
        color=[0]*v
        def verif(node,col):
            for nei in graph[node]:
                if color[nei]==col:
                    return False
            return True
        def assign(node):
            if node==v:
                return True
            for col in range(1,m+1):
                if verif(node,col):
                    color[node]=col
                    if assign(node+1):
                        return True
                    color[node]=0
            return False
        return assign(0)

###Undirected Graph Cycle(PROBLEM - 7)
class Solution:
	def isCycle(self, V, edges):
		#Code here
		adj=[[]for i in range(V)]
		for u,v in edges:
		    adj[u].append(v)
		    adj[v].append(u)
		visited=[False]*V
		def bfs(start):
		    q=[]
		    q.append((start,-1))
		    visited[start]=True
		    while q:
		        node,par=q.pop(0)
		        for nei in adj[node]:
		            if not visited[nei]:
		                visited[nei]=True
		                q.append((nei,node))
		            elif nei!=par:
		                return True
		    return False
		for i in range(V):
		     if not visited[i]:
		         if bfs(i):
		             return True
		return False

###BIPARTITE GRAPH (PROBLEM-8)
class Solution:
    def isBipartite(self, V, edges):
        adj=[[] for i in range(V)]
        for u,v in edges:
            adj[u].append(v)
            adj[v].append(u)
        color=[-1]*V
        for i in range(V):
            if color[i] ==-1:
               if not self.dfs(i,0,adj,color):
                    return False
        return True
    def dfs(self,node,col,adj,color):
        color[node]=col
        for neighbour in adj[node]:
            if color[neighbour]== -1:
                if not self.dfs(neighbour,1-col,adj,color):
                    return False
            elif color[neighbour] == col:
                return False
        return True

##Topological Sort(Problem-9)
(Using dfs method)
class Solution:
  def topoSort(self,V,edges):
    adj=[[]for _ in range(V)]
    for u,v in edges:
      adj[u].append(v)
    visited =[False]*V
    stack=[]
    def dfs(node):
      visited[node]=True
      for nei in adj[node]:
        if not visited[nei]:
          dfs(nei)
      stack.append(node)
    for i in range(V):
      if not visited[i]:
        dfs(i)
    return stack[::-1]

(Another method using BFS)
class Solution:
  def topoSort(self,V,edges):
    adj=[[]for _ in range(V)]
    indeg=[0]*V
    for u,v in edges:
      adj[u].append(v)
      indeg[v]+=1
    q=[]
    for i in range(V):
      if indeg[i]==0:
        q.append(i)
    res=[]
    while q:
      node=q.pop(0)
      res.append(node)
      for nei in adj[node]:
        indeg[nei]-=1
        if indeg[nei]==0:
          q.append(nei)
    return res

##Directed Graph Cycle(PROBLEM-10)
class Solution:
  def isCyclic(self,V,edges):
    adj=[[]for i in range(V)]
    indeg=[0]*V
    for u,v in edges: 
      adj[u].append(v)
      indeg[v]+=1
    q=deque([])
    for i in range(V):
      if indeg[i]==0:
        q.append(i)
    c=0
    while q:
      node=q.popleft()
      c+=1
      for nei in adj[node]:
        indeg[nei]-=1
        if indeg[nei]==0:
          q.append(nei)
    return c!=V

(Another method using DFS)
class Solution:
  def isCyclic(self,V,edges):
    adj=[[]for i in range(V)]
    for u,v in edges: 
      adj[u].append(v)
    visited=[False]*V
    path=[False]*V
    def dfs(node):
      visited[node]=True
      path[node]=True
      for nei in adj[node]:
        if not visited[nei]:
          if dfs(nei):
            return True
        elif path[nei]:
            return True
      path[node]=False
      return False
    for i in range(V):
      if not visited[i]:
        if dfs(i):
          return True
    return False

