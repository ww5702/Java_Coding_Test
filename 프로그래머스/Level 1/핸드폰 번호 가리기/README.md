```
class Solution {
    public String solution(String phone_number) {
        int index = phone_number.substring(0,phone_number.length()-4).length();
        String answer = ("*".repeat(index));
        return answer+phone_number.substring(index,phone_number.length());
    }
}
```
