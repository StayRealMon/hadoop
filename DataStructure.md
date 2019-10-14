
<!-- MarkdownTOC -->

- [排序](#%E6%8E%92%E5%BA%8F)
    - [快速排序](#%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F)
    - [直接插入排序](#%E7%9B%B4%E6%8E%A5%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F)
    - [选择插入排序](#%E9%80%89%E6%8B%A9%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F)
    - [堆排序](#%E5%A0%86%E6%8E%92%E5%BA%8F)
    - [比较次数和初始序列](#%E6%AF%94%E8%BE%83%E6%AC%A1%E6%95%B0%E5%92%8C%E5%88%9D%E5%A7%8B%E5%BA%8F%E5%88%97)
    - [确定最终位置](#%E7%A1%AE%E5%AE%9A%E6%9C%80%E7%BB%88%E4%BD%8D%E7%BD%AE)
- [基础题吧](#%E5%9F%BA%E7%A1%80%E9%A2%98%E5%90%A7)
    - [整数区间合并](#%E6%95%B4%E6%95%B0%E5%8C%BA%E9%97%B4%E5%90%88%E5%B9%B6)
    - [众数](#%E4%BC%97%E6%95%B0)
    - [链表](#%E9%93%BE%E8%A1%A8)
        - [头插法](#%E5%A4%B4%E6%8F%92%E6%B3%95)
        - [原地逆置](#%E5%8E%9F%E5%9C%B0%E9%80%86%E7%BD%AE)
        - [判断环](#%E5%88%A4%E6%96%AD%E7%8E%AF)
- [动态规划](#%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)
    - [二维数组最短路径](#%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%E6%9C%80%E7%9F%AD%E8%B7%AF%E5%BE%84)
    - [类二叉树的最短路径](#%E7%B1%BB%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E7%9F%AD%E8%B7%AF%E5%BE%84)
    - [抢银行](#%E6%8A%A2%E9%93%B6%E8%A1%8C)
    - [最长公共子串 Longest Common Substring](#%E6%9C%80%E9%95%BF%E5%85%AC%E5%85%B1%E5%AD%90%E4%B8%B2-longest-common-substring)
    - [最长公共子序列 Longest Common Sequence](#%E6%9C%80%E9%95%BF%E5%85%AC%E5%85%B1%E5%AD%90%E5%BA%8F%E5%88%97-longest-common-sequence)
    - [0/1背包](#01%E8%83%8C%E5%8C%85)
    - [两端取数](#%E4%B8%A4%E7%AB%AF%E5%8F%96%E6%95%B0)
    - [最大连续子序列和](#%E6%9C%80%E5%A4%A7%E8%BF%9E%E7%BB%AD%E5%AD%90%E5%BA%8F%E5%88%97%E5%92%8C)
    - [无限硬币找零组合数](#%E6%97%A0%E9%99%90%E7%A1%AC%E5%B8%81%E6%89%BE%E9%9B%B6%E7%BB%84%E5%90%88%E6%95%B0)
- [二叉树](#%E4%BA%8C%E5%8F%89%E6%A0%91)
    - [广度优先遍历BFS-Queue | 用于计算深度高度](#%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E9%81%8D%E5%8E%86bfs-queue-%7C-%E7%94%A8%E4%BA%8E%E8%AE%A1%E7%AE%97%E6%B7%B1%E5%BA%A6%E9%AB%98%E5%BA%A6)
    - [深度优先遍历DFS-Stack | 用于前中后序遍历](#%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E9%81%8D%E5%8E%86dfs-stack-%7C-%E7%94%A8%E4%BA%8E%E5%89%8D%E4%B8%AD%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86)
    - [Dijkstra 算法](#dijkstra-%E7%AE%97%E6%B3%95)
    - [朋友圈 lt547](#%E6%9C%8B%E5%8F%8B%E5%9C%88-lt547)
    - [分糖果](#%E5%88%86%E7%B3%96%E6%9E%9C)
        - [Rating高的多于Rating低的](#rating%E9%AB%98%E7%9A%84%E5%A4%9A%E4%BA%8Erating%E4%BD%8E%E7%9A%84)

<!-- /MarkdownTOC -->


<a id="%E6%8E%92%E5%BA%8F"></a>
# 排序 #
![](https://images2017.cnblogs.com/blog/1303641/201801/1303641-20180124091639006-2029462359.png)



<a id="%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F"></a>
## 快速排序 ##

找出序列的一个关键字作为枢纽，大于枢纽的元素放到枢纽之后，小于枢纽的元素放到枢纽之前，这样一趟排序将源数列分成两个子序列。然后对这两个子序列递归进行快速排序，直到每个子序列都包含一个元素为止
```java
quickSort(list[],low,high):
    int low,high,list[];
    int start = low,end = high;
    //关键字key
    int key = list[start];
    //循环结束的时候start == end，key到达了最终位置
    while(start<end):
        while(list[end]>=key)
            end--;
        //跳出子循环意味着后面有比key小的数，此时交换end和start
        list[start] <==> list[end];
        while(list[start]<=key)
            start++;
        //跳出子循环意味着前面有比key大的数，此时交换start和end
        list[end] <==> list[start];
    //一轮循环结束。左边的数都比key小，右边的数都比key大。
    //递归调用quickSort()
    quickSort(list[],low,start-1);
    quickSort(list[],end+1,high);
```

<a id="%E7%9B%B4%E6%8E%A5%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F"></a>
## 直接插入排序 ##
第一轮比较前两个数，第二轮拿第三个与前两个相比，以此类推，每一轮将第N+1个数和前面N个有序的数比较，比较之后前N+1个数有序

<a id="%E9%80%89%E6%8B%A9%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F"></a>
## 选择插入排序 ##
第一轮挑选N个数中最小的数放第一，第二轮从剩余N-1个数中找到最小的放到第二位，以此类推每次把剩余数中最小的放到前面有序队列的最后

<a id="%E5%A0%86%E6%8E%92%E5%BA%8F"></a>
## 堆排序 ##
1. 数组存储，先建完全二叉树
2. **初始化**过程：从n/2向下取整位置(即第一个非叶子结点的根节点处)开始调整堆，调整直到第一个根节点，此时完成堆的初始化
3. 大顶堆小顶堆初始化完成之后，根节点出堆，最后一个叶子结点放到根的位置，继续递归调整
4. 直到完全二叉树中的所有节点都输出，排序完成，**大顶堆升序排列，小顶堆降序排列**

<a id="%E6%AF%94%E8%BE%83%E6%AC%A1%E6%95%B0%E5%92%8C%E5%88%9D%E5%A7%8B%E5%BA%8F%E5%88%97"></a>
##比较次数和初始序列##
1. 插排 时间复杂度与比较次数，移动次数都与初始序列有关
2. 快排 时间复杂度与比较次数，与移动次数都与初始序列有关
3. 归排 时间复杂度与初始序列无关，比较次数有关（有序序列），移动次数无关（无论怎么有序，还是每个元素拷贝到新的数组）
4. 选排 时间复杂度与初始序列无关，比较次数无关，移动次数无关
5. 冒排 时间复杂度与初始序列无关，比较次数无关，移动次数有关

> 一堆（堆排序）乌龟（归并排序）选（选择排序）基（基数排序——算法复杂度与数组的初始状态无关

<a id="%E7%A1%AE%E5%AE%9A%E6%9C%80%E7%BB%88%E4%BD%8D%E7%BD%AE"></a>
## 确定最终位置 ##
1. 简单选择排序每次选择未排序列中的最小元素放入其最终位置
2. 希尔排序每次是对划分的子表进行排序，得到局部有序的结果，所以不能保证每一趟排序结束都能确定一个元素的最终位置
3. 快速排序每一趟排序结束后都将枢轴元素放到最终位置
4. 堆排序属于选择排序，每次都将大根堆的根结点与表尾结点交换，确定其最终位置
5. 二路归并排序每趟对子表进行两两归并从而得到若干个局部有序的结果，但无法确定最终位置

<a id="%E5%9F%BA%E7%A1%80%E9%A2%98%E5%90%A7"></a>
# 基础题吧 #
<a id="%E6%95%B4%E6%95%B0%E5%8C%BA%E9%97%B4%E5%90%88%E5%B9%B6"></a>
## 整数区间合并 ##
```java
import java.util.*;
public class MainSolution {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        //接收输入的区间集合如: 1,3/n2,4/n5,8/n10,15
        int nums = Integer.parseInt(sc.nextLine());
        String tmpInput = "";
        int[] startList = new int[nums];
        int[] endList = new int[nums];
        for (int i=0;i<nums;i++){
            tmpInput = sc.nextLine();
            startList[i] = Integer.parseInt(tmpInput.split(",")[0]);
            endList[i] = Integer.parseInt(tmpInput.split(",")[1]);
        }//将start和end分别排好序，便于合并
        Arrays.sort(startList);
        Arrays.sort(endList);
        mergeInterval(startList,endList);
    }
    public static void mergeInterval(int[] start, int[] end){
        int len = start.length;
        //Map用于存储最终的区间起始值，没有new一个区间的class Interval，临时用HashMap存储
        Map<Integer, Integer> resMap = new HashMap<>();
        for (int i=0,j=0;i<start.length;i++){
            //不合并的条件是下一个开始要大于前一个的结束如:1,2/n3,4 => 合并为1,2
            //当i==len-1的时候意味着走到了最后一个区间，直接将上一个start[j]作为开始，end[i]作为区间结尾添加即可
            if (i == len-1||start[i+1]>end[i]){
                resMap.put(start[j], end[i]);
                //3,4作为下一个区间的开始继续
                j= i+1;
            }
        }Set<Map.Entry<Integer, Integer>> entSet = resMap.entrySet();
        for (Map.Entry<Integer, Integer> tmpEnt : entSet)
            System.out.println(tmpEnt.getKey()+","+tmpEnt.getValue());
    }
}

```
<a id="%E4%BC%97%E6%95%B0"></a>
## 众数 ##
这里众数特制出现次数大于len/2向下取整，或者大于等于len/2向上取整
```java
import java.util.*;
public class MainSolution {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String tmpInput = sc.nextLine();
        int len = tmpInput.split(" ").length;
        int[] inputList = new int[len];
        for (int i=0;i<len;i++)
            inputList[i] = Integer.parseInt(tmpInput.split(" ")[i]);
        Arrays.sort(inputList);
        System.out.println(inputList[(int)Math.floor(len/2.0)]);
    }
}

```

<a id="%E9%93%BE%E8%A1%A8"></a>
## 链表 ##
<a id="%E5%A4%B4%E6%8F%92%E6%B3%95"></a>
### 头插法 ###
```java
while(oldList.hasNext()):
    //赋值给一个新节点
    Node newNode = oldHead.next;
    //新链表接到新节点之后
    newNode.next = newHead.next;
    //新节点接在新头节点之后
    newHead.next = newNode;
    //原链表向后遍历
    oldHead = oldHead.next;

```

<a id="%E5%8E%9F%E5%9C%B0%E9%80%86%E7%BD%AE"></a>
### 原地逆置 ###
1. 节点防断裂;
2. head为空或者仅有head
3. pre，head，next三个指针
4. 用栈也可以，一次for循环入栈，while not null再循环出栈即可，栈需要`import java.util.Stack;`，然后`Stack<Integer> stk = new Stack<>();`

```java
    while(head!=null):
        //记录原顺序的next
        next = head.next; 
        //切断原连接，将head的下一个节点由next指向pre
        head.next = pre;
        //pre, head, next依次往后移一位
        pre = head; head = next;
```

<a id="%E5%88%A4%E6%96%AD%E7%8E%AF"></a>
### 判断环 ###
1. 穷举/HashSet缓存节点唯一id信息
2. 快慢指针，环没有终点：快2先进环追慢1，相遇即有环
3. 求环的入口？求出2中的相遇交点，分别从head和交点node遍历，相遇的时候就是环的入口(也可仅仅考虑环中的追击相遇问题，入口为x，交点为n，slowNode走i步则fastNode走了2i步，相差的步数2i-i = k圈*N圈的大小=i)
4. 若判断两个单链表是否相交，相交肯定有唯一尾节点，连接其中一个链表的首尾即转化为环的问题

```java
	while(fastNode!=null):
		if(fastNode.next!=null)
			fastNode = fastNode.next.next;
		slowNode = slowNode.next;
		if(slowNode == fastnode)
			return TRUE;
			//找入口
			fastNode = slowNode；
			while(fastNode != slowNode):
				fastNode = fastNode.next.next;
				slowNode = slowNode.next;
			return fastNode;
```

<a id="%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92"></a>
# 动态规划 #
最优子问题/动态转移方程/边界->进阶背包问题

青蛙跳台阶/拿硬币等问题啊，数值可能过大，数组可以用`Long[]`代替`int[]`

<a id="%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%E6%9C%80%E7%9F%AD%E8%B7%AF%E5%BE%84"></a>
## 二维数组最短路径 ##
```java
    import java.util.Scanner;
    public class MainSolution {
        public static void main(String[] args){
            Scanner sc = new Scanner(System.in);
            String input = sc.nextLine();
            //M*N的Metric
            int M = Integer.parseInt(input.split(" ")[0]);
            int N = Integer.parseInt(input.split(" ")[1]);
            int[][] metric = new int[M][N];
            int lineFlag = 0;
            while(lineFlag < M){
                input = sc.nextLine();
                for (int j = 0;j<N;j++){
                    metric[lineFlag][j] = Integer.parseInt(input.split(" ")[j]);
                }lineFlag++;
            }int[][] grids = new int[M][N];
            grids[0][0] = metric[0][0];
            //初始化边界
            for (int i = 1;i<M;i++)
                grids[i][0] = metric[i][0]+grids[i-1][0];
            for (int j = 1;j<N;j++)
                grids[0][j] = metric[0][j]+grids[0][j-1];
            //动态转移方程
            for (int i=1;i<M;i++)
                for (int j=1;j<N;j++){
                    grids[i][j] = Math.min(grids[i-1][j],grids[i][j-1])+metric[i][j];
                }
            for (int i =0;i<M;i++)
                for (int j=0;j<N;j++)
                    System.out.println(grids[i][j]);
        }
    }
```
<a id="%E7%B1%BB%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E7%9F%AD%E8%B7%AF%E5%BE%84"></a>
## 类二叉树的最短路径 ##
```java
import java.util.Scanner;
public class MainSolution {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();
        int linesCnt = Integer.parseInt(input);
        int[][] metric = new int[linesCnt][linesCnt];
        int lineFlag = 0;
        while(lineFlag < linesCnt){
            input = sc.nextLine();
            for (int j = 0;j<=lineFlag;j++){
                metric[lineFlag][j] = Integer.parseInt(input.split(" ")[j]);
            }lineFlag++;
        }
        int[] lineRes = new int[linesCnt];
        //初始化
        for (int i =0;i<linesCnt;i++)
            lineRes[i] = metric[linesCnt-1][i];
        //自底向上汇总最小值存到一维数组
        for (int i =linesCnt-1;i>0;i--) {
            for (int j = i-1; j >= 0; j--) {
                lineRes[j] = Math.min(lineRes[j + 1], lineRes[j]) + metric[i - 1][j];
                System.out.print(lineRes[j] + "\t");
            }
            System.out.print("\n");
        }
    }
}
```
<a id="%E6%8A%A2%E9%93%B6%E8%A1%8C"></a>
## 抢银行 ##
环状的银行首尾不可兼得，分为两个list，`有头无尾` 和 `有尾无头`，分别当作参数传入以下的基本方法中，比较结果即可。
```java
import java.util.Scanner;
public class MainSolution {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();
        int len = input.split(" ").length;
        int[] values = new int[len];
        for (int i=0;i<len;i++)
            values[i] = Integer.parseInt(input.split(" ")[i]);
        int[] dp = new int[len];
        dp[0] = values[0];dp[1] = values[1];
        for (int i=2;i<len;i++)
            dp[i] = dp[i-2] + values[i];
        System.out.println(Math.max(dp[len-1],dp[len-2]));
    }
}

```

<a id="%E6%9C%80%E9%95%BF%E5%85%AC%E5%85%B1%E5%AD%90%E4%B8%B2-longest-common-substring"></a>
## 最长公共子串 Longest Common Substring ##
仅有长度，可优化到一维数组，可递归打印
```java
public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String firstWord = sc.nextLine();
        String secondWord = sc.nextLine();
        char[] firstList = firstWord.toCharArray();
        char[] secondList = secondWord.toCharArray();
        int firstLen = firstList.length;
        int secondLen = secondList.length;
        int[][] grid = new int[firstLen][secondLen];
        int[][] dp = new int[firstLen][secondLen];
        for (int i=0;i<firstLen;i++)
            for (int j=0;j<secondLen;j++)
                if (firstList[i] == secondList[j])
                    grid[i][j] = 1;
                else
                    grid[i][j] = 0;
        System.out.println("## doubleArrToString(grid) ##");
        doubleArrToString(grid);
        dp[0] = grid[0];
        for (int i=0;i<firstLen;i++)
            dp[i][0] = grid[i][0];
        for (int i=1;i<firstLen;i++) {
            for (int j = 1; j < secondLen; j++) {
                dp[i][j] = grid[i][j]+dp[i-1][j-1];
            }
        }
        System.out.println("\n## doubleArrToString(dp) ##");
        doubleArrToString(dp);
        int res = 0;
        //最后一行的length即为列数，遍历最后一行
        for (int i=0;i<dp[firstLen-1].length;i++)
            res = Math.max(dp[firstLen-1][i],res);
        //整个dp数组的length即为行数，遍历最后一列
        for (int i=0;i<dp.length;i++)
            res = Math.max(dp[i][secondLen-1],res);
        System.out.println("Max Result is : "+res);
    }

    public static void doubleArrToString(int[][] arr){
        int x = arr.length;
        int y = arr[0].length;
        for (int i=0;i<x;i++) {
            for (int j = 0; j < y; j++) {
                System.out.print(arr[i][j]+"\t");
            }
            System.out.println(" ");
        }
    }
```

**优化办法**:由一位数组`tmp`保存每一行的最大值状态，并用两个一位数组记录出现最大长度的位置`maxIndex`和值`maxSeq`。最后根据`maxSeq`和`maxIndex`的首位不为0的最大长度值和最大长度的位置打印出原字符串的子串
```java
import java.util.Scanner;

public class MainSolution {

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String firstWord = sc.nextLine();
        String secondWord = sc.nextLine();
        getLCS(firstWord, secondWord);
    }

    //获取LCS
    public static void getLCS(String firstWord, String secondWord){
        char[] fList = firstWord.toCharArray();
        char[] sList = secondWord.toCharArray();
        int fSize = fList.length;
        int sSize = sList.length;
        // 记录最长的字符串长度
        int maxSize = Math.max(fSize,sSize);
        //maxSeq代表每一行的最大值，只标记首位为最大，有相同时往后追加，小于忽略大于将首位置为max首位之后的置为0
        int[] maxSeq = new int[maxSize];
        //maxIndex在字符相等时标记maxIndex[0]为maxSeq最大值的位置，只有一个最大值就标记maxIndex[0]，maxSeq有几个最大值，maxIndex就有几个标记位置
        int[] maxIndex = new int[maxSize];
        //tmp数组标记每一行的动态变化，从上往下从右往左，当字符相等时为前一行时候的对角线值+1，不等时记为0
        int[] tmp = new int[maxSize];
        //相同时对角线+1，否则置为0
        for (int i=0;i<fSize;i++){
            for (int j=sSize-1;j>=0;j--){
                //当字符相等的时候进入判断前一个字符是否相等，相等长度累加1或者置为1，不等置为0
                if (fList[i]==sList[j]) {
                    if (i==0||j==0)    //首行首列是tmp[j]记为1
                        tmp[j] = 1;
                    else               //其余为前一行的最长值累加1获得
                        tmp[j] = tmp[j-1]+1;
                }else
                    tmp[j] = 0;

                //存储最大值和最大值的位置两个数组变动
                //如果maxSeq的第一位没有当前行的最大值大，即出现了更长的数组，更新maxSeq和maxIndex两个数组的首位值并充值之后的值为0
                if (tmp[j]>maxSeq[0]){
                    maxSeq[0] = tmp[j];
                    maxIndex[0] = j;
                    for (int q=1;q<maxSize;q++){
                        maxSeq[q] = 0;
                        maxIndex[q] = 0;
                    }
                    //如果maxSeq的首位即最大值和当前行的最大值相等，即出现了相等长度的字符串，此时在两个数组后面追加相等的值和出现这个值的位置
                }else if (tmp[j]==maxSeq[0]){
                    for (int q =0;q<maxSize;q++){
                        if (maxSeq[q]==0){
                            maxSeq[q] = tmp[j];
                            maxIndex[q] = j;
                            break;
                        }
                    }
                }
            }
        }// 若有相同字符串就打印出来多个字符串
        for (int x=0;x<maxSize;x++){
            if (maxSeq[x]>0){
                System.out.println("The "+x+1+" String is :");
                for (int y=maxIndex[x]-maxSeq[x]+1;y<=maxIndex[x];y++)
                    System.out.print(sList[y]);
                System.out.println("");
            }
        }
    }

}

```


<a id="%E6%9C%80%E9%95%BF%E5%85%AC%E5%85%B1%E5%AD%90%E5%BA%8F%E5%88%97-longest-common-sequence"></a>
## 最长公共子序列 Longest Common Sequence
递归打印，长度和子序列均有
```java
import java.util.Scanner;
public class MainSolution {

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String firstWord =  sc.nextLine();
        String secondWord =  sc.nextLine();
        getLCS(firstWord,secondWord);
    }

    public static void getLCS(String firstWord, String secondWord){

        char[] fList = firstWord.toCharArray();
        char[] sList = secondWord.toCharArray();
        int fSize = fList.length;
        int sSize = sList.length;
        int[][] res = new int[fSize+1][sSize+1];
        //初始化
        for (int i=0;i<=fSize;i++)
            res[i][0] = 0;
        for (int i=0;i<=sSize;i++)
            res[0][i] = 0;
        //状态转移。字符相等就对角线方向+1，否则取上一行或者左一行的最大值
        for (int i=1;i<=fSize;i++){
            for (int j=1;j<=sSize;j++){
                if (fList[i-1]==sList[j-1])
                    res[i][j] = res[i-1][j-1]+1;
                else
                    res[i][j] = (res[i-1][j]>=res[i][j-1])?res[i-1][j]:res[i][j-1];
            }
        }
        printLCS(fList,sList,res,fSize,sSize);
        System.out.println("\nMetric is : ");
        for (int i =0 ;i<=fSize;i++) {
            for (int j = 0; j <=sSize; j++) {
                System.out.print(res[i][j]+"\t");
            }System.out.println();
        }
    }

    public static void printLCS(char[] fList, char[] sList,int[][] metric, int i, int j){
        //遍历到i==0或者j==0时有一个字符串已经被遍历完成直接返回
        if (i==0||j==0)
            return ;
        //查看第i个和第j个是否相等，相等递归打印i-1和j-1位置
        if (fList[i-1] == sList[j-1]){
            printLCS(fList, sList, metric, i-1, j-1);
            System.out.print(sList[j-1]);
            //如果和上一行metric值相等，递归比较firstWord的第i-1位置和secondWord的第j位置是否相等
        }else if (metric[i-1][j]==metric[i][j])
            printLCS(fList, sList, metric, i-1, j);
        // 如果和上一行metric不相等，递归比较firstWord的第i位置和secondWord的第j-1位置是否相等
        // 这样下来直到找到左上角第位置使得 i-1 == j-1然后打印
        else
            printLCS(fList, sList, metric, i, j-1);
    }
}
```

<a id="01%E8%83%8C%E5%8C%85"></a>
## 0/1背包 ##
每个物品只能拿一次，背包不一定放满，物品不可拆分
```java
import java.util.*;

public class MainSolution {

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int bagSize = Integer.parseInt(sc.nextLine());
        String weightStr = sc.nextLine();
        String valueStr = sc.nextLine();
        int len = weightStr.split(" ").length;
        int[] weightList = new int[len];
        int[] valueList = new int[len];
        for (int i=0;i<len;i++){
            weightList[i] = Integer.parseInt(weightStr.split(" ")[i]);
            valueList[i] = Integer.parseInt(valueStr.split(" ")[i]);
        }printMaxValue(bagSize,len, weightList,valueList);
    }

    public static  void  printMaxValue(int bagSize, int count, int[] weightList, int[] valueList){
        if (count==1){
            if (bagSize>=weightList[0])
                System.out.println("Max Value is :"+valueList[0]);
            else
                System.out.println("Can NOT put any value!");
        }else if (count==0)
            System.out.println("Nothing Can put in.");
        else {
            int[][] res = new int[count+1][bagSize+1];
            for (int i=1;i<=count;i++){
                for (int j=1;j<=bagSize;j++){
                    // 放得下当前物品就比较不放时的值和放入之后的最大值比较
                    if (weightList[i-1]<=j) {
                        res[i][j] = Math.max(res[i - 1][j], res[i - 1][j - weightList[i - 1]] + valueList[i - 1]);
                    }// 放不下就和没有放的时候value保持一致
                    else
                        res[i][j] = res[i-1][j];
                }
            }
            System.out.println("MaxValue is "+res[count][bagSize]+"\nMetric is :\n");
            for (int i=0;i<=count;i++) {
                for (int j = 0; j <= bagSize; j++)
                    System.out.print(res[i][j] + "\t");
                System.out.println("");
            }
        }
        return;
    }
}
```

<a id="%E4%B8%A4%E7%AB%AF%E5%8F%96%E6%95%B0"></a>
## 两端取数 ##
先手取数保证和最大，每次可选两端任意数
```java
import java.util.Scanner;

public class MainSolution {

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();
        int len = input.split(" ").length;
        int[] nums = new int[len];
        for (int i=0;i<len;i++)
            nums[i] = Integer.parseInt(input.split(" ")[i]);
        boolean flag = isWinner(nums);
        System.out.println(flag?"Yes":"No");
    }
    public static boolean isWinner(int[] input) {
        int sum = 0;
        for(int i=0;i<input.length;i++)
            sum += input[i];
        int len = input.length;
        int[][] res = new int[len][len];
        for(int i = 0; i < len; i++)
            res[i][i] = input[i];
        for(int j = 1; j < len; j++)
            res[j-1][j] = Math.max(res[j-1][j-1], res[j][j]);
        for(int i = 2; i < len; i++) {
            for (int line = 0; i + line < len; line++) {
                //A拿左边i的时候B拿i+1或者最右的j即为value[i]+min(dp[i][i+1]，dp[i][j])
                //A拿右边j的时候B拿j-1或者最左的i即为value[j]+min(dp[j][j-1],dp[j][i])
                //以上两种情况再去max
                res[line][line + i] = Math.max(input[line] + Math.min(res[line + 2][i + line], res[line + 1][i + line - 1]),
                        input[i + line] + Math.min(res[line + 1][i + line - 1], res[line][i + line - 2]));
            }
        }
        return res[0][len-1] >= (sum - res[0][len-1]);
    }
}

```

<a id="%E6%9C%80%E5%A4%A7%E8%BF%9E%E7%BB%AD%E5%AD%90%E5%BA%8F%E5%88%97%E5%92%8C"></a>
## 最大连续子序列和 ##
不一定是负数就不可取，可能取了负数之后的正数更大，是简单的动态规划，取之前最大值加当前值和当前值比较
```java
public static void getMaxSum(int[] inputList, int len){
        int preSum = 0,maxSum = 0;
        for (int i=0;i<len;i++){
            //若之前的序列和小于0，则取当前值作为序列和(当前值也有可能小于0，不必在意)
            //之前的序列和不小于0，取之前序列和加上当前值作为最新的序列和(可能会加上负数导致结果小于之前的序列和)
            preSum = preSum<=0?inputList[i]:(preSum+inputList[i]);
            //maxSum代表着之前序列的和与加上当前值之后的序列和两者的较大值，即全局最大值
            maxSum = maxSum>preSum?maxSum:preSum;
        }
        System.out.println(preSum+"\t"+maxSum);
    }
```

<a id="%E6%97%A0%E9%99%90%E7%A1%AC%E5%B8%81%E6%89%BE%E9%9B%B6%E7%BB%84%E5%90%88%E6%95%B0"></a>
## 无限硬币找零组合数 ##
动态规划，每种硬币最多可以用 `sum/coin[i]` 个，可以用0个1个2个一直到`sum/coin[i]`个，用二维填表方法，行代表第i个硬币`coin[i]`，列代表`0-sum`，则dp[i][j]即代表着用前i个硬币组成j的方法数，动态转移方程是`dp[i][j]+=dp[i-1][sum-k*coin[i]]`，其中`0<k<sum/coin[i]`，即用k个硬币，代入到转移方程
```java
public static void getCoinCombin(int[] coins, int sum){
    //考虑到硬币种类为0和sum值为0两种情况，因此二维表要多一行一列边界值
    int[][] dp = new int[coins.length+1][sum+1];
    // 其中第一列代表要用硬币凑出值为0的情况数，这种组合结果就是不拿，因此结果为1
    // 第一行代表用不存在的硬币凑出值sum，这种组合结果不存在，因此结果为0
    for (int i=0;i<=coins.length ;i++ ) 
        dp[i][0] = 1;
    // 每次遍历一行，将前一行的组合数累加进来
    for (int i=0;i<=coins.length ;i++ ) {
        // 对于每一列，第一列初始值为1
        for (int j=1;j<=sum ;j++ ) {
            // 使用同一个硬币的时候组合数都是一样的，关键在于累加
            for (int k=0;k<sum/coins[i] ;k++ ) {
                dp[i][j] += dp[i-1][sum-k*coins[i]]
            }
        }
    }System.out.println(dp[coins.length][sum]);
}

```


<a id="%E4%BA%8C%E5%8F%89%E6%A0%91"></a>
# 二叉树 #
```java
##定义二叉树
class Node{
    Node left;
    Node right;
    int val;
    public void Node(int value){
        this.val = value;
    }
}
```

<a id="%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E9%81%8D%E5%8E%86bfs-queue-%7C-%E7%94%A8%E4%BA%8E%E8%AE%A1%E7%AE%97%E6%B7%B1%E5%BA%A6%E9%AB%98%E5%BA%A6"></a>
## 广度优先遍历BFS-Queue | 用于计算深度高度 ##
1. 非递归方法root先入队；判断root是否有子节点，没有直接出队，有就入左入右
2. 递归方法？？？
```java
##递归实现
public Node BFSRecur(Node root){
    if (root.left==null && root.right==null) 
        return root;
    else if () {
        
    }
}

##非递归实现
public void BFS(Node root){
    if (root == null)
        return;
    Queue<Node> queue = new Queue()<>;
    queue.add(root);
    while(queue.size()!=0){
        Node node = new Node();
        node = queue.remove();
        if (node.left!=null) 
            queue.add(node.left);
        if (node.right!=null) 
            queue.add(node.right);
    }
}

```

<a id="%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E9%81%8D%E5%8E%86dfs-stack-%7C-%E7%94%A8%E4%BA%8E%E5%89%8D%E4%B8%AD%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86"></a>
## 深度优先遍历DFS-Stack | 用于前中后序遍历 ##
1. 递归方法root入栈；判断root是否有子节点，没有直接出栈，有就递归入右入左最后出栈左树再右树
2. 非递归方法判断左树不为空再判断右树不为空
```java
##递归实现
public Node DFSRecur(Node root){
    if (root.left==null && root.right==null)
        return root;
    //先遍历左子树
    if (root.left!=null)
        return DFSRecur(root.left)
    //再遍历右子树
    if (root.right!=null) 
        return DFSRecur(root.right)
}
##非递归实现
public void DFS(Node root){
    if (root == null ) 
        return root;
    Stack<Node> stack = new Stack<>();
    stack.push(root);
    while(stack.size()!=0){
        Node node = stack.pop();
        //栈先压右节点再压左节点，打印的时候即可满足先出左节点再出右节点
        if (node.right != null)
            stack.push(node.right);
        if (node.left !=null)
            stack.push(node.left);
    }
}
```

<a id="dijkstra-%E7%AE%97%E6%B3%95"></a>
## Dijkstra 算法 ##
>迪杰斯特拉(Dijkstra)算法是典型 **最短路径算法**，用于计算一个节点到其他节点的最短路径。它的主要特点是以起始点为中心向外层层扩展(广度优先搜索思想)，直到扩展到终点为止。

![dijkstra](https://upload-images.jianshu.io/upload_images/9949918-ca1f25e72f90f53c.png?imageMogr2/auto-orient/strip|imageView2/2/w/276/format/webp)

1. 指定一个节点，例如我们要计算 'A' 到其他节点的最短路径
2. 引入两个集合（S、U），S集合包含已求出的最短路径的点（以及相应的最短长度），U集合包含未求出最短路径的点（以及A到该点的路径，注意 如上图所示，A->C由于没有直接相连 初始时为∞）
3. 初始化两个集合，S集合初始时 只有当前要计算的节点，`A->A = 0`，
U集合初始时为 `A->B = 4, A->C = ∞, A->D = 2, A->E = ∞`
4. 从U集合中找出路径最短的点，加入S集合，例如 `A->D = 2`
5. 更新U集合路径，`if ( 'D 到 B,C,E 的距离' + 'AD 距离' < 'A 到 B,C,E 的距离' )` 则更新U
6. 循环执行 4、5 两步骤，直至遍历结束，得到A 到其他节点的最短路径

<a id="%E6%9C%8B%E5%8F%8B%E5%9C%88-lt547"></a>
## 朋友圈 lt547 ##
```java
// 递归方法
public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int dim = Integer.parseInt(sc.nextLine());
        int[][] metrics = new int[dim][dim];
        int res = 0;
        for (int i=0;i<dim;i++){
            String tmpLine = sc.nextLine();
            for (int j=0;j<dim;j++)
                metrics[i][j] = Integer.parseInt(tmpLine.split(" ")[j]);
        }for (int i = 0;i<metrics.length;i++)
            if (dfsRecur(metrics,i))
                res++;
        System.out.println(res);
    }

    public static boolean dfsRecur(int[][] met, int cur){
        boolean flag = false;
        for (int i=0;i<met.length;i++){
            // 判断cur这一行的第i列是否为0，即cur和第i个人第关系是否被遍历到
            // 虽然for循环是在行的纬度上，但是行列相等不影响结果
            if (met[cur][i]==0)
                continue;
            // 标记为已遍历
            met[cur][i] = 0;
            met[i][cur] = 0;
            flag = true;
            dfsRecur(met,i);
        }
        return flag;
    }
```

<a id="%E5%88%86%E7%B3%96%E6%9E%9C"></a>
## 分糖果 ##
<a id="rating%E9%AB%98%E7%9A%84%E5%A4%9A%E4%BA%8Erating%E4%BD%8E%E7%9A%84"></a>
### Rating高的多于Rating低的 ###
初始化最终数组res[len]为1；一次循环判断rate[i+1]是否大于rate[i]，成立则res[i]+=1，否则res[i]保持初始值为1；二次循环判断rate[i-1]是否大于rate[i]，成立则res[i-1]=Math.max(res[i-1],res[i])
```java
public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String input = sc.nextLine();
        int len = input.split(" ").length;
        int[] rating = new int[len];
        for (int i =0;i<len;i++)
            rating[i] = Integer.parseInt(input.split(" ")[i]);
        int[] res = new int[len];
        //初始化为1
        for (int i =0;i<len;i++)
            res[i] = 1;
        //第一次循环把递增序列都值都加一
        for (int i=0;i<len-1;i++)
            if (rating[i+1]>rating[i])
                res[i+1] = res[i]+1;
        //第二次循环把递减序列都值逆向加一，取原值和加一后的最大值作为最终值
        for (int i=len-1;i>0;i--)
            if (rating[i-1]>rating[i])
                res[i-1] = Math.max(res[i]+1,res[i-1]);
        for (int i=0;i<len;i++)
            System.out.println("res["+i+"] is :\t"+res[i]);
    }
```