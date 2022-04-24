```
public class HJ5 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()) {
            long l = scanner.nextLong();
            StringBuffer s = new StringBuffer(String.valueOf(l));
            StringBuffer reverse = s.reverse();
            System.out.println(reverse.toString());
        }
    }
}
```
