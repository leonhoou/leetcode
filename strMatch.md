## 字符串匹配算法

暴力法，KMP算法

```
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

/**
 * 字符串匹配算法
 * 所有算法的思想就是
 * 主串s长度为n，模式串p长度为m
 * 1. BF，暴力法：主串包含n-m+1个长度为m的串，依次比较即可；时间复杂度O(n*m)
 * 2. RK算法：比较子串和模式串的哈希值，哈希值相等就说明两个串相等；时间复杂度O(n)
 * 哈希算法：对于字母来说，a-z就是一个26进制的数，转为10进制就是一个哈希值，缺点：串过长时数字太大；
 *         解决：改变hash算法，允许hash冲突，对于hash相同的子串和模式串，再比较一次两个串是否相同即可。
 * 3. KMP算法
 */
class Solution {
public:
    bool bf(string s, string p, int n, int m) {
        for(int i = 0; i < (n-m+1); ++i) {
            int j = 0;
            while(s[i+j] == p[j]) {
                j++;
            }
            if(j == m) return true;
        }
        return false;
    }
    
    /**
     * next数组：对模式串处理，假设长度由1开始的好前缀，我们来看好前缀里面的最长可匹配前缀子串和最长可匹配后缀子串
     * 因为在坏字符前的好前缀说明是可以匹配的，那就滑到好前缀的前缀和后缀相等即可
     * 但是模式串从头开始的任意串都可能是好前缀，所以我们的next数组的索引表示的是模式串字符索引，
     * next取值为最长可匹配前缀子串的结束索引（前缀不包括自己也就是整个模式串不算前缀，前缀长度必须小于模式串长度）
     * 根据这个来计算移动位数，假设主串i和模式串j未匹配（前面都匹配好了），我们找到好前缀0-next[j-1]的最长可匹配前缀，
     * 这个时候怎么移动呢？就是让最长可匹配前缀子串的后面位置元素与坏字符对应起来即可，j就变成了next[j-1]
     */
    int KMP(string s, string p, int n, int m) {
        int* next = getNext(p, m);
        int j = 0;
        for(int i = 0; i < s.size(); ++i) {
            while (j > 0 && s[i] != p[j]) {
                j = next[j-1] + 1;
            }
            // 先判断不等，因为先判断相等j++了，肯定不等了啊
            if(s[i] == p[j]) {
                ++j;
            }
            if(j == m) {
                return i - m + 1;
            }
        }
        return -1;
    }
    
    /**
     * 判断i位置的最大匹配后缀
     * 1. 看前面那位的最大匹配后缀，如果next[i-1]+1 == p[i]，则next[i]=next[i-1]+1
     * 2. abaab abaaa，i指向最后的a。如果不等，i位置的最大匹配后缀肯定比i-1的短（在i-1的基础上z缩短），设i-1的最大前缀串为c，
     * 其实就是找c和c+p[i]的最大前缀和后缀，其实就是c+p[i]的最大匹配，这个时候不就是和上面的求解类似吗？
     * 就是对于abaa新来一个字符a，判断它的最大匹配，如果不等就这样一直走下去
     * 求c+p[i] abaaa 的最大匹配：相当于把abaab的b变为了c，求abaac的最大匹配
     */
    int* getNext(string p, int m) {
        int* next = new int[m];
        next[0] = -1;
        int j = 0;
        for(int i = 1; i < m; ++i) {
            // 前个位置的最长匹配的索引
            j = next[i-1];
            // 如果不等，就缩小，缩小的处理是一样的，所以要先处理不等的情况。
            while(j >= 0 && p[i] != p[j+1]) {
                j = next[j];
            }
            // 如果相等
            if(p[i] == p[j+1]) {
                next[i] = j + 1;
            }
            // 如果i和之前的都匹配不了
            else {
                next[i] = -1;
            }
        }
        for(int i = 0; i < m; ++i) {
            cout << *(next+i) << " ";
        }
        cout << endl;
        return next;
    }
};

int main() {
    Solution* solution = new Solution();
    cout << solution->KMP("abacd", "bac", 5, 3);
    cout << endl;
}

```
