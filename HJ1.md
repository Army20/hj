

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
