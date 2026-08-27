1. Two Sum
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        output = {}
        n = len(nums)

        for i in range(n):
            output[nums[i]] = i
        
        for i in range(n):
            comp = target - nums[i]
            if comp in output and output[comp] != i:
                return [output[comp],i]
        
```
2. Contains Duplicate ⭐
```
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        noDupSet = set(nums)
        if len(noDupSet) == len(nums):
            return False
        else:
            return True
```
3. Best Time to Buy and Sell Stock ⭐
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        max = 0
        n = len(prices)
        buy = prices[0]

        for i in range(n):
            if prices[i]<buy:
                buy = prices[i]
            elif prices[i] - buy > max:
                max = prices[i] - buy
        
        return max
```
4. Maximum Subarray ⭐
```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        current_max, final_max = 0, -inf
        for num in nums:
            current_max = max(num, current_max+num)
            final_max = max(current_max,final_max)
        return final_max
        
```
5. Top K Frequent Elements
```
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # initializing a dict where each new key will get a new int initalization
        freqs = defaultdict(int)
        for num in nums:
            freqs[num]+=1
        # reverse sorting the dict based on the counter and then retaining only the top k values
        freqs = dict(sorted(freqs.items(), key = lambda item: item[1],reverse = True)[:k])
        return list(freqs.keys())
```
6.  Group Anagrams
```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        grouped = defaultdict(list)

        for word in strs:
            key = "".join(sorted(word))
            grouped[key].append(word)
        
        return list(grouped.values())
```
7.  Valid Anagram
```
from collections import Counter
class Solution:
    def isAnagram(self, s: str, t: str) -> bool: 
        return Counter(s) == Counter(t)

```
or 
```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool: 
        if len(s) != len(t):
            return False
        l2 = {}
        for char in t:
            if char in l2:
                l2[char] += 1
            else:
                l2[char] = 1
        
        for char in s:
            if char in l2:
                if l2[char] == 0:
                    return False
                else:
                    l2[char] -=1
            else:
                return False

        return True
```
8. Valid Palindrome ⭐
```
class Solution:
    def isPalindrome(self, s: str) -> bool:    
        s = s.lower().split()
        s = "".join(char for word in s for char in word if char.isalnum())
        return s == s[::-1]
        
```
9. Two Sum II
```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left = 0
        right = len(numbers) - 1

        while left < right:
            if numbers[left] + numbers[right] == target:
                return [left+1,right+1]
            elif numbers[left] + numbers[right] < target:
                left+=1
            else:
                right-=1
        
```
10. 3Sum
Brute force:
```
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        output = []
        oneL = {}
        n = len(nums)
        for i in range(n):
            oneL[nums[i]] = i
        for i in range(n):
            for j in range(n):
                k = (nums[i]+nums[j]) * -1
                if i !=j and k in nums and oneL[k] != i and oneL[k] != j:
                    val = sorted([nums[i],nums[j],k])
                    if not val in output:
                        output.append(val)
        return output
```
11. Move 0s
Snowball approach:
```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        snowBall = 0
        for i in range (len(nums)):
            if nums[i] == 0:
                snowBall+=1
            elif snowBall > 0:
                temp = nums[i]
                nums[i]=0
                nums[i-snowBall] = temp
```
Optimal approach:
```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        anchor = 0
        for i in range(1,len(nums)):
            if nums[i] != 0 and nums[anchor] == 0:
                nums[i], nums[anchor] = nums[anchor], nums[i]
            
            if nums[anchor] != 0: 
                anchor+=1
```
12. Remove Duplicates from Sorted Array
Approach
Have an anchor, lets keep as 0th index.
Traverse until you find a different value than that of the anchor
Once you find that number, increment the anchor, store the different value in the anchor's index in the array
Return the anchor+1 index(since array values start from 0, your distinct value will always be less by 1)
```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        n = len(nums)
        i=0
        for j in range(1,n):
            if nums[i] != nums[j]:
                i+=1
                nums[i]= nums[j]
            print(nums)
        return i+1                     
```
13. Product of Array Except Self ⭐
```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        output =  [1] * n
        prefix = [1] * n
        suffix = [1] * n
        for i in range(1,n):
            prefix[i] = nums[i-1] * prefix[i-1]
        for i in range(n-2,-1,-1):
            suffix[i] = nums[i+1] * suffix[i+1]
        for i in range(n):
            output[i] = prefix[i]*suffix[i]
        return output
```
14. Longest Consecutive Sequence
```
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        n = len(nums)
        if n < 2:
            return n
        nums.sort()
        maxCon = 1
        currentCon = 1
        currentNum = nums[0]
        for i in range(1,n):
            if nums[i] == currentNum:
                continue
            if nums[i] == (currentNum+1):
                currentCon += 1
                if currentCon > maxCon:
                    maxCon = currentCon
            else:
                if currentCon > maxCon:
                    maxCon = currentCon
                currentCon = 1
            currentNum = nums[i]
        return maxCon
```
15. Majority Element
```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        n = len(nums)
        threshold = n/2
        majority = 1
        output = defaultdict(int)
        for num in nums:
            output[num]+=1
        for (key,val) in output.items():
            if val > threshold:
                majority = key
        return majority
```
16. Merge Sorted Array
```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i = m -1
        j = n -1
        k = m + n -1

        while j >= 0:
            if i>=0 and nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                i-=1
            else:
                nums1[k] = nums2[j]
                j-=1
            k-=1
```
17. 
