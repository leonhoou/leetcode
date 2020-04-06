### 堆

包含建堆，堆化（自顶向下、自底向上），堆中插入元素，删除堆顶元素，堆排序

```
#include <iostream>
using namespace std;

/**
 * 堆：
 * 1. 一个完全二叉树（适合数组存储）；
 * 2. 只有两种-大顶堆，小顶堆；
 *
 * 应用：TopK；流里面的中位数；优先级队列；
 * 这里是大顶堆的例子
 */
class MyHeap {
public:
    int* arr;  // 动态初始化数组（arr[0]不存元素，方便下标计算）
    int size;  // 堆大小
    int count; // 堆元素数量
    
    MyHeap(int size) {
        this->size = size;
        this->count = 0;
        arr = new int[this->size+1]();
    }
    
    MyHeap(int* arr, int count, int size) {
        this->count = count;
        this->size = size;
        buildHeap2(arr, count, size);
    }
    
    /**
     * 向堆中插入元素
     * 思路：插到数组最后，再自底向上堆化
     * 时间复杂度：主要是堆化，即树的高度 O(logn)
     */
    void insertHeap(int num) {
        if(this->count >= this->size) {
            return;
        }
        this->count++;
        this->arr[this->count] = num;
        // 堆化
        // 从下往上堆化
        downTopHeapify(this->arr, this->count);
    }
    
    /**
     * 删除堆顶元素，并返回
     * 思路：交换堆顶与最后一个元素，再自顶向下堆化
     * 时间复杂度：主要是堆化，即树的高度 O(logn)
     */
    int deleteHeap() {
        if(this->count < 1) {
            return -1;
        }
        int res = this->arr[1];
        this->arr[1] = this->arr[this->count];
        this->count--;
        // 从上往下堆化
        TopDownHeapify(this->arr, this->count, 1);
        return res;
    }
    
    /**
     * 堆排序
     * 原地排序算法，时间复杂度：O(nlogn)，不稳定排序算法
     * 一般不稳定就是：距离大的交换元素位置
     * 两个过程：建堆，排序
     * 建堆：原地
     * 方法1. 每次向堆里添加一个元素，再自底向上堆化
     * 方法2. 对每个非叶子结点进行自顶向下的堆化过程
     * 排序：原地
     * 类似删除堆顶元素，每次交换堆顶元素和堆尾元素，相当于将最大元素放到了数组末尾，再对堆顶元素建堆（建堆过程不含堆尾）
     */
    void heapSort(int* arr, int count, int size) {
        // 建堆：O(n)
        buildHeap2(arr, count, size);
        // 排序：O(nlogn)
        int tmp;
        while(count > 0) {
            tmp = arr[count];
            arr[count] = arr[1];
            arr[1] = tmp;
            count--;
            TopDownHeapify(this->arr, count, 1);
        }
    }
    
    /**
     * 建堆（方法二）
     * 思路：给定一个数组，从第一个非叶子结点开始自顶向下堆化
     * 时间复杂度：O(n)
     */
    void buildHeap2(int* arr, int count, int size) {
        // 需要先初始化（分配空间）
        this->arr = new int[size+1];
        for(int i = 1; i <= count; ++i) {
            this->arr[i] = arr[i-1];
        }
        // 建堆操作
        int notLeafIdx = count / 2;
        for(int i = notLeafIdx; i > 0; --i) {
            TopDownHeapify(this->arr, this->count, i);
        }
    }
    
    /**
     * 自底向上堆化
     * 思想：最后一个w叶子结点慢慢向上堆化（交换位置）
     */
    void downTopHeapify(int* arr, int idx) {
        int tmp;
        while(idx/2 > 0 && arr[idx] > arr[idx/2]) {
            tmp = arr[idx];
            arr[idx] = arr[idx/2];
            arr[idx/2] = tmp;
            idx = idx / 2;
        }
    }
    
    /**
     * 自顶向下堆化（从位置idx开始）
     * 思想：顶元素与子最大元素交换位置
     */
    void TopDownHeapify(int* arr, int count, int idx) {
        int tmp, maxIdx;
        while(idx < count) {
            maxIdx = idx;
            // count就是最后一个元素的索引，所以要等号
            if(idx*2 <= count && arr[idx] < arr[idx*2])
                maxIdx = idx * 2;
            if(idx*2+1 <= count && arr[maxIdx] < arr[idx*2+1])
                maxIdx = idx * 2 + 1;
            if(maxIdx == idx)
                break;
            tmp = arr[idx];
            arr[idx] = arr[maxIdx];
            arr[maxIdx] = tmp;
            idx = maxIdx;
        }
        
    }
};

int main() {
//    MyHeap* heap = new MyHeap(6);
//    heap->insertHeap(6);
//    heap->insertHeap(3);
//    heap->insertHeap(5);
//    heap->insertHeap(8);
//    heap->insertHeap(2);
//    heap->insertHeap(4);
//    int arr[10] = {5,6,3,4,8,1,2,7,10,20};
//    MyHeap* heap = new MyHeap(arr, 10, 11);
//    for(int i = 1; i < heap->count+1; ++i) {
//        cout << heap->arr[i] << " ";
//    }
//    cout << endl;
//    while(heap->count > 0) {
//        cout << heap->deleteHeap() << " ";
//    }
//    cout << endl;
    int arr[10] = {5,6,3,4,8,1,2,7,10,20};
    MyHeap* heap = new MyHeap(6);
    heap->heapSort(arr, 10, 10);
    for(int i = 0; i < 10; ++i) {
        cout << arr[i] << " ";
    }
}


```
