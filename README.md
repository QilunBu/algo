# algo
时间复杂度 一个操作得到了表达式，譬如 aN^2 + bn + c, 不要低阶项，忽略高阶项的系数，然后得到的，以例子为例，O(N^2)表达式
----------------------------------------------------------------------
选择排序
public static void sortArray(int[] array){
        if (array == null || array.length < 2){
            return;
        }
        for (int i = 0; i < array.length - 1; i++) {
            int minIndex = i;
            for (int j = 1 + 1; j < array.length; j++) {
               minIndex = array[j] < array[i]? j : minIndex;
            }
            swap(array, i, minIndex);

        }
    }

    public static void swap(int[] array, int i, int j){
        int tmp = array[i];
        array[i] = array[j];
        array[j] = tmp;

    }
---------------------------------------------------------------------------
bubble 排序
    public static void bubbleSort(int[] arr){
        for (int e = arr.length - 1; e > 0; e--) {
            for (int i = 0; i < e; i++) {
                if (arr[i] > arr[i + 1]){
                    swap(arr, i, i+1);
                }
            }
        }
    }

    private static void swap(int[] arr, int i, int j) {
        arr[i] = arr[i] ^ arr[j];  //arr[i] = arr[i] ^ arr[j],  arr[j] = arr[j]
        arr[j] = arr[i] ^ arr[j];  //arr[i] = arr[i] ^ arr[j], arr[j] = arr[i] ^ arr[j] ^ arr[j],  arr[j] ^ arr[j] = 0, arr[i] ^ 0 = arr[i].
        arr[i] = arr[i] ^ arr[j];  //arr[j] = arr[i],  arr[i] = arr[i] ^ arr[j] ^ arr[i], arr[i] = arr[j]
    }
-----------------------------------------------------------------------
^亦或运算，满足交换律结合律 b^b = 0   a^0 = a
------------------------------------------------------------------------
QUERY1:
一个int数组array中， 
1）已知一种数出现奇数次，其余出现偶数次，如何找到这个数。
2）已知两种数出现了奇数次，其余出现偶数次，如何找到这两个数。 
时间复杂度O(N), 空间复杂度O(1).

1)
public static void prongOddNum(int[] arr){
        int eor = 0;
        for (int i : arr) {
            eor ^= i;
        }
        System.out.println(eor);
    }


2)
public static void prongOddNum(int[] arr){
        int eor = 0;
        for (int i = 0; i <arr.length; i++) {
            eor ^= arr[i];
        }
        //eor = a^b
        //eor  != 0
        //eor must have a "1" in position

        //常规操作，一个数字 与 自己的取反加1， 得出这个数字位运算最右边的第一个不为零的数字。
        int rightOne = eor & (~eor + 1); //~eor select the number definitly opposite to the origin number.  instance: eor:10110 ~eor:01001

        int onlyOne = 0;
        for (int i : arr) {
            if ((i & rightOne) == 0){
                onlyOne ^= i;
            }
        }
        int result1 = onlyOne;
        int result2 = eor ^ onlyOne;
        System.out.println(result1 + result2);
    }
如何在有序数组中找到某一个数字‘  二分法  时间复杂都  log2 N

对数器
--------------------------------------------------------------------------
递归算法，简单来说就是方法中调用本方法，就是递归。详情 https://zhuanlan.zhihu.com/p/94748605
public class getMax {

    public static int process(int[] arr, int L, int R) {
        if (L == R) {
            return arr[L];
        }
        int mid = L + ((R - L) >> 1); //request the middle position of the index
        int leftMax = process(arr, L, mid);
        int rightMax = process(arr, mid + 1, R);
        return Math.max(leftMax, rightMax);
    }

    public static int getMax(int[] arr) {
        return process(arr, 0, arr.length - 1);
    }
}
--------------------------------------------------------------
 master公式; T(N) = a * T(N/b) + O(N^d) 应用于子问题等规模的递归行为
 当abd满足logb ^a < d，时间复杂度为O(N^d)
 当abd满足logb ^a > d  时间复杂度为O(N^(logb^a))
 当abd满足logb ^a == d 时间复杂度为O(N^d * log N)
 --------------------------------------------------------------

归并排序：
public class mergeSort {

    public static void process(int[] arr, int L, int R) {
        if (L == R) {
            return;
        }
        int mid = L + ((R - L) >> 1);
        process(arr, L, mid);
        process(arr, mid + 1, R);
        merge(arr, L, mid, R);
    }
    private static void merge(int[] arr, int L, int M, int R) {
        int[] help = new int[R - L - 1];
        int i = 0;
        int p1 = L;
        int p2 = M + 1;
        while (p1 <= M && p2 <= R) { //两个判定挑两件，有一个越界以后，进行下面的判断，两个while只会中一个。
            help[i++] = arr[p1] <= arr[p2] ? arr[p1++] : arr[p2++];
        }
        while (p1 <= M) {//cope rest value to the help
            help[i++] = arr[p1++];
        }
        while (p2 <= R) {//cope rest value to the help
            help[i++] = arr[p2++];
        }
        for (int j = 0; j < help.length; j++) {
            arr[L + j] = help[j];
        }
    }
    public static void mergeSort(int[] arr) {
        if (arr == null || arr.length < 2) {
            return;
        }
        process(arr, 0, arr.length - 1);
    }
}
================================================================
在一个数组中，每一个数的左边比当前数小的数累加起来，叫做这个数组的小和。球一个数组的小和。
例如[1,3,4,2,5] 1左边比1小的数字，没有。3左边比3小的数字，1。 4左边比4小的数字，1，3. 2左边比2小的数字，1. 5左边比5小的数字，1 3 4 2 . 小和为1+1+3+1+1+3+4+2= 16

public class smallSum {
    public static int smallSum(int[] arr){
        if (arr == null || arr.length < 2){
            return 0;
        }
        return process(arr, 0, arr.length - 1);
    }

    private static int process(int[] arr, int l, int r) {
        if (l == r){
            return 0;
        }
        int mid = l + ((r - l) >> 1);
        return process(arr, 1, mid)
                +process(arr, mid + 1, r)
                +merge(arr, 1, mid, r);
    }

    private static int merge(int[] arr, int L, int m, int r) {
        int[] help = new int[r - L + 1];
        int i = 0;
        int p1 = L;
        int p2 = m + 1;
        int result = 0;

        while (p1 <= m && p2 <= r) {
            result = arr[p1] < arr[p2] ? (r-p1 + 1) * arr[p1] : 0;
            help[i++] = arr[p1] < arr[p2] ? arr[p1++] : arr[p2++];
        }
        while (p1 <= m) {//cope rest value to the help
            help[i++] = arr[p1++];
        }
        while (p2 <= r) {//cope rest value to the help
            help[i++] = arr[p2++];
        }
        for (int j = 0; j < help.length; j++) {
            arr[L + j] = help[j];
        }
        return result;
    }
}
-----------------------------------------------------------------------
在一个数组中，左边的数如果比右边的数大，则这两个数构成一个逆序对。打印所有逆序对。
-----------------------------------------------------------------------------
快速排序：
荷兰国旗问题
1：给定数组arr， 和一个数字sum， 请把小于等于sum的数字放在数组左边，大于sum的数字放在数组右边，要求额外空间复杂度O(1), O(N).


























