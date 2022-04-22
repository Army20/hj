## 牛客网-华为机试练习题 04

### 题目描述

*   提取不重复的整数
*   输入一个 int 型整数，按照从右向左的阅读顺序，返回一个不含重复数字的新的整数。
    保证输入的整数最后一位不是 0 。

    数据范围： 1≤n≤10^8   

### 输入描述:

+   连续输入字符串(输入2次,每个字符串长度小于100)

### 输出描述:

*   按照从右向左的阅读顺序，返回一个不含重复数字的新的整数

### 示例1

#### 输入
```
9876673
```
#### 输出

```
37689
```
### 思路
### 代码
```Java
/**
 * Created by ZAM-PC on 2022/4/3.
 */

import java.util.ArrayList;
import java.util.LinkedHashSet;
import java.util.Scanner;

/**
 * @program: NowCoder
 * @description:
 * @author: zam
 * @create: 2022-04-03
 **/
public class HJ9 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            String s = scanner.nextLine();
            LinkedHashSet<String> set = new LinkedHashSet<>();
            char[] chars = s.toCharArray();
            StringBuffer stringBuffer = new StringBuffer();
            for (int i = chars.length - 1; i >= 0; i--) {
                set.add(String.valueOf(chars[i]));
            }
            ArrayList<String> strings = new ArrayList<>(set);
            for (String string : strings) {
                stringBuffer.append(string);
            }
            System.out.println(stringBuffer);
        }
    }
}

```
### 总结
