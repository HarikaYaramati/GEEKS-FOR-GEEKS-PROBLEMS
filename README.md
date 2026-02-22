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



        
        
