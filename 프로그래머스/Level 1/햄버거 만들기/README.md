4개 이상 그리고 뒤에서부터 1 3 2 1 이 된다면 +1   
그리고 4개 전으로 돌아가 다시 덮어쓰는 구조로 진행   

```
class Solution {
    public int solution(int[] ingredient) {
        int[] stack = new int[ingredient.length];
        int sp = 0;
        int answer = 0;
        // 1 3 2 1
        for (int i : ingredient) {
            stack[sp++] = i;
            if (sp >= 4 && stack[sp - 1] == 1
                && stack[sp - 2] == 3
                && stack[sp - 3] == 2
                && stack[sp - 4] == 1) {
                sp -= 4;
                answer++;
            }
        }
        return answer;
    }
}
```
