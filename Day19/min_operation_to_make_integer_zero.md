
# Description
[Minimum Operations to Make the Integer Zero](https://leetcode.com/problems/minimum-operations-to-make-the-integer-zero/)

You are given two integers num1 and num2.

In one operation, you can choose integer i in the range [0, 60] and subtract 2i + num2 from num1.

Return the integer denoting the minimum number of operations needed to make num1 equal to 0.

If it is impossible to make num1 equal to 0, return -1.

# Note



# Solution
## Solution 1
```python
class Solution:
    def makeTheIntegerZero(self, num1: int, num2: int) -> int:
        # num1 - (num2)*n - sum(2^i)
        # num1/2 -  num2/2*n-sum(2^i)
        
        # 1+ (1, -1) -> if num2<0 and equal: 1+ (1, -4) if num2>0
        # if num2%2 ==1: num1- (2k+1)*n -sum(2^i) -> (num1-n) - 2k*n - sum(2^i)
        
        # min(num1, num2) = 1+ min(num1/2, num2/2) if num1 is odd, num2 is 
        
        # num2 <0: num1+ num2*n - sum(2^i) -> num1 + num2 + num2*(n-1) - sum\
        
        # num2>=0: num1-num2*n -sum(2^i)
                            
        # 3, -3 -> 6, 9
         # 2^0 + 2^1 = 3; 2^0 + 2^1+ 2^2 = 7 -> 10, 17 -> 
          # -> 2^0 +  2^1 + 2^1 + 2^2 + 2^3
        
        # def max_p2(num):
        #     if num ==1: 
        #         return 0 
        #     return 1+ max_p2(num//2)
        
        # def min_p2(num):
        #     count=0
        #     while num>0:
        #         p = max_p2(num)
        #         num -=pow(2, p)
        #         count+=1
        #     return count

        def count_bit(num):
            count =0
            while num>0: 
                m = num >>1
                bit = num ^ (m<<1)
                if bit == 1: 
                    count +=1
                num = m
            return count
       
        
        # print (max_p2(4), max_p2(5), max_p2(7))
        # print (min_p2(4), min_p2(5), min_p2(7), min_p2(8))
        
        n = 0
        while True: 
            s = num1 - n * num2
            if s<=0: 
                return -1
            val = count_bit(s)
            if val>n: 
                n+=1
            elif val ==n:
                return n
            else: # min_p2(s)<n: 
                if s == 1: # special case -> 2^0 cannot decompose further
                    return -1
                else: 
                    return n 
```