list를 2개 만들어 num1,num2,idx,sum   
을 넣어서 sum을 기준으로 내림차순정렬한다.   
그리고 다시 list를 순환하면서 만약 해당 num1과 num2가 둘다 작은 순간이 있다면   
넣어주지 않았다.   
하지만 실패하는 경우가 있었다.   
80점   

```
import java.util.Arrays;
import java.util.*;
class Point implements Comparable<Point> {
    int num1;
    int num2;
    int idx;
    int sum;
    
    public Point(int num1, int num2, int idx, int sum) {
        this.num1 = num1;
        this.num2 = num2;
        this.idx = idx;
        this.sum = sum;
    }
    
    @Override
    public int compareTo(Point point) {
        if (point.sum < sum) {
            return 1;
        } else if (point.sum > sum) {
            return -1;
        }
        return 0;
    }
    
    @Override    
    public String toString() {        
        return "[ "+ this.num1 + " "+this.num2+" "+this.idx+" "+this.sum+ " ]";
    }
    
    
}
class Solution {
    public int solution(int[][] scores) {
        int answer = 1;
        List<Point> list = new ArrayList<>();
        List<Point> list2 = new ArrayList<>();
        int mynum1 = scores[0][0], mynum2 = scores[0][1];
        int bignum1 = 0, bignum2 = 0, bigsum = 0;
        
        for (int i = 0; i < scores.length; i++) {
            list.add(new Point(scores[i][0], scores[i][1], i, scores[i][0] + scores[i][1]));
        }
        Collections.sort(list, Collections.reverseOrder());
        
        for (int i = 0; i < scores.length; i++) {
            System.out.println(bignum1+" "+bignum2);
            if (i == 0) {
                bignum1 = list.get(i).num1;
                bignum2 = list.get(i).num2;
                bigsum = bignum1 + bignum2;
                list2.add(list.get(i));
            } else {
                if (bigsum == list.get(i).num1 + list.get(i).num2) {
                    if (Math.abs(bignum1 - bignum2) > Math.abs(list.get(i).num1 - list.get(i).num2)) {
                        bignum1 = list.get(i).num1;
                        bignum2 = list.get(i).num2;
                    }
                    list2.add(list.get(i));
                } else {
                    if (bignum1 <= list.get(i).num1 || bignum2 <= list.get(i).num2) {
                        list2.add(list.get(i));
                    }
                }
            }
        }
        
        
        int cnt = 0, tempSum = -1;
        
        for (int i = 0; i < scores.length; i++) {
            int score1 = list2.get(i).num1;
            int score2 = list2.get(i).num2;
            int idx = list2.get(i).idx;
            int sum = list2.get(i).sum;
            System.out.println(list2.get(i));
            System.out.println(answer+" "+cnt+" "+tempSum);
            
            // 만약 못받는 경우    
            if (score1 > mynum1 && score2 > mynum2) {
                answer = -1;
                break;
            }
            
            if (idx == 0) {
                if (tempSum == sum) {
                    break;
                } else {
                    answer += cnt;
                    break;
                }
            }
                
            if (tempSum == -1) {
                cnt += 1;
                tempSum = sum;
                continue;
            }
                
            if (tempSum == sum) {
                cnt += 1;
            } else if (tempSum > sum) {
                answer += cnt;
                cnt = 1;
                tempSum = sum;
            }
            System.out.println(answer+" "+cnt+" "+tempSum);
        }
        System.out.println(answer);
        
        return answer;
    }
}
```
