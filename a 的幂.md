# a的幂
给定一个数字n（整数范围内 2^31-1），确定n是不是数字a的幂。

E.g.

[2的幂](https://leetcode-cn.com/problems/power-of-two/)

[3的幂](https://leetcode-cn.com/problems/power-of-three/)

[4的幂](https://leetcode-cn.com/problems/power-of-four/)


## 通解 

n = i*a^i =>  i * log<sub>a</sub>i = lg(n)/lg(a)

故只需证明i为整数即可

    class Solution {
      public boolean isPowerOfThree(int n) {
        return (Math.log10(n)/Math.log10(a) %1 ==0);        
      }    
    }

## 位运算

二进制中 2的幂为位数上为1的数，故只需证明n在二进制下有且只有一个1
如果n为2的幂，则 n&(n-1)==0

    class Solution {
      public boolean isPowerOfThree(int n) {
        return (n>0 && (n & (n-1) ==0) );        
      }    
    }
    
同理来看 4的幂， 4的幂在必然是2的幂，在二进制表现为奇数位上的数字为1。
可将上述代码改写为

    class Solution {
      public boolean isPowerOfThree(int n) {
        return (n>0 && (n & (n-1) ==0) && (n & 0xaaaaaaaa) == 0 );        
      }    
    }  

注：

0xaaaaaaaa = 10101010101010101010101010101010 (偶数位为1，奇数位为0）

0x55555555 = 1010101010101010101010101010101 (偶数位为0，奇数位为1）

0x33333333 = 110011001100110011001100110011 (1和0每隔两位交替出现)

0xcccccccc = 11001100110011001100110011001100 (0和1每隔两位交替出现)

0x0f0f0f0f = 00001111000011110000111100001111 (1和0每隔四位交替出现)

0xf0f0f0f0 = 11110000111100001111000011110000 (0和1每隔四位交替出现)
