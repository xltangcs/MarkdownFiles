# 10.07


## 1
每日一题 [最大升序子数组和](https://leetcode.cn/problems/maximum-ascending-subarray-sum/)

标签：简单题、模拟、暴力、动态规划、DP

分析：

枚举数组中每个元素，判断是否大于前一个，若``nums[i] > nums[i-1]``，则总和``sum += nums[i]``否则，``sum = nums[i]``.

## 2

[两数之和](https://leetcode.cn/problems/two-sum/)

标签：枚举、暴力、哈希、stl unordered_map

分析：

解法一：两层循环遍历看``nums[i] + nums[j]``是否等于target。

解法二：使用unordered_map，一层遍历，每次查找target-nums[i] 是否在map中，不在则记录``map[nums[i]] = i``，否则就已经找到答案。

# 10.08

## 3
每日一题 [优势洗牌](https://leetcode.cn/problems/advantage-shuffle/)

标签：二分、贪心

分析：

将nums1排序，遍历nums2，在nums1中二分查找刚好大于nums2[i]的值，若存在，则加入数组ans中，反之则将nums1中尚未加入ans中的最小值加入ans。

二分查找算法
 ```c++
    left = 0;
    right = nums1.size( )-1;
    while(left < right)
    {
        int mid = left + ( right - left) >> 1;  //防止溢出
        if(nums1[mid] < nums2[i])
        left = mid+1;
        else right = mid;
    }
 ```

# 10.09

## 4
每日一题 [856. 括号的分数](https://leetcode.cn/problems/score-of-parentheses/)

标签：栈、stack、模拟

分析：
遍历s[i]，若为'('，则加入stack；若为')'，访问stack，若为'('，则配对，弹出并写入1，否则一直弹出并相加，最后*2即可。

## 5 第314场周赛 AC T1 T2 
T3 [6202. 使用机器人打印字典序最小的字符串](https://leetcode.cn/problems/using-a-robot-to-print-the-lexicographically-smallest-string/)

标签：模拟、栈、stack
分析：
先预处理，记录每个字符后面最小的字符。
接着遍历s[i],入栈，和他后面最小的字符进行比较，弹出栈中所有小于后面最小字符的元素。


T4 [6203. 矩阵中和能被 K 整除的路径](https://leetcode.cn/contest/weekly-contest-314/problems/paths-in-matrix-whose-sum-is-divisible-by-k/)

标签：dp、动态规划
dp[i][j][v]表示以 (i, j) 为终点，且路径和 mod k 等于 v 的路径数。答案就是dp[m-1][n-1][0];
转移方程：
```c++
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                for(int v=0;v<k;v++)
                {
                    if(i>0)
                    dp[i][j][v] = (dp[i][j][v] + dp[i-1][j][ (v+k-grid[i][j]%k) % k])%mod;
                    if(j>0)
                    dp[i][j][v] = (dp[i][j][v] + dp[i][j-1][ (v+k-grid[i][j]%k) % k])%mod;
                }
            }
        }
```
# 10.10

## 6
每日一题 [801. 使序列递增的最小交换次数](https://leetcode.cn/problems/minimum-swaps-to-make-sequences-increasing/)

标签：动态规划、dp
分析：
nums1[i] > nums1[i - 1] && nums2[i] > nums2[i - 1]
nums1[i] > nums2[i - 1] && nums2[i] > nums1[i - 1]

```c++
class Solution {
public:
    int minSwap(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size( );
        int dp[n+1][2];
        dp[0][0] = 0;
        dp[0][1] = 1;
        for(int i=1; i<n;i++)
        {
            if((nums1[i] > nums1[i-1] && nums2[i] > nums2[i-1]) && (nums1[i] > nums2[i-1] && nums2[i] > nums1[i-1]))
            {
                dp[i][0] = min(dp[i-1][0],dp[i-1][1]);
                dp[i][1] = min(dp[i-1][1],dp[i-1][0])+1;
            }
            else if(nums1[i] > nums1[i-1] && nums2[i] > nums2[i-1])
            {
                dp[i][0] = dp[i-1][0];
                dp[i][1] = dp[i-1][1] + 1;
            }
            else if(nums1[i] > nums2[i-1] && nums2[i] > nums1[i-1])
            {
                dp[i][0] = dp[i-1][1];
                dp[i][1] = dp[i-1][0]+1;
            }
        }
        return min(dp[n-1][0], dp[n-1][1]);
    }
};
```
# 10.11
## 7
每日一题 [1790. 仅执行一次字符串交换能否使两个字符串相等](https://leetcode.cn/problems/check-if-one-string-swap-can-make-strings-equal/)
标签：字符串、模拟
分析：
```c++
class Solution {
public:
    bool areAlmostEqual(string s1, string s2) {
        int l1 = s1.length( );
        int l2 = s2.length( );
        char a,b,c,d;
        if(l1 != l2)
        {
            return false;
        }
        int cnt = 0;
        for(int i=0;i<l1;i++)
        {
            if(s1[i] != s2[i])
            {
                cnt ++;
                if(cnt == 1)
                {
                    a = s1[i];
                    b = s2[i];
                }
                if(cnt == 2)
                {
                    c = s1[i];
                    d = s2[i];
                }

            }
            
        }
        if(cnt == 0 || (cnt == 2 && a == d && b == c))
        return true;
        else
        return false;

    }
};
```
## 8
[2.两数相加](https://leetcode.cn/problems/add-two-numbers/comments/)
标签：链表、模拟
分析：
```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode *ans = new ListNode( );
        ListNode *l = ans;
        bool carry = false;
        int sum = 0;
        while(l1 != NULL || l2 != NULL || carry)
        {
            int a1 = (l1 == NULL) ? 0 : l1->val;
            int a2 = (l2 == NULL) ? 0 : l2->val;
            sum = a1 + a2 + (carry == true);
            if(sum > 9) carry = true;
            else carry = false;
            ListNode *temp = new ListNode(sum%10);
            l->next = temp;
            l = temp;
            if(l1 != NULL) l1 = l1->next;
            if(l2 != NULL) l2 = l2->next;
        }
        return ans->next;
    }
};
```

# 10.12
## 9
[817.链表组件](https://leetcode.cn/problems/linked-list-components/)
标签：链表、set、模拟
分析：
```c++
class Solution {
public:
    int numComponents(ListNode* head, vector<int>& nums) {
        set<int> s;
        for(int i =0;i<nums.size( );i++) s.insert(nums[i]);
        bool flag = false;
        int cnt = 0;
        int t;
        while(head != NULL)
        {
            t = head -> val;
            if(s.find(head->val) != s.end( )) flag = true;
            else
            {
                if(flag)
                {
                    flag = false;
                    cnt ++;
                }
            }
            head = head->next;
        }
        if(s.find(t) != s.end( )) cnt ++;
        return cnt;
    }
};
```
# 10.13
## 10
[769. 最多能完成排序的块](https://leetcode.cn/problems/max-chunks-to-make-sorted/)
标签：多思考...
分析：
当遍历到第i个位置时，如果可以切分为块，那前i个位置的最大值一定等于i。
```c++
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        int mark = 0;
        int n = arr.size( );
        int cnt =0;
        for(int i=0;i<n;i++)
        {
            mark = max(mark, arr[i]);
            if(mark == i)
            {
                cnt++;
                mark = -1;
            }
        }
        return cnt;
    }
};
```
# 10.14
## 11
[940. 不同的子序列 II](https://leetcode.cn/problems/distinct-subsequences-ii/)
标签：动态规划、计数、找规律
分析：
解法一：动态规划
dp[i][j]表示到字符s[i]时以j(s[i]-'a')结尾的子序列总数。
* 当s[i] != j 时，dp[i][j] = dp[i-1][j];
* 当s[i] == j 时，dp[i][j] = s[i] 单独作为子序列 +s[i] 拼接在其余子序列后面形成新子序列

```c++
class Solution {
public:
    int distinctSubseqII(string s) {
        int n = s.length( );
        int ans = 0;
        const int mod = 1e9+7;
        int dp[n+1][27];
        memset(dp,0,sizeof(dp));
        dp[0][s[0]-'a'] = 1;
        for(int i=1;i<n;i++)
        {
            for(int j =0;j<26;j++)
            {
                if(s[i] - 'a' != j)
                {
                    dp[i][j] = dp[i-1][j];
                }
                else
                {
                    int temp = 1;
                    for(int k =0;k<26;k++)
                    temp = (temp + dp[i-1][k]) % mod;
                    dp[i][j] = temp;
                }
            }
        }
        for(int i=0;i<26;i++)
            ans = (ans + dp[n-1][i]) %  mod;
        return ans;
    }
};
```
解法二：找规律
```c++
class Solution {
public:
    int distinctSubseqII(string s) {
        const int mod = 1e9+7;
        long ans = 0;   //加法可能超出int范围
        int cnt[27];
        memset(cnt,0,sizeof(cnt));
        for(int i = 0;i<s.length( );i++)
        {
            int pre = cnt[s[i]-'a'];
            cnt[s[i]-'a'] = (ans + 1) % mod;
            ans = (ans + cnt[s[i]-'a']  - pre + mod) % mod;
        }
        return int(ans%mod);
    }
};
```
# 10.15 
## 12
[1441. 用栈操作构建数组](https://leetcode.cn/problems/build-an-array-with-stack-operations/)
标签：简单模拟
分析：
```c++
class Solution {
public:
    vector<string> buildArray(vector<int>& target, int n) {
        vector<string> vec;
        int index = 1;
        for(int i=0;i<target.size( );i++)
        {
            if(target[i] == index)
            {
                vec.push_back("Push");
                index ++;
            }
            else
            {
                while(index != target[i])
                {
                    vec.push_back("Push");
                    vec.push_back("Pop");
                    index ++;
                }
                vec.push_back("Push");
                index ++;
            }
        }
        return vec;
    }
};
```

# 10.16
## 13
[886.可能的二分法](https://leetcode.cn/problems/possible-bipartition/)
标签：并查集、dfs、染色法
分析：
```c++
class Solution {
public:
    static const int N = 2005;
    int fa[2*N];
    int findfa(int x)
    {
        if(x != fa[x]) return fa[x] = findfa(fa[x]);
        else 
        return x;
    }

    bool possibleBipartition(int n, vector<vector<int>>& dis) {
        for(int i=0;i<2*N;i++) fa[i] = i;
        for(auto d : dis)
        {
            int a = d[0], b = d[1];
            if(findfa(a) == findfa(b)) return false;
            else
            {
                fa[findfa(a)] = findfa(b+n);
                fa[findfa(b)] = findfa(a+n);
            }
        }
        return true;
    }
};
```

# 10.17
## 14
[904.水果成篮](https://leetcode.cn/problems/fruit-into-baskets/)
标签：滑动窗口、双指针
分析：
```c++
class Solution {
public:
    int totalFruit(vector<int>& f) {
        unordered_map<int, int> cnt;
        int ans = -1;
        for(int i=0,j=0;j<f.size( );j++)
        {
            int x = f[j];
            cnt[x] ++;
            while(cnt.size( ) > 2)
            {
                cnt[f[i]] --;
                if(cnt[f[i]] == 0) cnt.erase(f[i]);
                i++;
            }
            ans = max(ans, j-i+1);
        }
        return ans;
    }
};
```


# 10.18
## 15
[902. 最大为 N 的数字组合](https://leetcode.cn/problems/numbers-at-most-n-given-digit-set/)
标签：数位dp、数学、找规律
分析：
解法一：纯数学规律
```c++
class Solution {
public:
    int atMostNGivenDigitSet(vector<string>& digits, int n) {
        string num = to_string(n);
        int m = digits.size( ), l = num.length( );
        int ans = 0;
        //所有位数低于n的数都满足要求
        for(int i=1;i<l;i++) ans += pow(m,i);
        for(int i=0, j=0; i<l; i++)
        {
            //找到大于等于num[i]的digits[j]
            for(j=0;j<m && stoi(digits[j]) < (num[i]-'0'); j++);
            //小于num[i]的直接加上去
            ans += j * pow(m, l-i-1);
            //刚好等于n的
            if(i == l-1 && j < m && stoi(digits[j]) == (num[i]-'0'))
                ans ++;
            //没有小于等于num[i]的digits[j]了
            if(j >= m || stoi(digits[j]) != (num[i]-'0'))
                break;
        }
        return ans;
    }
};
```
解法二：数位dp
```c++

```

# 10.19
## 16
[1700. 无法吃午餐的学生数量](https://leetcode.cn/problems/number-of-students-unable-to-eat-lunch/)
标签：模拟、简单题
分析：
```c++
class Solution {
public:
    int countStudents(vector<int>& students, vector<int>& sandwiches) {
        int one = 0;
        for(int i=0; i<students.size( ); i++)
            if(students[i])
                one ++;
        int zero = students.size( ) - one;
        for(int i=0; i<sandwiches.size( ); i++)
        {
            if(sandwiches[i]) one --;
            else zero --;
            if(zero < 0 || one < 0) break;
        }
        return max(one, 0) + max(zero, 0);
    }
};
```

# 10.20
## 17
[779. 第K个语法符号](https://leetcode.cn/problems/k-th-symbol-in-grammar/)
标签：找规律、递归
分析：
```c++
class Solution {
public:
    int kthGrammar(int n, int k) {
        if(n == 1) return 0;
        int mid = pow(2,n-2);
        if(k <= mid) return kthGrammar(n-1,k);
        else return 1-kthGrammar(n-1, k-mid);
    }
};
```

# 10.21
## 18
[901. 股票价格跨度](https://leetcode.cn/problems/online-stock-span/)
标签：单调栈
分析：
```c++
class StockSpanner {
public:
    StockSpanner() {
        
    }
    
    int next(int price) {
        int ans = 1;
        while(!stk.empty( ) && stk.top( ).first <= price)
        {
            ans += stk.top().second;
            stk.pop( );
        }
        stk.push({price, ans});
        return ans;
    }
private:
    stack<pair<int, int> > stk;
};
```

# 10.22
## 19
[1235. 规划兼职工作](https://leetcode.cn/problems/maximum-profit-in-job-scheduling/)
标签：动态规划、二分查找
分析：
```c++
class Solution {
public:
    int jobScheduling(vector<int>& startTime, vector<int>& endTime, vector<int>& profit) {
        int n = startTime.size( );
        vector< vector<int>> work(n);
        for(int i=0; i<n; i++)
            work[i] = {startTime[i], endTime[i],profit[i]};
        sort(work.begin(), work.end(), cmp);
        sort(endTime.begin(), endTime.end( ));
        vector<int> dp(n+1);
        dp[0] = 0;
        for(int i=1; i<=n; i++)
        {
            int j = upper_bound(endTime.begin(), endTime.begin( )+i-1, work[i-1][0]) - endTime.begin();
            dp[i] = max(dp[i-1], dp[j]+work[i-1][2]);
        }
        return dp[n];
    }
    static bool cmp(vector<int> v1, vector<int> v2)
    {
        return v1[1] < v2[1];
    }
};
```

# 10.23
## 20
[1768. 交替合并字符串](https://leetcode.cn/problems/merge-strings-alternately/)
标签：模拟、简单题
分析：
```c++
class Solution {
public:
    string mergeAlternately(string word1, string word2) {
        string ans;
        int l1 = word1.length( );
        int l2 = word2.length( );
        int i=0, j=0;
        while(i<l1 || j<l2)
        {
            if(i<l1) ans += word1[i];
            if(j<l2) ans += word2[j];
            if(i < l1) i++;
            if(j < l2) j++;
        }
        return ans;
    }
};
```

# 10.22
## 19
[]()
标签：
分析：
```c++

```

















