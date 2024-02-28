```
class Solution {
    public int solution(int n) {
        String threeJin = Integer.toString(n,3);
        //System.out.println(threeJin);
        StringBuilder sb = new StringBuilder();
        sb.append(threeJin);
        sb.reverse();
        //System.out.println(sb);
        int answer = Integer.parseInt(sb.toString(),3);
        return answer;
    }
}
```
