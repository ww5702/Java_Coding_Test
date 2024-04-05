1차 풀이   
```
import java.util.*;
import java.util.Arrays;
class Point {
    int sequence;
    String title;
    int time;
    
    public Point(int sequence, String title, int time) {
        this.sequence = sequence;
        this.title = title;
        this.time = time;
    }
}
class Solution {
    public String solution(String m, String[] musicinfos) {
        String answer = "";
        List<Point> result = new ArrayList<>();
        List<String> l = new ArrayList<>();
        int lidx = 0;
        String[] mm = m.split("");
        for (int i = 0; i < mm.length; i++) {
            if (mm[i].equals("#")) {
                l.set(lidx-1, l.get(lidx-1)+"#");
                continue;
            }
            l.add(mm[i]);
            lidx += 1;
        }
        //System.out.println(l.toString());
        int se = 0;
        for (String music: musicinfos) {
            se += 1;
            String[] info = music.split(",");
            String[] start = info[0].split(":");
            String[] end = info[1].split(":");
            String title = info[2];
            int time = timeCal(start, end);
            String[] arr = info[3].split("");
            int idx = 0;
            String[] value = new String[time];
            for (int i = 0; i < time; i++) {
                if (arr[idx].equals("#")) {
                    value[i-1] += "#";
                    idx += 1;
                }
                value[i] = arr[idx++];
                if (idx == arr.length) { idx = 0; }
            }
            //System.out.println(time);
            
            List<String> list = new ArrayList<>(Arrays.asList(value));
            //System.out.println(list.toString());
            //System.out.println(check(l, list));
            if (check(l,list)) {
                result.add(new Point(se, title, time));
            }
        }
        String[][] ans = new String[result.size()][3];
        for (int i = 0; i < result.size(); i++) {
            ans[i][0] = String.valueOf(result.get(i).sequence);
            ans[i][1] = result.get(i).title;
            ans[i][2] = String.valueOf(result.get(i).time);
        }
        Arrays.sort(ans, (o1,o2) -> {
            if (Integer.valueOf(o1[2]) == Integer.valueOf(o2[2])) {
                return Integer.compare(Integer.valueOf(o1[0]), Integer.valueOf(o2[0]));
            } else {
                return Integer.compare(Integer.valueOf(o2[2]), Integer.valueOf(o1[2]));
            }
        });
        
        // for (int i = 0; i < ans.length; i++) {
        //     System.out.println(Arrays.deepToString(ans[i]));
        // }
        if (ans.length == 0) {
            answer = "(None)";
        } else {
            answer = ans[0][1];
        }
        return answer;
    }
    public int timeCal(String[] start, String[] end) {
        int startHour = Integer.valueOf(start[0]) * 60;
        int startMin = Integer.valueOf(start[1]);
        int endHour = Integer.valueOf(end[0]) * 60;
        int endMin = Integer.valueOf(end[1]);
        return (endHour + endMin) - (startHour + startMin);
    }
    public boolean check(List<String> word, List<String> music) {
        for (int i = 0; i < music.size(); i++) {
            if (music.get(i).equals(word.get(0)) && i+word.size() < music.size()-1) {
                boolean isOk = true;
                for (int j = 0; j < word.size(); j++) {
                    if (!music.get(i+j).equals(word.get(j))) {
                        isOk = false;
                        break;
                    }
                }
                if (isOk) {
                    return true;
                }
            }
            
        }
        return false;
    }
}
```
2차 풀이   
각 #들을 U~Z까지 안쓰는 단어로 형성할 경우 더 쉽게 풀이할 수 있다.   
```
class Solution {
    public String solution(String m, String[] musicinfos) {
        String answer = "(None)";
        int time = 0;

        m = edit(m);
        for (int inx = 0; inx < musicinfos.length; inx++) {
            String[] info = musicinfos[inx].split(",");

            int start = (60 * Integer.parseInt(info[0].substring(0, 2)) + Integer.parseInt(info[0].substring(3)));
            int end = (60 * Integer.parseInt(info[1].substring(0, 2)) + Integer.parseInt(info[1].substring(3)));
            int t = end - start;

            if (t > time) {
                info[3] = edit(info[3]);
                StringBuffer sb = new StringBuffer();
                for (int jnx = 0; jnx < t; jnx++) {
                    sb.append(info[3].charAt(jnx % (info[3].length())));
                }
                //System.out.println(sb.toString());
                //System.out.println(sb.toString().indexOf(m));
                if (sb.toString().indexOf(m) >= 0) {
                    answer = info[2];
                    time = t;
                }
            }
        }

        return answer;
    }

    public String edit(String m) {
        m = m.replaceAll("B#", "U");
        m = m.replaceAll("C#", "V");
        m = m.replaceAll("D#", "W");
        m = m.replaceAll("F#", "X");
        m = m.replaceAll("G#", "Y");
        m = m.replaceAll("A#", "Z");

        return m;
    }
}

```
