## 牛客网-华为机试练习题 33

### 题目描述

*   整数与IP地址间的转换
```
原理：ip地址的每段可以看成是一个0-255的整数，把每段拆分成一个二进制形式组合起来，然后把这个二进制数转变成
一个长整数。
举例：一个ip地址为10.0.3.193
每段数字             相对应的二进制数
10                   00001010
0                    00000000
3                    00000011
193                  11000001
组合起来即为：00001010 00000000 00000011 11000001,转换为10进制数就是：167773121，即该IP地址转换后的数字就是它了。

的每段可以看成是一个0-255的整数，需要对IP地址进行校验
```

### 输入描述:

+   输入 
    1 输入IP地址
    2 输入10进制型的IP地址

### 输出描述:
```
输出
1 输出转换成10进制的IP地址
2 输出转换后的IP地址

示例1

输入
10.0.3.193
167969729

输出
167773121
10.3.3.193
```

### 思路
### 代码
```Java
package com.example.hj;

import java.util.Scanner;

/**
 * 功能描述
 *
 * @author zWX1011101
 * @since 2022-04-21
 */
public class HJ33 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNextLine()) {
            String ipStr = scanner.nextLine();
            long longStr = Long.parseLong(scanner.nextLine());
            long newIntValue = ip2Int(ipStr);
            System.out.println(newIntValue);
            String s = int2Ip(longStr);
            System.out.println(s);
        }
    }

    private static String int2Ip(long longStr) {
        String s = Long.toBinaryString(longStr);
        String zeroStr = "00000000000000000000000000000000";
        String newStr = "";
        if (s.length() < 32) {
            StringBuffer stringBuffer = new StringBuffer(s);
            stringBuffer.insert(0, zeroStr.toCharArray(), 1, zeroStr.length() - s.length());
            s = stringBuffer.toString();
        }
        for (int i = 0; i < s.length(); i = i + 8) {
            String substring = s.substring(i, i + 8);
            int i1 = Integer.parseInt(substring, 2);
            if (i == 24) {
                newStr += i1;
            } else {
                newStr += i1 + ".";
            }
        }
        return newStr;
    }

    private static long ip2Int(String ipStr) {
        String[] split = ipStr.split("\\.");
        String zeroStr = "00000000";
        String newStr = "";
        for (String str : split) {
            String s = Integer.toBinaryString(Integer.parseInt(str));
            if (s.length() < 8) {
                s = zeroStr.substring(0, 8 - s.length()) + s;
            }
            newStr += s;
        }
        long newIntValue = Long.parseLong(newStr, 2);
        return newIntValue;
    }
}

```
### 总结
