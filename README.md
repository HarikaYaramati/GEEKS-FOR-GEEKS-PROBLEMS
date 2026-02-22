##PROBLEM 1 Minimum-Platforms GEEKS FOR GEEKS PROBLEM
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
        
## PROBLEM 2 Aggressive Cows
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

##PROBLEM 3 Allocate Minimum Pages
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

##PROBLEM 4 Rat in a Maze
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

##PROBLEM 5 Count Subarrays with given XOR
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

##PROBLEM 6 M-Coloring Problem
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


