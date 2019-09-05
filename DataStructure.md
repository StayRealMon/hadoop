# 排序 #
![](https://images2017.cnblogs.com/blog/1303641/201801/1303641-20180124091639006-2029462359.png)

##快速排序##
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

## 直接插入排序 ##
第一轮比较前两个数，第二轮拿第三个与前两个相比，以此类推，每一轮将第N+1个数和前面N个有序的数比较，比较之后前N+1个数有序

## 选择插入排序 ##
第一轮挑选N个数中最小的数放第一，第二轮从剩余N-1个数中找到最小的放到第二位，以此类推每次把剩余数中最小的放到前面有序队列的最后

##比较次数和初始序列##
1. 插排 时间复杂度与比较次数，移动次数都与初始序列有关
2. 快排 时间复杂度与比较次数，与移动次数都与初始序列有关
3. 归排 时间复杂度与初始序列无关，比较次数有关（有序序列），移动次数无关（无论怎么有序，还是每个元素拷贝到新的数组）
4. 选排 时间复杂度与初始序列无关，比较次数无关，移动次数无关
5. 冒排 时间复杂度与初始序列无关，比较次数无关，移动次数有关

> 一堆（堆排序）乌龟（归并排序）选（选择排序）基（基数排序——算法复杂度与数组的初始状态无关

## 确定最终位置 ##
1. 简单选择排序每次选择未排序列中的最小元素放入其最终位置
2. 希尔排序每次是对划分的子表进行排序，得到局部有序的结果，所以不能保证每一趟排序结束都能确定一个元素的最终位置
3. 快速排序每一趟排序结束后都将枢轴元素放到最终位置
4. 堆排序属于选择排序，每次都将大根堆的根结点与表尾结点交换，确定其最终位置
5. 二路归并排序每趟对子表进行两两归并从而得到若干个局部有序的结果，但无法确定最终位置


## 链表 ##
### 头插法 ###
```java
while(oldList.hasNext()):
    //赋值给一个新节点
    Node new = oldList.hasNext();
    //记录头插新链表的链接信息
    next = head.next;
    //头插新链表的新链接
    new.next = next;
    //新节点连到头后面
    head.next = new;

```

### 原地逆置 ###
1. 节点防断裂;
2. head为空或者仅有head
3. pre，head，next三个指针

```java
    while(head!=null):
        //记录原顺序的next
        next = head.next; 
        //切断原连接，将head的下一个节点由next指向pre
        head.next = pre;
        //pre, head, next依次往后移一位
        pre = head; head = next; next = head.next; 
```

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

## 动态规划 ##
最优子问题/动态转移方程/边界->进阶背包问题

青蛙跳台阶/拿硬币等问题啊，数值可能过大，数组可以用`Long[]`代替`int[]`

### 二维数组最短路径 ###
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
### 类二叉树的最短路径 ###
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
### 抢银行 ###
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