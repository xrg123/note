<!-- GFM-TOC -->
* [�ڶ��� ������Ҫ�Ļ���֪ʶ](#�ڶ���-������Ҫ�Ļ���֪ʶ)
    * [2. ʵ�� Singleton](#2-ʵ��-singleton)
    * [3. �������ظ�������](#3-�������ظ�������)
    * [4. ��ά�����еĲ���](#4-��ά�����еĲ���)
    * [5. �滻�ո�](#5-�滻�ո�)
    * [6. ��β��ͷ��ӡ����](#6-��β��ͷ��ӡ����)
    * [7. �ؽ�������](#7-�ؽ�������)
    * [8. ����������һ�����](#8-����������һ�����)
    * [9. ������ջʵ�ֶ���](#9-������ջʵ�ֶ���)
    * [10.1 쳲���������](#101-쳲���������)
    * [10.2 ��̨��](#102-��̨��)
    * [10.3 ��̬��̨��](#103-��̬��̨��)
    * [10.4 ���θ���](#104-���θ���)
    * [11. ��ת�������С����](#11-��ת�������С����)
    * [12. �����е�·��](#12-�����е�·��)
    * [13. �����˵��˶���Χ](#13-�����˵��˶���Χ)
    * [14. ������](#14-������)
    * [15. �������� 1 �ĸ���](#15-��������-1-�ĸ���)
* [������ �������Ĵ���](#������-�������Ĵ���)
    * [16. ��ֵ�������η�](#16-��ֵ�������η�)
    * [18. ɾ���������ظ��Ľ��](#18-ɾ���������ظ��Ľ��)
    * [19. ������ʽƥ��](#19-������ʽƥ��)
    * [20. ��ʾ��ֵ���ַ���](#20-��ʾ��ֵ���ַ���)
    * [21. ��������˳��ʹ����λ��ż��ǰ��](#21-��������˳��ʹ����λ��ż��ǰ��)
    * [22. �����е����� k �����](#22-�����е�����-k-�����)
    * [23. �����л�����ڽ��](#23-�����л�����ڽ��)
    * [24. ��ת����](#24-��ת����)
    * [25. �ϲ��������������](#25-�ϲ��������������)
    * [26. �����ӽṹ](#26-�����ӽṹ)
* [������ ����������˼·](#������-����������˼·)
    * [27. �������ľ���](#27-�������ľ���)
    * [28.1 �ԳƵĶ�����](#281-�ԳƵĶ�����)
    * [28.2 ƽ�������](#282-ƽ�������)
    * [29. ˳ʱ���ӡ����](#29-˳ʱ���ӡ����)
    * [30. ���� min ������ջ](#30-����-min-������ջ)
    * [31. ջ��ѹ�롢��������](#31-ջ��ѹ�뵯������)
    * [32.1 �������´�ӡ������](#321-�������´�ӡ������)
    * [32.3  �Ѷ�������ӡ�ɶ���](#323--�Ѷ�������ӡ�ɶ���)
    * [32.3 ��֮����˳���ӡ������](#323-��֮����˳���ӡ������)
    * [33. �����������ĺ����������](#33-�����������ĺ����������)
    * [34. �������к�Ϊĳһֵ��·��](#34-�������к�Ϊĳһֵ��·��)
    * [35. ��������ĸ���](#35-��������ĸ���)
    * [36. ������������˫������](#36-������������˫������)
    * [37. ���л�������](#37-���л�������)
    * [38. �ַ���������](#38-�ַ���������)
* [������ �Ż�ʱ��Ϳռ�Ч��](#������-�Ż�ʱ��Ϳռ�Ч��)
    * [39. �����г��ִ�������һ�������](#39-�����г��ִ�������һ�������)
    * [40. ��С�� K ����](#40-��С��-k-����)
    * [41.1 �������е���λ��](#411-�������е���λ��)
    * [14.2 �ַ����е�һ�����ظ����ַ�](#142-�ַ����е�һ�����ظ����ַ�)
    * [42. ���������������](#42-���������������)
    * [43. �� 1 �� n ������ 1 ���ֵĴ���](#43-��-1-��-n-������-1-���ֵĴ���)
    * [45. �������ų���С����](#45-�������ų���С����)
    * [49. ����](#49-����)
    * [50. ��һ��ֻ����һ�ε��ַ�λ��](#50-��һ��ֻ����һ�ε��ַ�λ��)
    * [51. �����е������](#51-�����е������)
    * [52. ��������ĵ�һ���������](#52-��������ĵ�һ���������)
* [������ �����еĸ�������](#������-�����еĸ�������)
    * [53 ���������������г��ֵĴ���](#53-���������������г��ֵĴ���)
    * [54. �����������ĵ� k �����](#54-�����������ĵ�-k-�����)
    * [55 �����������](#55-�����������)
    * [56. ������ֻ����һ�ε�����](#56-������ֻ����һ�ε�����)
    * [57.1 ��Ϊ S ����������](#571-��Ϊ-s-����������)
    * [57.2 ��Ϊ S ��������������](#572-��Ϊ-s-��������������)
    * [58.1 ��ת����˳����](#581-��ת����˳����)
    * [58.2 ����ת�ַ���](#582-����ת�ַ���)
    * [59. �������ڵ����ֵ](#59-�������ڵ����ֵ)
    * [61. �˿���˳��](#61-�˿���˳��)
    * [62. ԲȦ�����ʣ�µ���](#62-ԲȦ�����ʣ�µ���)
* [63. ��Ʊ���������](#63-��Ʊ���������)
    * [64. �� 1+2+3+...+n](#64-��-1+2+3++n)
    * [65. ���üӼ��˳����ӷ�](#65-���üӼ��˳����ӷ�)
    * [66. �����˻�����](#66-�����˻�����)
* [������ �������԰���](#������-�������԰���)
    * [67. ���ַ���ת��������](#67-���ַ���ת��������)
    * [68. ���������ڵ����͹�������](#68-���������ڵ����͹�������)
      <!-- GFM-TOC -->

# �ڶ��� ������Ҫ�Ļ���֪ʶ

## 2. ʵ�� Singleton

**����ʵ��**

����ʵ���У�˽�о�̬�������ӳٻ�ʵ�������������ĺô��ǣ����û���õ����࣬��ô�Ͳ��ᴴ����˽�о�̬�������Ӷ���Լ��Դ�����ʵ���ڶ��̻߳������ǲ���ȫ�ģ���Ϊ����߳��ܹ�ͬʱ���� if(uniqueInstance == null) �ڵ����飬��ô�ͻ���ʵ���� uniqueInstance ˽�о�̬������

```java
public class Singleton {
    private static Singleton uniqueInstance;
    private Singleton() {
    }
    public static Singleton getUniqueInstance() {
        if (uniqueInstance == null) {
            uniqueInstance = new Singleton();
        }
        return uniqueInstance;
    }
}
```

**�̲߳���ȫ����Ľ������һ**

ֻ��Ҫ�� getUniqueInstance() ���������������ø÷���һ��ֻ��һ���̷߳��ʣ��Ӷ������˶� uniqueInstance �������ж��ʵ���������⡣����������һ��������һ��ֻ��һ���߳̽��룬�����ϻ���һ�����˷ѡ�

```java
public static synchronized Singleton getUniqueInstance() {
    if (uniqueInstance == null) {
        uniqueInstance = new Singleton();
    }
    return uniqueInstance;
}
```
**�̲߳���ȫ����Ľ��������**

�����ӳ�ʵ����������ֱ��ʵ������

```java
private static Singleton uniqueInstance = new Singleton();
```

**�̲߳���ȫ����Ľ��������**

���ǵ�һ���������������ֱ�Ӷ� getUniqueInstance() �������м�������ʵ����ֻ��Ҫ�� uniqueInstance = new Singleton(); �������������ɡ�ʹ����������������ж� uniqueInstance �Ƿ��Ѿ�ʵ���������û��ʵ��������Ҫ������

```java
public class Singleton {
    private volatile static Singleton uniqueInstance;
    private Singleton() {
    }
    public static synchronized Singleton getUniqueInstance() {
        if (uniqueInstance == null) {
            synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```

## 3. �������ظ�������

**��Ŀ����**

��һ������Ϊ n ����������������ֶ��� 0 �� n-1 �ķ�Χ�ڡ� ������ĳЩ�������ظ��ģ�����֪���м����������ظ��ġ�Ҳ��֪��ÿ�������ظ����Ρ����ҳ�����������һ���ظ������֡� ���磬������볤��Ϊ 7 ������ {2, 3, 1, 0, 2, 5, 3}����ô��Ӧ������ǵ�һ���ظ������� 2��

**����˼·**

��������Ԫ���� [0, n-1] ��Χ�ڵ����⣬���Խ�ֵΪ i ��Ԫ�طŵ��� i ��λ���ϡ�

```java
public boolean duplicate(int numbers[], int length, int[] duplication) {
    for (int i = 0; i < length; i++) {
        while (numbers[i] != i && numbers[i] != numbers[numbers[i]]) {
            swap(numbers, i, numbers[i]);
        }
        if (numbers[i] != i && numbers[i] == numbers[numbers[i]]) {
            duplication[0] = numbers[i];
            return true;
        }
    }
    return false;
}

private void swap(int[] numbers, int i, int j) {
    int t = numbers[i];
    numbers[i] = numbers[j];
    numbers[j] = t;
}
```

## 4. ��ά�����еĲ���

**��Ŀ����**

��һ����ά�����У�ÿһ�ж����մ����ҵ�����˳������ÿһ�ж����մ��ϵ��µ�����˳�����������һ������������������һ����ά�����һ���������ж��������Ƿ��и�������

```java
public boolean Find(int target, int [][] array) {
    if (array == null || array.length == 0 || array[0].length == 0) return false;
    int m = array.length, n = array[0].length;
    int row = 0, col = n - 1;
    while (row < m && col >= 0) {
        if (target == array[row][col]) return true;
        else if (target < array[row][col]) col--;
        else row++;
    }
    return false;
}
```

## 5. �滻�ո�

**��Ŀ����**

��ʵ��һ����������һ���ַ����еĿո��滻�ɡ�%20�������磬���ַ���Ϊ We Are Happy. �򾭹��滻֮����ַ���Ϊ We%20Are%20Happy��

**��ĿҪ��**

�� O(1) �Ŀռ临�Ӷ�����⡣

```java
public String replaceSpace(StringBuffer str) {
    int n = str.length();
    for (int i = 0; i < n; i++) {
        if (str.charAt(i) == ' ') str.append("  "); // β���������
    }

    int idxOfOriginal = n - 1;
    int idxOfNew = str.length() - 1;
    while (idxOfOriginal >= 0 && idxOfNew > idxOfOriginal) {
        if (str.charAt(idxOfOriginal) == ' ') {
            str.setCharAt(idxOfNew--, '0');
            str.setCharAt(idxOfNew--, '2');
            str.setCharAt(idxOfNew--, '%');
        } else {
            str.setCharAt(idxOfNew--, str.charAt(idxOfOriginal));
        }
        idxOfOriginal--;
    }
    return str.toString();
}
```

## 6. ��β��ͷ��ӡ����

�������Ȼ����� Collections.reverse().

```java
public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
    ArrayList<Integer> ret = new ArrayList<>();
    while (listNode != null) {
        ret.add(listNode.val);
        listNode = listNode.next;
    }
    Collections.reverse(ret);
    return ret;
}
```

�ݹ�

```java
public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
    ArrayList<Integer> ret = new ArrayList<>();
    if(listNode != null) {
        ret.addAll(printListFromTailToHead(listNode.next));
        ret.add(listNode.val);
    }
    return ret;
}
```

��ʹ�ÿ⺯�������Ҳ�ʹ�õݹ�ĵ���ʵ�֣����������ͷ�巨Ϊ��������ԡ�

```java
public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
    ListNode head = new ListNode(-1); // ͷ���
    ListNode cur = listNode;
    while (cur != null) {
        ListNode next = cur.next;
        cur.next = head.next;
        head.next = cur;
        cur = next;
    }
    ArrayList<Integer> ret = new ArrayList<>();
    head = head.next;
    while (head != null) {
        ret.add(head.val);
        head = head.next;
    }
    return ret;
}
```

## 7. �ؽ�������

**��Ŀ����**

����ĳ��������ǰ���������������Ľ�������ؽ����ö����������������ǰ���������������Ľ���ж������ظ������֡�

```java
public TreeNode reConstructBinaryTree(int[] pre, int[] in) {
    return reConstructBinaryTree(pre, 0, pre.length - 1, in, 0, in.length - 1);
}
private TreeNode reConstructBinaryTree(int[] pre, int preL, int preR, int[] in, int inL, int inR) {
    if(preL > preR || inL > inR) return null;
    TreeNode root = new TreeNode(pre[preL]);
    if (preL != preR) {
        int idx = inL;
        while (idx <= inR && in[idx] != root.val) idx++;
        int leftTreeLen = idx - inL;
        root.left = reConstructBinaryTree(pre, preL + 1, preL + leftTreeLen, in, inL, inL + leftTreeLen - 1);
        root.right = reConstructBinaryTree(pre, preL + leftTreeLen + 1, preR, in, inL + leftTreeLen + 1, inR);
    }
    return root;
}
```

## 8. ����������һ�����

**��Ŀ����**

����һ�������������е�һ����㣬���ҳ��������˳�����һ����㲢�ҷ��ء�ע�⣬���еĽ�㲻�����������ӽ�㣬ͬʱ����ָ�򸸽���ָ�롣

```java
public TreeLinkNode GetNext(TreeLinkNode pNode) {
    if (pNode == null) return null;
    if (pNode.right != null) {
        pNode = pNode.right;
        while (pNode.left != null) pNode = pNode.left;
        return pNode;
    } else {
        TreeLinkNode parent = pNode.next;
        while (parent != null) {
            if (parent.left == pNode) return parent;
            pNode = pNode.next;
            parent = pNode.next;
        }
    }
    return null;
}
```

## 9. ������ջʵ�ֶ���

```java
Stack<Integer> stack1 = new Stack<Integer>();
Stack<Integer> stack2 = new Stack<Integer>();

public void push(int node) {
    stack1.push(node);
}

public int pop() {
    if (stack2.isEmpty()) {
        while (!stack1.isEmpty()) {
            stack2.push(stack1.pop());
        }
    }
    return stack2.pop();
}
```

## 10.1 쳲���������

```java
private int[] fib = new int[40];

public Solution() {
    fib[1] = 1;
    fib[2] = 2;
    for (int i = 2; i < fib.length; i++) {
        fib[i] = fib[i - 1] + fib[i - 2];
    }
}

public int Fibonacci(int n) {
    return fib[n];
}
```

## 10.2 ��̨��

```java
public int JumpFloor(int target) {
    if (target == 1) return 1;
    int[] dp = new int[target];
    dp[0] = 1;
    dp[1] = 2;
    for (int i = 2; i < dp.length; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[target - 1];
}
```

## 10.3 ��̬��̨��

```java
public int JumpFloorII(int target) {
    int[] dp = new int[target];
    Arrays.fill(dp, 1);
    for (int i = 1; i < target; i++) {
        for (int j = 0; j < i; j++) {
            dp[i] += dp[j];
        }
    }
    return dp[target - 1];
}
```

## 10.4 ���θ���

**��Ŀ����**

���ǿ����� 2\*1 ��С���κ��Ż�������ȥ���Ǹ���ľ��Ρ������� n �� 2\*1 ��С�������ص��ظ���һ�� 2\*n �Ĵ���Σ��ܹ��ж����ַ�����

```java
public int RectCover(int target) {
    if (target <= 2) return target;
    return RectCover(target - 1) + RectCover(target - 2);
}
```


## 11. ��ת�������С����

**��Ŀ����**

��һ�������ʼ�����ɸ�Ԫ�ذᵽ�����ĩβ�����ǳ�֮Ϊ�������ת�� ����һ���ǵݼ�����������һ����ת�������ת�������СԪ�ء� �������� {3, 4, 5, 1, 2} Ϊ {1, 2, 3, 4, 5} ��һ����ת�����������СֵΪ 1�� NOTE������������Ԫ�ض����� 0���������СΪ 0���뷵�� 0��

```java
public int minNumberInRotateArray(int[] array) {
    if (array.length == 0) return 0;
    for (int i = 0; i < array.length - 1; i++) {
        if (array[i] > array[i + 1]) return array[i + 1];
    }
    return 0;
}
```

## 12. �����е�·��

**��Ŀ����**

�����һ�������������ж���һ���������Ƿ����һ������ĳ�ַ��������ַ���·����·�����ԴӾ����е�����һ�����ӿ�ʼ��ÿһ�������ھ������������ң����ϣ������ƶ�һ�����ӡ����һ��·�������˾����е�ĳһ�����ӣ����·�������ٽ���ø��ӡ� ���� a b c e s f c s a d e e �����а���һ���ַ��� "bcced" ��·�������Ǿ����в����� "abcb" ·������Ϊ�ַ����ĵ�һ���ַ� b ռ���˾����еĵ�һ�еڶ�������֮��·�������ٴν���ø��ӡ�

```java
private int[][] next = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};

public boolean hasPath(char[] matrix, int rows, int cols, char[] str) {
    if (rows == 0 || cols == 0) return false;
    char[][] m = new char[rows][cols];
    for (int i = 0, idx = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            m[i][j] = matrix[idx++];
        }
    }

    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            if (backtracking(m, rows, cols, str, new boolean[rows][cols], 0, i, j)) return true;
        }
    }
    return false;
}

private boolean backtracking(char[][] m, int rows, int cols, char[] str, boolean[][] used, int path, int r, int c) {
    if (path == str.length) return true;
    if (r < 0 || r >= rows || c < 0 || c >= cols) return false;
    if (m[r][c] != str[path]) return false;
    if (used[r][c]) return false;
    used[r][c] = true;
    for (int i = 0; i < next.length; i++) {
        if (backtracking(m, rows, cols, str, used, path + 1, r + next[i][0], c + next[i][1])) return true;
    }
    used[r][c] = false;
    return false;
}
```


## 13. �����˵��˶���Χ

**��Ŀ����**

������һ�� m �к� n �еķ���һ�������˴����� 0, 0 �ĸ��ӿ�ʼ�ƶ���ÿһ��ֻ�������ң��ϣ����ĸ������ƶ�һ�񣬵��ǲ��ܽ�������������������λ֮�ʹ��� k �ĸ��ӡ� ���磬�� k Ϊ 18 ʱ���������ܹ����뷽��35, 37������Ϊ 3+5+3+7 = 18�����ǣ������ܽ��뷽��35, 38������Ϊ 3+5+3+8 = 19�����ʸû������ܹ��ﵽ���ٸ����ӣ�

```java
private int cnt = 0;
private int[][] next = {{0, -1}, {0, 1}, {-1, 0}, {1, 0}};
private int[][] digitSum;

public int movingCount(int threshold, int rows, int cols) {
    initDigitSum(rows, cols);
    dfs(new boolean[rows][cols], threshold, rows, cols, 0, 0);
    return cnt;
}

private void dfs(boolean[][] visited, int threshold, int rows, int cols, int r, int c) {
    if (r < 0 || r >= rows || c < 0 || c >= cols) return;
    if (visited[r][c]) return;
    visited[r][c] = true;
    if (this.digitSum[r][c] > threshold) return;
    this.cnt++;
    for (int i = 0; i < this.next.length; i++) {
        dfs(visited, threshold, rows, cols, r + next[i][0], c + next[i][1]);
    }
}

private void initDigitSum(int rows, int cols) {
    int[] digitSumOne = new int[Math.max(rows, cols)];
    for (int i = 0; i < digitSumOne.length; i++) {
        int n = i;
        while (n > 0) {
            digitSumOne[i] += n % 10;
            n /= 10;
        }
    }
    this.digitSum = new int[rows][cols];
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            this.digitSum[i][j] = digitSumOne[i] + digitSumOne[j];
        }
    }
}
```

## 14. ������

**��Ŀ����**

��һ�����Ӽ��ɶ�Σ�����ʹ��ÿ�εĳ��ȳ˻����

**����˼·**

�����ܶ�ü�����Ϊ 3 �����ӣ����Ҳ������г���Ϊ 1 �����ӳ��֣���������ˣ��ʹ��Ѿ��кó���Ϊ 3 ���������ó�һ���볤��Ϊ 1 ������������ϣ��������г����γ���Ϊ 2 �����ӡ�

```java
int maxProductAfterCuttin(int length) {
    if (length < 2) return 0;
    if (length == 2) return 1;
    if (length == 3) return 2;
    int timesOf3 = length / 3;
    if (length - timesOf3 * 3 == 1) timesOf3--;
    int timesOf2 = (length - timesOf3 * 3) / 2;
    return (int) (Math.pow(3, timesOf3)) * (int) (Math.pow(2, timesOf2));
}
```

## 15. �������� 1 �ĸ���

```java
public int NumberOf1(int n) {
    return Integer.bitCount(n);
}
```

n&(n-1) ��λ������ȥ�� n ��λ����ʾ����͵���һλ��������ڶ����Ʊ�ʾ 10110100����ȥ 1 �õ� 10110011��������������õ� 10110000��

```java
public int NumberOf1(int n) {
    int cnt = 0;
    while (n != 0) {
        cnt++;
        n &= (n - 1);
    }
    return cnt;
}

```

# ������ �������Ĵ���

## 16. ��ֵ�������η�

```java
public double Power(double base, int exponent) {
    if (exponent == 0) return 1;
    if (exponent == 1) return base;
    boolean isNegative = false;
    if (exponent < 0) {
        exponent = -exponent;
        isNegative = true;
    }
    double pow = Power(base * base, exponent / 2);
    if (exponent % 2 != 0) pow = pow * base;
    return isNegative ? 1 / pow : pow;
}
```

## 18. ɾ���������ظ��Ľ��

```java
public ListNode deleteDuplication(ListNode pHead) {
    if (pHead == null) return null;
    if (pHead.next == null) return pHead;
    if (pHead.val == pHead.next.val) {
        ListNode next = pHead.next;
        while (next != null && pHead.val == next.val) {
            next = next.next;
        }
        return deleteDuplication(next);
    } else {
        pHead.next = deleteDuplication(pHead.next);
        return pHead;
    }
}
```

## 19. ������ʽƥ��

**��Ŀ����**

��ʵ��һ����������ƥ����� '.' �� '\*' ��������ʽ��ģʽ�е��ַ� '.' ��ʾ����һ���ַ����� '\*' ��ʾ��ǰ����ַ����Գ�������Σ����� 0 �Σ��� �ڱ����У�ƥ����ָ�ַ����������ַ�ƥ������ģʽ�����磬�ַ��� "aaa" ��ģʽ "a.a" �� "ab\*ac\*a" ƥ�䣬������ "aa.a" �� "ab\*a" ����ƥ��

```java
public boolean match(char[] str, char[] pattern) {
    int n = str.length, m = pattern.length;
    boolean[][] dp = new boolean[n + 1][m + 1];
    dp[0][0] = true;
    for (int i = 1; i <= m; i++) {
        if (pattern[i - 1] == '*') dp[0][i] = dp[0][i - 2];
    }
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (str[i - 1] == pattern[j - 1] || pattern[j - 1] == '.') dp[i][j] = dp[i - 1][j - 1];
            else if (pattern[j - 1] == '*') {
                if (pattern[j - 2] != str[i - 1] && pattern[j - 2] != '.') dp[i][j] = dp[i][j - 2];
                else dp[i][j] = dp[i][j - 1] || dp[i][j - 2] || dp[i - 1][j];
            }
        }
    }
    return dp[n][m];
}
```

## 20. ��ʾ��ֵ���ַ���

**��Ŀ����**

��ʵ��һ�����������ж��ַ����Ƿ��ʾ��ֵ������������С���������磬�ַ��� "+100","5e2","-123","3.1416" �� "-1E-16" ����ʾ��ֵ�� ���� "12e","1a3.14","1.2.3","+-5" �� "12e+4.3" �����ǡ�

```java
public boolean isNumeric(char[] str) {
    String string = String.valueOf(str);
    return string.matches("[\\+-]?[0-9]*(\\.[0-9]*)?([eE][\\+-]?[0-9]+)?");
}
```

## 21. ��������˳��ʹ����λ��ż��ǰ��

ʱ�临�Ӷ� : O(n<sup>2</sup>)
�ռ临�Ӷ� : O(1)

```java
public void reOrderArray(int[] array) {
    int n = array.length;
    for (int i = 0; i < n; i++) {
        if (array[i] % 2 == 0) {
            int nextOddIdx = i + 1;
            while (nextOddIdx < n && array[nextOddIdx] % 2 == 0) nextOddIdx++;
            if (nextOddIdx == n) break;
            int nextOddVal = array[nextOddIdx];
            for (int j = nextOddIdx; j > i; j--) {
                array[j] = array[j - 1];
            }
            array[i] = nextOddVal;
        }
    }
}
```

ʱ�临�Ӷ� : O(n)
�ռ临�Ӷ� : O(n)

```java
public void reOrderArray(int[] array) {
    int oddCnt = 0;
    for (int num : array) if (num % 2 == 1) oddCnt++;
    int[] copy = array.clone();
    int i = 0, j = oddCnt;
    for (int num : copy) {
        if (num % 2 == 1) array[i++] = num;
        else array[j++] = num;
    }
}
```

## 22. �����е����� k �����

```java
public ListNode FindKthToTail(ListNode head, int k) {
    if (head == null) return null;
    ListNode fast, slow;
    fast = slow = head
    while (fast != null && k-- > 0) fast = fast.next;
    if (k > 0) return null;
    while (fast != null) {
        fast = fast.next;
        slow = slow.next;
    }
    return slow;
}
```



## 23. �����л�����ڽ��

```java
public ListNode EntryNodeOfLoop(ListNode pHead) {
    if (pHead == null) return null;
    ListNode slow = pHead, fast = pHead;
    while (fast != null && fast.next != null) {
        fast = fast.next.next;
        slow = slow.next;
        if (slow == fast) {
            fast = pHead;
            while (slow != fast) {
                slow = slow.next;
                fast = fast.next;
            }
            return slow;
        }
    }
    return null;
}
```

## 24. ��ת����

```java
public ListNode ReverseList(ListNode head) {
    ListNode newList = new ListNode(-1);
    while (head != null) {
        ListNode next = head.next;
        head.next = newList.next;
        newList.next = head;
        head = next;
    }
    return newList.next;
}
```

## 25. �ϲ��������������

```java
public ListNode Merge(ListNode list1, ListNode list2) {
    ListNode head = new ListNode(-1);
    ListNode cur = head;
    while (list1 != null && list2 != null) {
        if (list1.val < list2.val) {
            cur.next = list1;
            list1 = list1.next;
        } else {
            cur.next = list2;
            list2 = list2.next;
        }
        cur = cur.next;
    }
    if (list1 != null) cur.next = list1;
    if (list2 != null) cur.next = list2;
    return head.next;
}
```

## 26. �����ӽṹ

```java
public boolean HasSubtree(TreeNode root1, TreeNode root2) {
    if (root1 == null || root2 == null) return false;
    return isSubtree(root1, root2) || HasSubtree(root1.left, root2) || HasSubtree(root1.right, root2);
}

private boolean isSubtree(TreeNode root1, TreeNode root2) {
    if (root1 == null && root2 == null) return true;
    if (root1 == null) return false;
    if (root2 == null) return true;
    if (root1.val != root2.val) return false;
    return isSubtree(root1.left, root2.left) && isSubtree(root1.right, root2.right);
}
```

# ������ ����������˼·

## 27. �������ľ���

```java
public void Mirror(TreeNode root) {
    if (root == null) return;
    TreeNode t = root.left;
    root.left = root.right;
    root.right = t;
    Mirror(root.left);
    Mirror(root.right);
}
```

## 28.1 �ԳƵĶ�����

```java
boolean isSymmetrical(TreeNode pRoot) {
    if (pRoot == null) return true;
    return isSymmetrical(pRoot.left, pRoot.right);
}

boolean isSymmetrical(TreeNode t1, TreeNode t2) {
    if (t1 == null && t2 == null) return true;
    if (t1 == null || t2 == null) return false;
    if (t1.val != t2.val) return false;
    return isSymmetrical(t1.left, t2.right) && isSymmetrical(t1.right, t2.left);
}
```

## 28.2 ƽ�������

```java
private boolean isBalanced = true;

public boolean IsBalanced_Solution(TreeNode root) {
    height(root);
    return isBalanced;
}

private int height(TreeNode root) {
    if (root == null) return 0;
    int left = height(root.left);
    int right = height(root.right);
    if (Math.abs(left - right) > 1) isBalanced = false;
    return 1 + Math.max(left, right);
}
```

## 29. ˳ʱ���ӡ����

```java
public ArrayList<Integer> printMatrix(int[][] matrix) {
    ArrayList<Integer> ret = new ArrayList<>();
    int r1 = 0, r2 = matrix.length - 1, c1 = 0, c2 = matrix[0].length - 1;
    while (r1 <= r2 && c1 <= c2) {
        for (int i = c1; i <= c2; i++) ret.add(matrix[r1][i]);
        for (int i = r1 + 1; i <= r2; i++) ret.add(matrix[i][c2]);
        if (r1 != r2) for (int i = c2 - 1; i >= c1; i--) ret.add(matrix[r2][i]);
        if (c1 != c2) for (int i = r2 - 1; i > r1; i--) ret.add(matrix[i][c1]);
        r1++; r2--; c1++; c2--;
    }
    return ret;
}
```

## 30. ���� min ������ջ

```java
private Stack<Integer> stack = new Stack<>();
private Stack<Integer> minStack = new Stack<>();
private int min = Integer.MAX_VALUE;

public void push(int node) {
    stack.push(node);
    if (min > node) min = node;
    minStack.push(min);
}

public void pop() {
    stack.pop();
    minStack.pop();
    min = minStack.peek();
}

public int top() {
    return stack.peek();
}

public int min() {
    return minStack.peek();
}
```

## 31. ջ��ѹ�롢��������

```java
public boolean IsPopOrder(int[] pushA, int[] popA) {
    int n = pushA.length;
    Stack<Integer> stack = new Stack<>();
    for (int i = 0, j = 0; i < n; i++) {
        stack.push(pushA[i]);
        while (j < n && stack.peek() == popA[j]) {
            stack.pop();
            j++;
        }
    }
    return stack.isEmpty();
}
```

## 32.1 �������´�ӡ������

```java
public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<>();
    ArrayList<Integer> ret = new ArrayList<>();
    if (root == null) return ret;
    queue.add(root);
    while (!queue.isEmpty()) {
        int cnt = queue.size();
        for (int i = 0; i < cnt; i++) {
            TreeNode t = queue.poll();
            if (t.left != null) queue.add(t.left);
            if (t.right != null) queue.add(t.right);
            ret.add(t.val);
        }
    }
    return ret;
}
```

## 32.3  �Ѷ�������ӡ�ɶ���

```java
ArrayList<ArrayList<Integer>> Print(TreeNode pRoot) {
    ArrayList<ArrayList<Integer>> ret = new ArrayList<>();
    if (pRoot == null) return ret;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(pRoot);
    while (!queue.isEmpty()) {
        int cnt = queue.size();
        ArrayList<Integer> list = new ArrayList<>();
        for (int i = 0; i < cnt; i++) {
            TreeNode node = queue.poll();
            list.add(node.val);
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        ret.add(list);
    }
    return ret;
}
```

## 32.3 ��֮����˳���ӡ������

```java
public ArrayList<ArrayList<Integer>> Print(TreeNode pRoot) {
    ArrayList<ArrayList<Integer>> ret = new ArrayList<>();
    if (pRoot == null) return ret;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(pRoot);
    boolean reverse = false;
    while (!queue.isEmpty()) {
        int cnt = queue.size();
        ArrayList<Integer> list = new ArrayList<>();
        for (int i = 0; i < cnt; i++) {
            TreeNode node = queue.poll();
            list.add(node.val);
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        if (reverse) {
            Collections.reverse(list);
            reverse = false;
        } else {
            reverse = true;
        }
        ret.add(list);
    }
    return ret;
}
```


## 33. �����������ĺ����������

```java
public boolean VerifySquenceOfBST(int[] sequence) {
    if (sequence.length == 0) return false;
    return verify(sequence, 0, sequence.length - 1);
}

private boolean verify(int[] sequence, int start, int end) {
    if (end - start <= 1) return true;
    int rootVal = sequence[end];
    int cutIdx = start;
    while (cutIdx < end) {
        if (sequence[cutIdx] > rootVal) break;
        cutIdx++;
    }
    for (int i = cutIdx + 1; i < end; i++) {
        if (sequence[i] < rootVal) return false;
    }
    return verify(sequence, start, cutIdx - 1) && verify(sequence, cutIdx, end - 1);
}
```

## 34. �������к�Ϊĳһֵ��·��

```java
private ArrayList<ArrayList<Integer>> ret = new ArrayList<>();

public ArrayList<ArrayList<Integer>> FindPath(TreeNode root, int target) {
    dfs(root, target, 0, new ArrayList<>());
    return ret;
}

private void dfs(TreeNode node, int target, int curSum, ArrayList<Integer> path) {
    if (node == null) return;
    curSum += node.val;
    path.add(node.val);
    if (curSum == target && node.left == null && node.right == null) {
        ret.add(new ArrayList(path));
    } else {
        dfs(node.left, target, curSum, path);
        dfs(node.right, target, curSum, path);
    }
    path.remove(path.size() - 1);
}
```

## 35. ��������ĸ���

**��Ŀ����**

����һ����������ÿ���ڵ����нڵ�ֵ���Լ�����ָ�룬һ��ָ����һ���ڵ㣬��һ������ָ��ָ������һ���ڵ㣩�����ؽ��Ϊ���ƺ�������� head����ע�⣬���������벻Ҫ���ز����еĽڵ����ã�������������ֱ�ӷ��ؿգ�

��һ������ÿ���ڵ�ĺ�����븴�ƵĽڵ㡣

![](https://github.com/CyC2018/InterviewNotes/blob/master/pics/f8b12555-967b-423d-a84e-bc9eff104b8b.jpg)

�ڶ������Ը��ƽڵ�� random ���ӽ��и�ֵ��

![](https://github.com/CyC2018/InterviewNotes/blob/master/pics/7b877a2a-8fd1-40d8-a34c-c445827300b8.jpg)

����������֡�

![](https://github.com/CyC2018/InterviewNotes/blob/master/pics/b2b6253c-c701-4b30-aff4-bc3c713542a7.jpg)


```java
public RandomListNode Clone(RandomListNode pHead) {
    if (pHead == null) return null;
    // �����½ڵ�
    RandomListNode cur = pHead;
    while (cur != null) {
        RandomListNode node = new RandomListNode(cur.label);
        node.next = cur.next;
        cur.next = node;
        cur = node.next;
    }
    // ���� random ����
    cur = pHead;
    while (cur != null) {
        RandomListNode clone = cur.next;
        if (cur.random != null) {
            clone.random = cur.random.next;
        }
        cur = clone.next;
    }
    // ���
    RandomListNode pCloneHead = pHead.next;
    cur = pHead;
    while (cur.next != null) {
        RandomListNode t = cur.next;
        cur.next = t.next;
        cur = t;
    }
    return pCloneHead;
}
```

## 36. ������������˫������

**��Ŀ����**

����һ�ö��������������ö���������ת����һ�������˫������Ҫ���ܴ����κ��µĽ�㣬ֻ�ܵ������н��ָ���ָ��

```java
private TreeNode pre = null;
public TreeNode Convert(TreeNode pRootOfTree) {
    if(pRootOfTree == null) return null;
    inOrder(pRootOfTree);
    while(pRootOfTree.left != null) pRootOfTree = pRootOfTree.left;
    return pRootOfTree;
}

private void inOrder(TreeNode node) {
    if(node == null) return;
    inOrder(node.left);
    node.left = pre;
    if(pre != null) pre.right = node;
    pre = node;
    inOrder(node.right);
}
```

## 37. ���л�������

```java
private String serizeString = "";

String Serialize(TreeNode root) {
    if (root == null) return "#";
    return root.val + " " + Serialize(root.left) + " "
        + Serialize(root.right);
}

TreeNode Deserialize(String str) {
    this.serizeString = str;
    return Deserialize();
}

private TreeNode Deserialize() {
    if (this.serizeString.length() == 0) return null;
    int idx = this.serizeString.indexOf(" ");
    if (idx == -1) return null;
    String sub = this.serizeString.substring(0, idx);
    this.serizeString = this.serizeString.substring(idx + 1);
    if (sub.equals("#")) {
        return null;
    }
    int val = Integer.valueOf(sub);
    TreeNode t = new TreeNode(val);
    t.left = Deserialize();
    t.right = Deserialize();
    return t;
}
```

## 38. �ַ���������

**��Ŀ����**

����һ���ַ��� , ���ֵ����ӡ�����ַ������ַ����������С����������ַ��� abc, ���ӡ�����ַ� a, b, c �������г����������ַ��� abc, acb, bac, bca, cab �� cba��

```java
private ArrayList<String> ret = new ArrayList<>();

public ArrayList<String> Permutation(String str) {
    if (str.length() == 0) return new ArrayList<>();
    char[] chars = str.toCharArray();
    Arrays.sort(chars);
    backtracking(chars, new boolean[chars.length], "");
    return ret;
}

private void backtracking(char[] chars, boolean[] used, String s) {
    if (s.length() == chars.length) {
        ret.add(s);
        return;
    }
    for (int i = 0; i < chars.length; i++) {
        if (used[i]) continue;
        if (i != 0 && chars[i] == chars[i - 1] && !used[i - 1]) continue; // ��֤���ظ�
        used[i] = true;
        backtracking(chars, used, s + chars[i]);
        used[i] = false;
    }
}
```

# ������ �Ż�ʱ��Ϳռ�Ч��

## 39. �����г��ִ�������һ�������

```java
public int MoreThanHalfNum_Solution(int[] array) {
    int cnt = 1, num = array[0];
    for (int i = 1; i < array.length; i++) {
        if (array[i] == num) cnt++;
        else cnt--;
        if (cnt == 0) {
            num = array[i];
            cnt = 1;
        }
    }
    cnt = 0;
    for (int i = 0; i < array.length; i++) {
        if (num == array[i]) cnt++;
    }
    return cnt > array.length / 2 ? num : 0;
}
```


## 40. ��С�� K ����

������СΪ k ��С���ѡ�

ʱ�临�Ӷȣ�O(nlgk)
�ռ临�Ӷȣ�O(k)

```java
public ArrayList<Integer> GetLeastNumbers_Solution(int[] input, int k) {
    if (k > input.length || k <= 0) return new ArrayList<>();
    PriorityQueue<Integer> pq = new PriorityQueue<>((o1, o2) -> o2 - o1);
    for (int num : input) {
        pq.add(num);
        if (pq.size() > k) {
            pq.poll();
        }
    }
    ArrayList<Integer> ret = new ArrayList<>(pq);
    return ret;
}
```

���ÿ���ѡ��

ʱ�临�Ӷȣ�O(n)
�ռ临�Ӷȣ�O(1)

```java
public ArrayList<Integer> GetLeastNumbers_Solution(int[] input, int k) {
    if (k > input.length || k <= 0) return new ArrayList<>();
    int kthSmallest = findKthSmallest(input, k - 1);
    ArrayList<Integer> ret = new ArrayList<>();
    for (int num : input) {
        if(num <= kthSmallest && ret.size() < k) ret.add(num);
    }
    return ret;
}

public int findKthSmallest(int[] nums, int k) {
    int lo = 0;
    int hi = nums.length - 1;
    while (lo < hi) {
        int j = partition(nums, lo, hi);
        if (j < k) {
            lo = j + 1;
        } else if (j > k) {
            hi = j - 1;
        } else {
            break;
        }
    }
    return nums[k];
}

private int partition(int[] a, int lo, int hi) {
    int i = lo;
    int j = hi + 1;
    while (true) {
        while (i < hi && less(a[++i], a[lo])) ;
        while (j > lo && less(a[lo], a[--j])) ;
        if (i >= j) {
            break;
        }
        exch(a, i, j);
    }
    exch(a, lo, j);
    return j;
}

private void exch(int[] a, int i, int j) {
    final int tmp = a[i];
    a[i] = a[j];
    a[j] = tmp;
}

private boolean less(int v, int w) {
    return v < w;
}
```

## 41.1 �������е���λ��


**��Ŀ����**

��εõ�һ���������е���λ����������������ж�����������ֵ����ô��λ������������ֵ����֮��λ���м����ֵ��������������ж���ż������ֵ����ô��λ������������ֵ����֮���м���������ƽ��ֵ��

```java
private PriorityQueue<Integer> maxHeap = new PriorityQueue<>((o1, o2) -> o2-o1); // ʵ����߲���
private PriorityQueue<Integer> minHeep = new PriorityQueue<>(); // ʵ���ұ߲��֣��ұ߲�������Ԫ�ش�����߲���
private int cnt = 0;

public void Insert(Integer num) {
    // ����Ҫ��֤�����Ѵ���ƽ��״̬
    if(cnt % 2 == 0) { 
        // Ϊż��������²��뵽��С�ѣ��Ⱦ�������ɸѡ���������ܱ�֤�����е�Ԫ�ض�С����С���е�Ԫ��
        maxHeap.add(num);
        minHeep.add(maxHeap.poll());
    } else {
        minHeep.add(num);
        maxHeap.add(minHeep.poll());
    }
    cnt++;
}

public Double GetMedian() {
    if(cnt % 2 == 0) {
        return (maxHeap.peek() + minHeep.peek()) / 2.0;
    } else {
        return (double) minHeep.peek();
    }
}
```

## 14.2 �ַ����е�һ�����ظ����ַ�

**��Ŀ����**

��ʵ��һ�����������ҳ��ַ����е�һ��ֻ����һ�ε��ַ������磬�����ַ�����ֻ����ǰ�����ַ� "go" ʱ����һ��ֻ����һ�ε��ַ��� "g"�����Ӹ��ַ����ж���ǰ�����ַ���google" ʱ����һ��ֻ����һ�ε��ַ��� "l"��

```java
//Insert one char from stringstream
private int[] cnts = new int[256];
private Queue<Character> queue = new LinkedList<>();

public void Insert(char ch) {
    cnts[ch]++;
    queue.add(ch);
    while (!queue.isEmpty() && cnts[queue.peek()] > 1) {
        queue.poll();
    }
}

//return the first appearence once char in current stringstream
public char FirstAppearingOnce() {
    if (queue.isEmpty()) return '#';
    return queue.peek();
}
```


## 42. ���������������

```java
public int FindGreatestSumOfSubArray(int[] array) {
    if(array.length == 0) return 0;
    int ret = Integer.MIN_VALUE;
    int sum = 0;
    for(int num : array) {
        if(sum <= 0) sum = num;
        else sum += num;
        ret = Math.max(ret, sum);
    }
    return ret;
}
```

## 43. �� 1 �� n ������ 1 ���ֵĴ���

����ο���[Leetcode : 233. Number of Digit One](https://leetcode.com/problems/number-of-digit-one/discuss/64381/4+-lines-O(log-n)-C++JavaPython)

```java
public int NumberOf1Between1AndN_Solution(int n) {
    int cnt = 0;
    for (int m = 1; m <= n; m *= 10) {
        int a = n / m, b = n % m;
        cnt += (a + 8) / 10 * m + (a % 10 == 1 ? b + 1 : 0);
    }
    return cnt;
}
```

## 45. �������ų���С����

**��Ŀ����**

����һ�����������飬����������������ƴ�������ų�һ��������ӡ��ƴ�ӳ���������������С��һ���������������� {3��32��321}�����ӡ���������������ųɵ���С����Ϊ 321323��

```java
public String PrintMinNumber(int[] numbers) {
    int n = numbers.length;
    String[] nums = new String[n];
    for (int i = 0; i < n; i++) nums[i] = numbers[i] + "";
    Arrays.sort(nums, (s1, s2) -> (s1 + s2).compareTo(s2 + s1));
    String ret = "";
    for (String str : nums) ret += str;
    return ret;
}
```

## 49. ����

**��Ŀ����**

��ֻ�������� 2��3 �� 5 ��������������Ugly Number�������� 6��8 ���ǳ������� 14 ���ǣ���Ϊ���������� 7�� ϰ�������ǰ� 1 �����ǵ�һ���������󰴴�С�����˳��ĵ� N ��������

```java
public int GetUglyNumber_Solution(int index) {
    if (index <= 6) return index;
    int i2 = 0, i3 = 0, i5 = 0;
    int cnt = 1;
    int[] dp = new int[index];
    dp[0] = 1;
    while (cnt < index) {
        int n2 = dp[i2] * 2, n3 = dp[i3] * 3, n5 = dp[i5] * 5;
        int tmp = Math.min(n2, Math.min(n3, n5));
        dp[cnt++] = tmp;
        if (tmp == n2) i2++;
        if (tmp == n3) i3++;
        if (tmp == n5) i5++;
    }
    return dp[index - 1];
}
```

## 50. ��һ��ֻ����һ�ε��ַ�λ��

```java
public int FirstNotRepeatingChar(String str) {
    int[] cnts = new int[256];
    for (int i = 0; i < str.length(); i++) cnts[str.charAt(i)]++;
    for (int i = 0; i < str.length(); i++) if (cnts[str.charAt(i)] == 1) return i;
    return -1;
}
```

## 51. �����е������

```java
private long cnt = 0;

public int InversePairs(int[] array) {
    mergeSortUp2Down(array, 0, array.length - 1);
    return (int) (cnt % 1000000007);
}

private void mergeSortUp2Down(int[] a, int start, int end) {
    if (end - start < 1) return;
    int mid = start + (end - start) / 2;
    mergeSortUp2Down(a, start, mid);
    mergeSortUp2Down(a, mid + 1, end);
    merge(a, start, mid, end);
}

private void merge(int[] a, int start, int mid, int end) {
    int[] tmp = new int[end - start + 1];
    int i = start, j = mid + 1, k = 0;
    while (i <= mid || j <= end) {
        if (i > mid) tmp[k] = a[j++];
        else if (j > end) tmp[k] = a[i++];
        else if (a[i] < a[j]) tmp[k] = a[i++];
        else {
            tmp[k] = a[j++];
            this.cnt += mid - i + 1; // a[i] > a[j] ��˵�� a[i...mid] ������ a[j]
        }
        k++;
    }

    for (k = 0; k < tmp.length; k++) {
        a[start + k] = tmp[k];
    }
}
```

## 52. ��������ĵ�һ���������

```java
public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {
    ListNode l1 = pHead1, l2 = pHead2;
    while (l1 != l2) {
        if (l1 == null) l1 = pHead2;
        else l1 = l1.next;
        if (l2 == null) l2 = pHead1;
        else l2 = l2.next;
    }
    return l1;
}
```

# ������ �����еĸ�������

## 53 ���������������г��ֵĴ���



```java
public int GetNumberOfK(int[] array, int k) {
    int l = 0, h = array.length - 1;
    while (l <= h) {
        int m = l + (h - l) / 2;
        if (array[m] >= k) h = m - 1;
        else l = m + 1;
    }
    int cnt = 0;
    while (l < array.length && array[l++] == k) cnt++;
    return cnt;
}
```

## 54. �����������ĵ� k �����

```java
TreeNode ret;
int cnt = 0;

TreeNode KthNode(TreeNode pRoot, int k) {
    inorder(pRoot, k);
    return ret;
}

private void inorder(TreeNode root, int k) {
    if (root == null) return;
    if (cnt > k) return;
    inorder(root.left, k);
    cnt++;
    if (cnt == k) ret = root;
    inorder(root.right, k);
}
```

## 55 �����������

```java
public int TreeDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(TreeDepth(root.left), TreeDepth(root.right));
}
```

## 56. ������ֻ����һ�ε�����

��������ȵ�Ԫ����λ����ʾ�ϱض�����һλ���ڲ�ͬ��

�����������Ԫ�����õ��Ľ��Ϊ�������ظ�������Ԫ�����Ľ����

diff &= -diff �õ��� diff ���Ҳ಻Ϊ 0 ��λ��Ҳ���ǲ������ظ�������Ԫ����λ����ʾ�����Ҳ಻ͬ����һλ��������һλ�Ϳ��Խ�����Ԫ�����ֿ�����

```java
public void FindNumsAppearOnce(int[] array, int num1[], int num2[]) {
    int diff = 0;
    for (int num : array) diff ^= num;
    // �õ�����һλ
    diff &= -diff;
    for (int num : array) {
        if ((num & diff) == 0) num1[0] ^= num;
        else num2[0] ^= num;
    }
}
```

## 57.1 ��Ϊ S ����������

```java
public ArrayList<Integer> FindNumbersWithSum(int[] array, int sum) {
    int i = 0, j = array.length - 1;
    while (i < j) {
        int cur = array[i] + array[j];
        if (cur == sum) return new ArrayList<Integer>(Arrays.asList(array[i], array[j]));
        else if (cur < sum) i++;
        else j--;
    }
    return new ArrayList<Integer>();
}
```

## 57.2 ��Ϊ S ��������������

```java
public ArrayList<ArrayList<Integer>> FindContinuousSequence(int sum) {
    ArrayList<ArrayList<Integer>> ret = new ArrayList<>();
    int start = 1, end = 2;
    int mid = sum / 2;
    int curSum = 3;
    while (start <= mid && end < sum) {
        if (curSum > sum) {
            curSum -= start;
            start++;
        } else if (curSum < sum) {
            end++;
            curSum += end;
        } else {
            ArrayList<Integer> list = new ArrayList<>();
            for (int i = start; i <= end; i++) {
                list.add(i);
            }
            ret.add(list);
            curSum -= start;
            start++;
            end++;
            curSum += end;
        }
    }
    return ret;
}
```

## 58.1 ��ת����˳����

```java
public String ReverseSentence(String str) {
    if (str.length() == 0) return str;
    int n = str.length();
    char[] chars = str.toCharArray();
    int start = 0, end = 0;
    while (end <= n) {
        if (end == n || chars[end] == ' ') {
            reverse(chars, start, end - 1);
            start = end + 1;
        }
        end++;
    }
    reverse(chars, 0, n - 1);
    return new String(chars);
}

private void reverse(char[] c, int start, int end) {
    while (start < end) {
        char t = c[start];
        c[start] = c[end];
        c[end] = t;
        start++;
        end--;
    }
}
```

## 58.2 ����ת�ַ���

```java
public String LeftRotateString(String str, int n) {
    if (str.length() == 0) return "";
    char[] c = str.toCharArray();
    reverse(c, 0, n - 1);
    reverse(c, n, c.length - 1);
    reverse(c, 0, c.length - 1);
    return new String(c);
}

private void reverse(char[] c, int i, int j) {
    while (i < j) {
        char t = c[i];
        c[i] = c[j];
        c[j] = t;
        i++;
        j--;
    }
}
```

## 59. �������ڵ����ֵ

```java
public ArrayList<Integer> maxInWindows(int[] num, int size) {
    ArrayList<Integer> ret = new ArrayList<>();
    PriorityQueue<Integer> heap = new PriorityQueue<Integer>((o1, o2) -> o2 - o1);
    if (size > num.length || size < 1) return ret;
    for (int i = 0; i < size; i++) heap.add(num[i]);
    ret.add(heap.peek());
    for (int i = 1; i + size - 1 < num.length; i++) {
        heap.remove(num[i - 1]);
        heap.add(num[i + size - 1]);
        ret.add(heap.peek());
    }
    return ret;
}
```

## 61. �˿���˳��

```java
public boolean isContinuous(int[] numbers) {
    if (numbers.length < 5) return false;
    Arrays.sort(numbers);
    int cnt = 0;
    for (int num : numbers) if (num == 0) cnt++;
    for (int i = cnt; i < numbers.length - 1; i++) {
        if (numbers[i + 1] == numbers[i]) return false;
        int cut = numbers[i + 1] - numbers[i] - 1;
        if (cut > cnt) return false;
        cnt -= cut;
    }
    return true;
}
```

## 62. ԲȦ�����ʣ�µ���

**��Ŀ����**

��С������Χ��һ����Ȧ��Ȼ�� , �����ָ��һ���� m, �ñ��Ϊ 0 ��С���ѿ�ʼ������ÿ�κ��� m-1 ���Ǹ�С����Ҫ���г��׸� , Ȼ���������Ʒ�����������ѡ���� , ���Ҳ��ٻص�Ȧ�� , ��������һ��С���ѿ�ʼ , ���� 0...m-1 ���� .... ������ȥ .... ֱ��ʣ�����һ��С���� , ���Բ��ñ��� ,

**����˼·**

Լɪ��

```java
public int LastRemaining_Solution(int n, int m) {
    if (n == 0) return -1;
    if (n == 1) return 0;
    return (LastRemaining_Solution(n - 1, m) + m) % n;
}
```

# 63. ��Ʊ���������

```java
public int maxProfit(int[] prices) {
    int n = prices.length;
    if(n == 0) return 0;
    int soFarMin = prices[0];
    int max = 0;
    for(int i = 1; i < n; i++) {
        if(soFarMin > prices[i]) soFarMin = prices[i];
        else max = Math.max(max, prices[i] - soFarMin);
    }
    return max;
}
```

## 64. �� 1+2+3+...+n

```java
public int Sum_Solution(int n) {
    if(n == 0) return 0;
    return n + Sum_Solution(n - 1);
}
```

## 65. ���üӼ��˳����ӷ�

a ^ b ��ʾû�п��ǽ�λ������������ĺͣ�(a & b) << 1 ���ǽ�λ���ݹ����ֹ��ԭ���� (a & b) << 1 ���ұ߻��һ�� 0����ô�����ݹ飬��λ���ұߵ� 0 ���������࣬����λ���Ϊ 0���ݹ���ֹ��

```java
public int Add(int num1, int num2) {
    if(num2 == 0) return num1;
    return Add(num1 ^ num2, (num1 & num2) << 1);
}
```

## 66. �����˻�����

```java
public int[] multiply(int[] A) {
    int n = A.length;
    int[][] dp = new int[n][n];
    for (int i = 0; i < n; i++) {
        dp[i][i] = A[i];
    }
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            dp[i][j] = dp[i][j - 1] * A[j];
        }
    }

    int[] B = new int[n];
    Arrays.fill(B, 1);
    for (int i = 0; i < n; i++) {
        if (i != 0) B[i] *= dp[0][i - 1];
        if (i != n - 1) B[i] *= dp[i + 1][n - 1];
    }
    return B;
}
```

# ������ �������԰���

## 67. ���ַ���ת��������

```java
public int StrToInt(String str) {
    if (str.length() == 0) return 0;
    char[] chars = str.toCharArray();
    boolean isNegative = chars[0] == '-';
    int ret = 0;
    for (int i = 0; i < chars.length; i++) {
        if (i == 0 && (chars[i] == '+' || chars[i] == '-')) continue;
        if (chars[i] < '0' || chars[i] > '9') return 0;
        ret = ret * 10 + (chars[i] - '0');
    }
    return isNegative ? -ret : ret;
}
```

## 68. ���������ڵ����͹�������

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if(root.val > p.val && root.val > q.val) return lowestCommonAncestor(root.left, p, q);
    if(root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right, p, q);
    return root;
}
```
