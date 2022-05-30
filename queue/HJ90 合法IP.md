
## 牛客网-华为机试练习题 90

### 题目描述

*    现在IPV4下用一个32位无符号整数来表示，一般用点分方式来显示，点将IP地址分成4个部分，每个部分为8位，表示成一个无符号整数（因此不需要用正号出现），如10.137.17.1，是我们非常熟悉的IP地址，一个IP地址串中没有空格出现（因为要表示成一个32数字）。

现在需要你用程序来判断IP是否合法。

注意本题有多组样例输入。

### 输入描述:

+  输入一个ip地址，保证是xx.xx.xx.xx的形式（xx为整数）

### 输出描述:

*  返回判断的结果YES or NO

### 示例1

```
输入：

10.138.15.1
255.0.0.255
255.255.255.1000

输出：

YES
YES
NO


```

### 思路

不满足条件的情况：
1. 长度不为4
2. 某一项不为空
3. 某一项长度大于1时，不能以”0“开头
4. 某一项不介于[0,255]之间
5. 某一项不以“+”开头。
6. 首项不为0
  
### 代码
```Java

package com.example.hj;

import java.util.Scanner;

/**
 * 功能描述
 *
 * @author zWX1011101
 * @since 2022-05-30
 */
public class HJ90 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            String s = scanner.nextLine();
            String[] split = s.split("\\.");
            boolean flag = true;
            if (split.length != 4) {
                flag = false;
            } else {
                for (int i = 0; i < split.length; i++) {
                    if (split[i].trim().length() == 0 || (split[i].length() > 1 &&
                            split[i].startsWith("0")) || Integer.parseInt(split[i]) < 0 || Integer.parseInt(split[i]) > 255 || split[i].startsWith("+")) {
                        flag = false;
                        break;
                    }
                    if (Integer.parseInt(split[0]) == 0) {
                        flag = false;
                        break;
                    }
                }
            }

            if (flag) {
                System.out.println("YES");
            } else {
                System.out.println("NO");
            }
        }
    }
}


```
### 总结
*   
