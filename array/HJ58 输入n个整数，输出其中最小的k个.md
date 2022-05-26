## 牛客网-华为机试练习题 58

### 题目描述

*   输入n个整数，输出其中最小的k个。

    本题有多组输入样例，请使用循环读入，比如while(cin>>)等方式处理

### 输入描述:

+   第一行输入两个整数n和k
    第二行输入一个整数数组

### 输出描述:

*  输出一个从小到大排序的整数数组

### 示例1

```
输入：

5 2
1 3 5 7 2

输出：
1 2
```
### 思路
*   
### 代码

```Java
方法一：
package com.example.hj;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;

/**
 * 功能描述
 *
 * @author zWX1011101
 * @since 2022-05-26
 */
public class HJ58 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            String[] s = scanner.nextLine().split(" ");
            String[] s1 = scanner.nextLine().split(" ");
            ArrayList<Integer> list = new ArrayList<>();
            for (int i = 0; i < Integer.parseInt(s[0]); i++) {
                list.add(Integer.parseInt(s1[i]));
            }
            Collections.sort(list);
            for (int i =0 ;i<Integer.parseInt(s[1]);i++){
                System.out.print(list.get(i)+" ");
            }
        }
    }
}


方法二：
package com.example.hj;

import java.util.Arrays;
import java.util.Scanner;

/**
 * 功能描述
 *
 * @author zWX1011101
 * @since 2022-05-26
 */
public class HJ58 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            int n = scanner.nextInt();
            int k = scanner.nextInt();
            int[] arr = new int[n];
            for (int i = 0; i < n; i++) {
                arr[i] = scanner.nextInt();
            }
            Arrays.sort(arr);
            for (int i = 0; i < k; i++) {
                System.out.print(arr[i] + " " );
            }
        }
    }
}

```
### 总结
*  scanner.nextInt: 返回为int。只读取数值，以数值结束接收。
   scanner.nextLine: 返回为String，以"\n"结束接收。
   scanner.next:返回为string。以空格或者TAB 结束接收。
   https://blog.csdn.net/qq_41620270/article/details/120582910

   1.   数组排序:升序：Arrays.sort(arr);

   2.   数组排序：降序：new Comparator，实现compare方法。Comparator用于构造基本数据类型的比较器时，只能对基本类型的包装类进行排序，也就是说只能传入包装类的数组，这里我们需要首先把int[]转为Integer[]
   
```Java
public class Main {
    public static void main(String[] args) {
        // 数组初始化
        Integer[] arr = new Integer[]{1,2,3,65,5};
        // 降序排序
        Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return (int) o2 - o1;
            }
        });

        for (Integer pageSize : arr) {
            System.out.print(pageSize + " ");
        }
    }
}
        
输出： 65 5 3 2 1 

```
