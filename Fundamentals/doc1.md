## 二进制转化

```python
def sToBinString(num):
    if num > 0:
        res = posToBinString(num)
        return "".join(res)
    elif num < 0:
        res = negToBinString(num)
        return "".join(res)
    else:
        return "0"


def posToBinString(num):
    res = list()
    while num > 0:
        q, r = divmod(num, 2)
        res.insert(0, str(r))
        num = q
    return res

def negToBinString(num):
    num = abs(num)
    res = posToBinString(num)
    invertBit(res)
    res = binAdd(res, ["1"])
    return res

def invertBit(nums):
    for i in range(len(nums)):
        if nums[i] == "1":
            nums[i] = "0"
        else:
            nums[i] = "1"

def binAdd(b1, b2):
    max_len = max(len(b1), len(b2))

    while len(b1) < max_len: b1.insert(0, "0")
    while len(b2) < max_len: b2.insert(0, "0")
    carry = 0
    res = []
    for i in range(max_len-1, -1, -1):
        int1, int2 =  sToInt(b1[i]), sToInt(b2[i])
        res.insert(0, intToS(int1^int2^carry))
        if int1+int2+carry > 1:
            carry = 1
        else:
            carry = 0
    if carry:
        res.insert(0, "1")

    return res

def sToInt(s):
    return ord(s) - ord("0")

def intToS(i):
    return chr(ord("0")+i)
```
