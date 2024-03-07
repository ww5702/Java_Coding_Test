```
class Solution {
    public int solution(String s) {
        int answer = 0;
        String[] arr = s.split("");
        String versus = "";
        int samecnt = 0;
        int wrongcnt = 0;
        for (int i = 0; i < arr.length; i++) {
            if (versus.equals("")) {
                versus = arr[i];
                samecnt = 1;
                continue;
            } else {
                if (versus.equals(arr[i])) {
                    samecnt += 1;
                } else {
                    wrongcnt += 1;
                }
            }
            
            if (samecnt == wrongcnt) {
                answer += 1;
                versus = "";
                samecnt = 0;
                wrongcnt = 0;
            }
        }
        if (samecnt != wrongcnt) { answer += 1; }
        return answer;
    }
}
```
