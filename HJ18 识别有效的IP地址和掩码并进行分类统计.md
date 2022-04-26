## 牛客网-华为机试练习题 18

### 题目描述

*   编写一个函数，计算字符串中含有的不同字符的个数。字符在 ASCII 码范围内( 0~127 ，包括 0 和 127 )，换行表示结束符，不算在字符里。不在范围内的不作统计。多个相同的字符只计算一次
    例如，对于字符串 abaca 而言，有 a、b、c 三种不同的字符，因此输出 3 。

    数据范围： 1≤n≤500  

### 输入描述:

+   输入一行没有空格的字符串。

### 输出描述:

*   输出 输入字符串 中范围在(0~127，包括0和127)字符的种数。

### 示例1

```
输入：
abc

输出：
3
```
### 示例2
```
输入：
aaa

输出：
1
```
### 思路
### 代码
```Java

package com.example.hj;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Scanner;

/**
 * 功能描述
 *
 * @author zWX1011101
 * @since 2022-04-24
 */
public class HJ18 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
//        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        while (scanner.hasNext()) {
            int size = 4;
            List<String> ipList = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                ipList.add(scanner.nextLine());
            }
            int errorIpNum = 0;
            int AIpNum = 0;
            int BIpNum = 0;
            int CIpNum = 0;
            int DIpNum = 0;
            int EIpNum = 0;
            int privateIpNum = 0;
            for (String ipMask : ipList) {
                String[] split = ipMask.split("~");
                if (split.length != 2) {
                    errorIpNum++;
                    continue;
                }
                String ip = split[0];
                String mask = split[1];
                String[] ipArr = ip.split("\\.");
                int integer = Integer.parseInt(ipArr[0]);
                if (integer == 0 || integer == 127) {
                    continue;
                }
                if (!invalidIp(ip) || !invalidMask(mask)) {
                    errorIpNum++;
                    continue;
                }
                if (isAip(integer)) {
                    AIpNum++;
                    if (isPrivateIp(ip)) {
                        privateIpNum++;
                    }
                    continue;
                } else if (isBIp(integer)) {
                    BIpNum++;
                    if (isPrivateIp(ip)) {
                        privateIpNum++;
                    }
                    continue;
                } else if (isCIp(integer)) {
                    CIpNum++;
                    if (isPrivateIp(ip)) {
                        privateIpNum++;
                    }
                    continue;
                } else if (isDIp(integer)) {
                    DIpNum++;
                    continue;
                } else if (isEIp(integer)) {
                    EIpNum++;
                    continue;
                } else {
                    errorIpNum++;
                }
            }
            System.out.println(AIpNum + " " + BIpNum + " " +
                    CIpNum + " " + DIpNum + " " + EIpNum + " " + errorIpNum + " " + privateIpNum);
        }
    }

    private static boolean invalidMask(String mask) {
        if (!invalidIp(mask)) {
            return false;
        }
        String[] maskStr = mask.split("\\.");
        String zero = "00000000";
        String binaryStr = "";
        for (int i = 0; i < maskStr.length; i++) {
            String s = Integer.toBinaryString(Integer.valueOf(maskStr[i]));
            binaryStr += zero.substring(0, 8 - s.length()) + s;
        }
        int count = 0;
        for (int i = 0; i < binaryStr.length() - 1; i++) {
            // 相邻2个是否相等，不相等计数
            if (binaryStr.charAt(i) != binaryStr.charAt(i + 1)) {
                count++;
                if (count >= 2) {
                    return false;
                }
            }
        }
        // 全为0或全为1
        if (count == 0) {
            return false;
        }
        return true;
    }

    private static boolean invalidIp(String ip) {
        // 长度是否为4
        String[] ipStr = ip.split("\\.");
        if (ipStr.length != 4) {
            return false;
        }

        for (String id : ipStr) {
            // 每个是否是0-9
            for (int i = 0; i < id.length(); i++) {
                if (id.charAt(i) < '0' || id.charAt(i) > '9') {
                    return false;
                }
            }
            // 是否是0-255之间
            Integer integer = Integer.valueOf(id);
            if (integer < 0 || integer > 255) {
                return false;
            }
        }
        return true;

    }

    private static boolean isPrivateIp(String ip) {
        String[] ipArr = ip.split("\\.");
        int ip0 = Integer.parseInt(ipArr[0]);
        int ip1 = Integer.parseInt(ipArr[1]);
        if (ip0 == 10 || (ip0 == 172 && ip1 >= 16 && ip1 <= 31) || (ip0 == 192 && ip1 == 168)) {
            return true;
        }
        return false;
    }

    private static boolean isEIp(int integer) {
        if (integer >= 240 && integer <= 255) {
            return true;
        }
        return false;
    }

    private static boolean isDIp(int integer) {
        if (integer >= 224 && integer <= 239) {
            return true;
        }
        return false;
    }

    private static boolean isCIp(int integer) {
        if (integer >= 192 && integer <= 223) {
            return true;
        }
        return false;
    }

    private static boolean isBIp(int integer) {
        if (integer >= 128 && integer <= 191) {
            return true;
        }
        return false;
    }


    private static boolean isAip(int integer) {
        if (integer >= 1 && integer <= 126) {
            return true;
        }
        return false;
    }
}


```

