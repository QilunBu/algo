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









































