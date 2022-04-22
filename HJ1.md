## 牛客网-华为机试练习题 04

### 题目描述

*   密码要求:

    1.长度超过8位

    2.包括大小写字母.数字.其它符号,以上四种至少三种

    3.不能有相同长度超2的子串重复

    说明:长度超过2的子串

### 输入描述:

+   一组或多组长度超过2的子符串。每组占一行

### 输出描述:

*   如果符合要求输出：OK，否则输出NG

### 示例1

#### 输入
```
021Abc9000 021Abc9Abc1 021ABC9000 021$bc9000
```
#### 输出

```
OK NG NG OK
```
### 思路
### 代码
```Java
public class HJ20 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNextLine()) {
            String str = scanner.nextLine();
            if (str.length() < 8 || !checkSpecialChar(str) || checkCommonStr(str)) {
                System.out.println("NG");
            } else {
                System.out.println("OK");
            }
        }
    }

    private static boolean checkCommonStr(String str) {
        for (int i = 0; i < str.length() - 3; i++) {
            String substring = str.substring(i, i + 2);
            String sub = str.substring(i + 1);
            if (sub.contains(substring)) {
                return true;
            }
        }
        return false;
    }

    private static boolean checkSpecialChar(String str) {
        int lowChar = 0;
        int upperChar = 0;
        int numChar = 0;
        int otherChar = 0;
        char[] chars = str.toCharArray();
        for (char c : chars) {
            if (c >= 'a' && c <= 'z') {
                if (lowChar == 0) {
                    lowChar = 1;
                }
            } else if (c >= 'A' && c <= 'Z') {
                if (upperChar == 0) {
                    upperChar = 1;
                }
            } else if (c >= '0' && c <= '9') {
                if (numChar == 0) {
                    numChar = 1;
                }
            } else if (c != ' ' && c != '\n') {
                if (otherChar == 0) {
                    otherChar = 1;
                }
            }
        }
        return lowChar + upperChar + numChar + otherChar >= 3;
    }
}
```
### 总结
