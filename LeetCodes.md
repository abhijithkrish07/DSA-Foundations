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
8.  
