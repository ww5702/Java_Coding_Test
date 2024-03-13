replaceAll 연습문제였다.   
```
class Solution {
    public String solution(String new_id) {
        String answer = "";
        //System.out.println(new_id);
        // 1
        new_id = new_id.toLowerCase();
        //System.out.println(new_id);
        // 2
        new_id = new_id.replaceAll("[^a-z0-9._-]", "");
        //System.out.println(new_id);
        // 3
        new_id = new_id.replaceAll("[.]{2,}", ".");
        //System.out.println(new_id);
        // 4
        new_id = new_id.replaceAll("^[.]|[.]$", "");
        //System.out.println(new_id);
        // 5
        new_id = new_id.isEmpty() ? "a" : new_id;
        //System.out.println(new_id);
        // 6
        new_id = new_id.length() >= 16 ? new_id.substring(0,15) : new_id;
        new_id = new_id.replaceAll("[.]$","");
        //System.out.println(new_id);
        // 7
        if (new_id.length() <= 2) {
            String str = String.valueOf(new_id.charAt(new_id.length()-1));
            new_id += (str.repeat(3-new_id.length()));
        }
        //System.out.println(new_id);
        return new_id;
    }
}
```
