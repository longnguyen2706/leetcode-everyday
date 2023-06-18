# Description
[Encode decode string](https://leetcode.com/problems/encode-and-decode-strings/editorial/)

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

# Note

# Solution 
My solution - will work with any non ascii characters
```python
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        # encoded string = [size_arr] + concat all str 
        size =[]
        r = ""
        for s in strs: 
            size.append(len(s))
            r+=s
        r = str(size) + r
        # print (r)
        return r 
        

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        last_size_idx = s.find("]")
        size_str = s[:last_size_idx+1]
        sizes = size_str[1:last_size_idx].split(",")
        
        l = []
        idx = last_size_idx + 1
        for size in sizes: 
            l.append(s[idx:idx+int(size)])
            idx +=int(size)

        return l 
```