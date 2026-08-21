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