```Java
package com.example.hj;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

/**
 * 功能描述
 *
 * @author zWX1011101
 * @since 2022-04-25
 */
public class HJ18Copy {
    public static void main(String[] args) throws IOException {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        String str ;
        while ((str=br.readLine())!=null) {
            int errorIpNum = 0;
            int AIpNum = 0;
            int BIpNum = 0;
            int CIpNum = 0;
            int DIpNum = 0;
            int EIpNum = 0;
            int privateIpNum = 0;
//            for (String str : ipList) {
                String[] split = str.split("~");
                if (split.length != 2) {
                    errorIpNum++;
                    continue;
                }
                String ip = split[0];
                String mask = split[1];
                String[] ipArr = ip.split("\\.");
                int integer = Integer.parseInt(ipArr[0]);
                if (integer == 0 || integer == 127) {
                    continue;
                }
                if (!invalidIp(ip) || !invalidMask(mask)) {
                    errorIpNum++;
                    continue;
                }
                if (isAip(integer)) {
                    AIpNum++;
                    if (isPrivateIp(ip)) {
                        privateIpNum++;
                    }
                    continue;
                } else if (isBIp(integer)) {
                    BIpNum++;
                    if (isPrivateIp(ip)) {
                        privateIpNum++;
                    }
                    continue;
                } else if (isCIp(integer)) {
                    CIpNum++;
                    if (isPrivateIp(ip)) {
                        privateIpNum++;
                    }
                    continue;
                } else if (isDIp(integer)) {
                    DIpNum++;
                    continue;
                } else if (isEIp(integer)) {
                    EIpNum++;
                    continue;
                } else {
                    errorIpNum++;
                }
//            }
            System.out.println(AIpNum + " " + BIpNum + " " +
                    CIpNum + " " + DIpNum + " " + EIpNum + " " + errorIpNum + " " + privateIpNum);
        }
    }

    private static boolean invalidMask(String mask) {
        if (!invalidIp(mask)) {
            return false;
        }
        String[] maskStr = mask.split("\\.");
        String zero = "00000000";
        String binaryStr = "";
        for (int i = 0; i < maskStr.length; i++) {
            String s = Integer.toBinaryString(Integer.valueOf(maskStr[i]));
            binaryStr += zero.substring(0, 8 - s.length()) + s;
        }
        int count = 0;
        for (int i = 0; i < binaryStr.length() - 1; i++) {
            // 相邻2个是否相等，不相等计数
            if (binaryStr.charAt(i) != binaryStr.charAt(i + 1)) {
                count++;
                if (count >= 2) {
                    return false;
                }
            }
        }
        // 全为0或全为1
        if (count == 0) {
            return false;
        }
        return true;
    }

    private static boolean invalidIp(String ip) {
        // 长度是否为4
        String[] ipStr = ip.split("\\.");
        if (ipStr.length != 4) {
            return false;
        }

        for (String id : ipStr) {
            // 每个是否是0-9
            for (int i = 0; i < id.length(); i++) {
                if (id.charAt(i) < '0' || id.charAt(i) > '9') {
                    return false;
                }
            }
            // 是否是0-255之间
            Integer integer = Integer.valueOf(id);
            if (integer < 0 || integer > 255) {
                return false;
            }
        }
        return true;

    }

    private static boolean isPrivateIp(String ip) {
        String[] ipArr = ip.split("\\.");
        int ip0 = Integer.parseInt(ipArr[0]);
        int ip1 = Integer.parseInt(ipArr[1]);
        if (ip0 == 10 || (ip0 == 172 && ip1 >= 16 && ip1 <= 31) || (ip0 == 192 && ip1 == 168)) {
            return true;
        }
        return false;
    }

    private static boolean isEIp(int integer) {
        if (integer >= 240 && integer <= 255) {
            return true;
        }
        return false;
    }

    private static boolean isDIp(int integer) {
        if (integer >= 224 && integer <= 239) {
            return true;
        }
        return false;
    }

    private static boolean isCIp(int integer) {
        if (integer >= 192 && integer <= 223) {
            return true;
        }
        return false;
    }

    private static boolean isBIp(int integer) {
        if (integer >= 128 && integer <= 191) {
            return true;
        }
        return false;
    }


    private static boolean isAip(int integer) {
        if (integer >= 1 && integer <= 126) {
            return true;
        }
        return false;
    }
}

```

### 总结
*   获取字符串中某个位置的元素可以用：s.charAt(i);
