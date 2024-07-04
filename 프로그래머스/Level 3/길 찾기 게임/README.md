트리를 만들어 각 노드의 왼쪽자식노드, 오른쪽자식노드를 만들어준다.   
먼저 트리를 생성하고, 트리를 y축이 큰 순서로 같으면 x축이 작은 순서로 정렬해준다.   
그러면 루트노드는 0번째 인덱스이다.   
그리고 1번부터 순환하며 트리를 만들어준다.   
그리고 전위순회 (루트,좌,우)   
후위순회(좌,우,루트)를 돌아준다.   

```
import java.util.*;
public class Tree {
    int value;
    int x;
    int y;
    Tree leftChild;
    Tree rightChild;
    
    public Tree (int x, int y, int value, Tree leftChild, Tree rightChild) {
        this.x = x;
        this.y = y;
        this.value = value;
        this.leftChild = leftChild;
        this.rightChild = rightChild;
    }
    
}
class Solution {
    int[][] answer = {};
    int idx;
    public int[][] solution(int[][] nodeinfo) {
        Tree[] tree = new Tree[nodeinfo.length];
        for (int i = 0; i < nodeinfo.length; i++) {
            tree[i] = new Tree(nodeinfo[i][0], nodeinfo[i][1], i+1, null, null);
        }
        
        // y값이 큰 순서대로, y값이 같다면 x축이 작은 순서대로
    
        Arrays.sort(tree, new Comparator<Tree>() {
            public int compare(Tree t1, Tree t2) {
                if (t1.y == t2.y) return t1.x - t2.x;
                else return t2.y - t1.y;
            }
        });
        
        // root노드를 만든다.
        Tree root = tree[0];
        System.out.println(root.value);
        for (int i = 1; i < tree.length; i++) {
            insertTree(root, tree[i]);
        }
        // 잘 들어갔는지 확인 4,2 출력
        //System.out.println(root.leftChild.value);
        //System.out.println(root.rightChild.value);
        answer = new int[2][nodeinfo.length];
        idx = 0;
        preorder(root);
        idx = 0;
        postorder(root);
        
        return answer;
    }
    
    public void insertTree(Tree parent, Tree child) {
        // x축이 왼쪽이라면 왼쪽 자식노드로, 근데 왼쪽자식노드에 무언가 있다면 그 무언가의 왼쪽자식노드로
        if (parent.x > child.x) {
            if (parent.leftChild == null) parent.leftChild = child;
            else insertTree(parent.leftChild, child);
        } else {
        // 반대 즉 오른쪽 자식노드
            if (parent.rightChild == null) parent.rightChild = child;
            else insertTree(parent.rightChild, child);
        }
    }
    public void preorder(Tree tree) {
        // null이 나올때까지 전위 순위한 결과는 루트,왼쪽,오른쪽
        if (tree != null) {
            answer[0][idx++] = tree.value;
            preorder(tree.leftChild);
            preorder(tree.rightChild);
        }
    }
    
    public void postorder(Tree tree) {
        // null이 나올때까지 후위 순위한 결과는 왼쪽,오른쪽,루트
        if (tree != null) {
            postorder(tree.leftChild);
            postorder(tree.rightChild);
            answer[1][idx++] = tree.value;
        }
    }
}
```
다른 사람의 풀이 또한 트리를 만들어서 순회한것으로 보인다.   

