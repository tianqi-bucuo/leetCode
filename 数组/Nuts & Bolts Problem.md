给定一组 n 个不同大小的 nuts 和 n 个不同大小的 bolts. nuts 和 bolts 一一匹配.
不允许将 nut 之间互相比较, 也不允许将 bolt 之间互相比较. 也就是说, 只许将 nut 与 bolt 进行比较, 或将 bolt 与 nut 进行比较. 我们会提供一个比较函数, 用于nut和bolt的比较.
利用我们提供的函数, 你需要将 nuts 或者 bolts 重新排列, 使得它们按照顺序一一匹配.

***
用nuts对blots进行快速排序，用blots对nuts进行快速排序，对排序后的配对即可。

```Java
public class Solution {
    public void sortNutsAndBolts(String[] nuts, String[] bolts, NBComparator compare) {
        int n = nuts.length, m = bolts.length;
        if(m!=n) {
            return;
        }
        // 通过快速排序的思想进行排序
        quickSort(nuts,bolts,compare, 0, n-1);
    }
    void quickSort(String[] nuts, String[] bolts,NBComparator compare, int start, int end){
        if(start >= end) {
            return;
        }
        int index = partition(nuts,bolts[start], compare, start, end);
        partition(bolts, nuts[index], compare, start, end);// 找到匹配的bolt
        // 将bolts划分为两部分
        quickSort(nuts, bolts, compare, start, index-1);
        quickSort(nuts, bolts, compare, index+1, end);
    }
    int partition(String[] NorB, String pivot, NBComparator compare, int start, int end){
        int m = start;// m表示枢轴的实际位置。
        for(int i = start+1; i<=end; ++i){// 判断并且对nut和bolt通过交换进行排序
            if(compare.cmp(pivot, NorB[i]) == 1 || compare.cmp(NorB[i],pivot) == -1){
                String tmp = NorB[++m];
                NorB[m] = NorB[i];
                NorB[i] = tmp;
            }else if(compare.cmp(pivot,NorB[i]) == 0 || compare.cmp(NorB[i], pivot) == 0){
                String tmp = NorB[start];
                NorB[start] = NorB[i];
                NorB[i] = tmp;
                i--;
            }
        }
        String tmp = NorB[m];
        NorB[m] = NorB[start];
        NorB[start] = tmp;
        return m;
    }
};
```