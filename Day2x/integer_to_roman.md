# Description
Integer to Roman

https://leetcode.com/problems/integer-to-roman/description/

# Note 
- Time taken: 10 mins 

# Solution 
```python 
class Solution:
    def intToRoman(self, num: int) -> str:
        m = {1: "I", 4: "IV", 5: "V", 9: "IX", 10: "X", 40: "XL", 50: "L", 90: "XC", 100: "C", 400: "CD", 500: "D", 900: "CM", 1000: "M"}
        keys = sorted(m, reverse=True)
        # print (m, keys)

        res = ""
        pt = 0
        while num>0: 
            if num< keys[pt]:
                pt +=1
            else: 
                times = num//keys[pt]
                for i in range (times):
                    res += m[keys[pt]]
                num -= keys[pt]*times
        return res

```

Cleaner 
```python 
def intToRoman(self, num: int) -> str:
        m = [(1000, "M"), (900, "CM"), (500, "D"), (400, "CD"), (100, "C"), (90, "XC") ,(50, "L"), (40, "XL"), (10, "X"),  (9, "IX"),  (5, "V"),(4 , "IV"),  (1, "I")]
       
        res = ""
        pt = 0
        while num>0: 
            if num< m[pt][0]:
                pt +=1
            else: 
                count, num = divmod(num, m[pt][0])
                res += m[pt][1] * count     
        return res
```
