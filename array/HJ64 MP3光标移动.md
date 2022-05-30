## 牛客网-华为机试练习题 10

### 题目描述

*   MP3 Player因为屏幕较小，显示歌曲列表的时候每屏只能显示几首歌曲，用户要通过上下键才能浏览所有的歌曲。为了简化处理，假设每屏只能显示4首歌曲，光标初始的位置为第1首歌。

现在要实现通过上下键控制光标移动来浏览歌曲列表，控制逻辑如下：

歌曲总数<=4的时候，不需要翻页，只是挪动光标位置。

光标在第一首歌曲上时，按Up键光标挪到最后一首歌曲；光标在最后一首歌曲时，按Down键光标挪到第一首歌曲。



其他情况下用户按Up键，光标挪到上一首歌曲；用户按Down键，光标挪到下一首歌曲。



2. 歌曲总数大于4的时候（以一共有10首歌为例）：

特殊翻页：屏幕显示的是第一页（即显示第1 – 4首）时，光标在第一首歌曲上，用户按Up键后，屏幕要显示最后一页（即显示第7-10首歌），同时光标放到最后一首歌上。同样的，屏幕显示最后一页时，光标在最后一首歌曲上，用户按Down键，屏幕要显示第一页，光标挪到第一首歌上。



一般翻页：屏幕显示的不是第一页时，光标在当前屏幕显示的第一首歌曲时，用户按Up键后，屏幕从当前歌曲的上一首开始显示，光标也挪到上一首歌曲。光标当前屏幕的最后一首歌时的Down键处理也类似。



其他情况，不用翻页，只是挪动光标就行。

数据范围：命令长度1\le s\le 100\1≤s≤100 ，歌曲数量1\le n \le 150\1≤n≤150 

进阶：时间复杂度：O(n)\O(n) ，空间复杂度：O(n)\O(n) 


### 输入描述:

+   输入说明：
1 输入歌曲数量
2 输入命令 U或者D

### 输出描述:

*   输出说明
1 输出当前列表
2 输出当前选中歌曲

### 示例1

```
输入：
10
UUUU

输出：
7 8 9 10
7
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
 * @since 2022-05-30
 */
public class HJ64 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            int musicNum = scanner.nextInt();
            scanner.nextLine();
            String command = scanner.nextLine();
            char[] chars = command.toCharArray();
            int[] resultPosition = getResultPosition(chars, musicNum);
            System.out.println(resultPosition[1] + " " + (resultPosition[1] + 1) + " " + (resultPosition[1] + 2) + " " + (resultPosition[1] + 3));
            System.out.println(resultPosition[0]);

        }
    }

    private static int[] getResultPosition(char[] chars, int musicNum) {
        int position = 1;
        int startPosition = 1;
        for (int i = 0; i < chars.length; i++) {
            if (musicNum <= 4) {
                if (chars[i] == 'U') {
                    position--;
                    if (position == 0) {
                        position = musicNum;
                    }
                } else {
                    position++;
                    if (position > musicNum) {
                        position = 1;
                    }
                }
                startPosition = 1;
            } else {
                if (position == 1) {
                    if (chars[i] == 'U') {
                        position = musicNum;
                        startPosition = musicNum - 3;
                    } else {
                        position++;
                        startPosition = 1;
                    }
                } else if (position == musicNum) {
                    if (chars[i] == 'U') {
                        position--;
                        startPosition = musicNum - 3;
                    } else {
                        position = 1;
                        startPosition = 1;
                    }
                } else {
                    if (chars[i] == 'U') {
                        position--;
                    } else {
                        position++;
                    }
                    if (position >= musicNum - 3 && position <= musicNum) {
                        startPosition = musicNum - 3;
                    } else if (startPosition >= 1 && startPosition <= 4) {
                        startPosition = 1;
                    } else {
                        startPosition = position;
                    }
                }
            }
        }
        int[] arr = new int[2];
        arr[0] = position;
        arr[1] = startPosition;
        return arr;
    }
}


```
### 总结
*   获取字符串中某个位置的元素可以用：s.charAt(i);
