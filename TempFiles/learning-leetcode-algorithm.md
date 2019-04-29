#### 斐波那契数列
    # 非递归
    class Solution(object):
        def fib(self, N):
            """
            :type N: int
            :rtype: int
            """
            n_1 = 1
            n_2 = 0
            tmp = 0
            if N >= 2:
                for idx in range(N):
                    n_1, n_2 = n_1 + n_2, n_1
            else:
                return N
            return n_2
    # 递归
    class Solution(object):
        def fib(self, N):
            """
            :type N: int
            :rtype: int
            """
            if N == 0:
                return 0
            elif N == 1:
                return 1
            else:
                return self.fib(N - 1) + self.fib(N - 2)

#### 求平方根（牛顿法）

    class Solution(object):
        def mySqrt(self, x):
            """
            :type x: int
            :rtype: int
            """
            if x <= 1:
                return x
            r = x
            while r > x / r:
                r = (r + x / r) // 2
            return int(r)

#### 爬楼梯

    假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

    每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

    class Solution(object):
        def climbStairs(self, n):
            """
            :type n: int
            :rtype: int
            """
            dp = []
            dp.extend([0, 1, 2])
            if n >= 3: 
                for idx in range(3, n + 1): # 注意这里的 n + 1
                    dp.append(dp[idx - 1] + dp[idx - 2])
            return dp[n]


#### 字符串list公共前缀

    编写一个函数来查找字符串数组中的最长公共前缀。
    如果不存在公共前缀，返回空字符串 ""。

    # 优解
    # 思路：利用python的max()和min()，在Python里字符串是可以比较的，按照ascII值排，举例abb， aba，abac，最大为abb，最小为aba。所以只需要比较最大最小的公共前缀就是整个数组的公共前缀

    def longestCommonPrefix(strs):
        if not strs: return ""
        s1 = min(strs)
        s2 = max(strs)
        for i,x in enumerate(s1):
            if x != s2[i]:
                return s2[:i]
        return s1
    
    # 不优解
    class Solution(object):
        def longestCommonPrefix(self, strs):
            """
            :type strs: List[str]
            :rtype: str
            """
            all_son = []
            for s in strs:
                all_son.extend(self.son(s))

            dic = {}
            for s in all_son:
                if s not in dic:
                    dic.setdefault(s, 0)
                dic[s] += 1
            try:
                return max([s for s,count in dic.items() if count == len(strs)])
            except ValueError:
                return ''

        def son(self, str_):
            tmp = []
            tmp_str = ''
            for c in str_:
                tmp_str += c
                tmp.append(tmp_str)
            return tmp


#### 删除数组重复数字

    给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

    不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

    # 解
    # 双指针（快慢指针）
    class Solution(object):
        def removeDuplicates(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            i = 0
            for j in range(len(nums)):
                if nums[j] != nums[i]:
                    i += 1
                    nums[i] = nums[j]
            return i + 1
            
    