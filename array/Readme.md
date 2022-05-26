## 牛客网-华为机试练习题 34

### 题目描述

*   Lily上课时使用字母数字图片教小朋友们学习英语单词，每次都需要把这些图片按照大小（ASCII码值从小到大）排列收好。请大家给Lily帮忙，通过C语言解决。

    本题含有多组样例输入

### 输入描述:

+   Lily使用的图片包括"A"到"Z"、"a"到"z"、"0"到"9"。输入字母或数字个数不超过1024。

### 输出描述:

*  Lily的所有图片按照从小到大的顺序输出

### 示例1

```
输入：
Ihave1nose2hands10fingers

输出：
0112Iaadeeefghhinnnorsssv
```
### 思路
*   字符串转为字符数组，再转为list，利用Collections.sort(list)排序。升序排序。
### 代码
```Java
package com.example.hj;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;

/**
 * 功能描述
 *
 * @author zWX1011101
 * @since 2022-05-25
 */
public class HJ34 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            String s = scanner.nextLine();
//        String s = "Ihave1nose2hands10fingers";
            ArrayList<Character> list = new ArrayList<>();
            char[] chars = s.toCharArray();
            for (char c : chars) {
                list.add(c);
            }
            // list升序排序：Collections.sort(list);
            // list降序排序：Collections.sort(list, Collections.reverseOrder());
            Collections.sort(list);
            for (int i = 0; i < list.size(); i++) {
                System.out.print(list.get(i));
            }
        }
    }
}



```
### 总结
*   list升序排序：Collections.sort(list);
*   list降序排序：Collections.sort(list, Collections.reverseOrder());
