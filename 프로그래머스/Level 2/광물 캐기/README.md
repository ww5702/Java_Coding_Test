50가지밖에 안되므로 dfs로도 충분히 풀이가 가능하다.   

```
class Solution {
    private static int min;
    public int solution(int[] picks, String[] minerals) {
        int answer = 0;

        min = 987654321;
        int mineralsSize = minerals.length;
        dfs(picks, minerals, mineralsSize, 0, 0);

        answer = min;
        return answer;
    }

    public void dfs(int[] picks, String[] minerals, int mineralsSize, int idx, int fatigue){
        if(idx >= mineralsSize || (picks[0] == 0 && picks[1] == 0 && picks[2] == 0)){
            // System.out.println(fatigue);
            min = Math.min(min, fatigue);
            return;
        }

        if(picks[0] != 0){ // 다이아 곡괭이
            int tmp = mining(0, minerals, mineralsSize, idx, fatigue);
            int[] newPicks = {picks[0]-1, picks[1], picks[2]};
            dfs(newPicks, minerals, mineralsSize, idx+5, tmp);
        }
        if(picks[1] != 0){ // 철 곡괭이
            int tmp = mining(1, minerals, mineralsSize, idx, fatigue);
            int[] newPicks = {picks[0], picks[1]-1, picks[2]};
            dfs(newPicks, minerals, mineralsSize, idx+5, tmp);
        }
        if(picks[2] != 0){ // 돌 곡괭이
            int tmp = mining(2, minerals, mineralsSize, idx, fatigue);
            int[] newPicks = {picks[0], picks[1], picks[2]-1};
            dfs(newPicks, minerals, mineralsSize, idx+5, tmp);
        }
    }

    public int mining(int pick, String[] minerals, int mineralsSize, int idx, int fatigue){
        int tmp = 0;
        for(int i = 0; i<5; i++){ // 곡괭이는 5개 캠
            if(i+idx < mineralsSize){
                tmp += calFatigue(pick, minerals[i+idx]);
            }else{ // 모든 광물 캠                
                break;
            }
        }
        return fatigue+tmp;
    }

    public int calFatigue(int pick, String mineral){
        if(pick == 0){ // 다이아몬드 곡괭이
            return 1;
        }else if(pick == 1){ // 철 곡괭이
            if(mineral.equals("diamond")){
                return 5;
            }else if(mineral.equals("iron")){
                return 1;
            }else if(mineral.equals("stone")){
                return 1;
            }
        }else if(pick == 2){ // 돌 곡괭이
            if(mineral.equals("diamond")){
                return 25;
            }else if(mineral.equals("iron")){
                return 5;
            }else if(mineral.equals("stone")){
                return 1;
            }
        }
        return 0;
    }
}


```
