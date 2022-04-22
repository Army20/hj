=====
牛客网-华为机试练习题 04

题目描述

•连续输入字符串，请按长度为8拆分每个字符串后输出到新的字符串数组； •长度不是8整数倍的字符串请在后面补数字0，空字符串不处理。

输入描述:
连续输入字符串(输入2次,每个字符串长度小于100)

输出描述:
输出到长度为8的新字符串数组

示例1

输入
```
abc
123456789
```
输出

```
abc00000
12345678
90000000
```
代码
```Java
public class HJ4 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            String s = scanner.nextLine();
            String zero = "00000000";
            int i1 = s.length() % 8;
            String s1 = s + zero.substring(i1);
            int i2 = s1.length() % 8;
            for (int i = 0; i < s.length() % 8 + 1; i++) {
                String substring = s.substring(i * 8, (i + 1) * 8);
                if (substring.length() < 8) {
                    substring = substring + zero.substring(substring.length());
                }
                System.out.println(substring);
            }
        }
    }
}
```
