```
class Solution {
    public String solution(int[] food) {
        String answer = "";
        StringBuilder sb = new StringBuilder();
        
        for (int i = 1; i < food.length; i++) {
            int num = food[i]/2;
            sb.append(Integer.toString(i).repeat(num));
        }
        sb.reverse();
        String reversed = sb.toString();
        sb.reverse();
        sb.append("0");
        sb.append(reversed);
        System.out.println(sb);
        return sb.toString();
    }
}
```
