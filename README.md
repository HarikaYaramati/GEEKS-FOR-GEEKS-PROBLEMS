# Minimum-Platforms GEEKS FOR GEEKS PROBLEM
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
        
        
