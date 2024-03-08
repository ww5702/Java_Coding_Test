```
class Solution {
    public int[] solution(String[] keymap, String[] targets) {
        int[] answer = new int[targets.length];
        int answerIdx = 0;
        for (String target : targets) {
            String[] cur = target.split("");
            int sum = 0;
            boolean isPossible = true;
            for (String word : cur) {
                //System.out.println(word);
                int touch = Integer.MAX_VALUE;
                for (String key : keymap) {
                    //System.out.println(key.indexOf(word));
                    int index = key.indexOf(word);
                    if (index != -1) {
                        touch = Math.min(touch,index);
                    }
                }
                if (touch == Integer.MAX_VALUE) {
                    isPossible = false;
                    continue;
                } else {
                    sum += touch+1;
                }
            }
            //System.out.println("합: "+sum+isPossible);
            answer[answerIdx++] = isPossible ? sum : -1;

        }
        return answer;
    }
}
```
