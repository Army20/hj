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
