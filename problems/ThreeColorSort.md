## 三色排序问题

问题描述：

给定一个数组，里面只有0，1，2三种元素，对其进行排序。

一种思路是：可知数组元素是有范围的，可以使用计数排序。

另一种思路是：双指针

```
#include <iostream>
#include <vector>
using namespace std;


// 三色排序问题
// 实际问题要学会转为计算机问题：其实就是一个整型数组（含三种元素0，1，2）对他进行排序
void ThreeColorSort(vector<int>& arr, int count) {
    // 双指针 first指向0-1分界的1；last指向1-2分界的1
    int first = 0, last = count - 1;
    
    // 注意这里：排好序之后后面的元素都是2了，就不需要排序
    // 否则会一直与last指向的1-2分界前的1交换位置
    for(int i = 0; i <= last; ++i) {
        // 如果指向2，就与last交换位置
        if(arr[i] == 2) {
            swap(arr[i], arr[last]);
            last--;
        }
        // 如果指向0，就与first交换位置
        else if(arr[i] == 0) {
            swap(arr[i], arr[first]);
            first++;
        }
    }
}

int main(int argc, const char * argv[]) {
    vector<int> arr = { 2, 2, 0, 0, 1, 1 };
    ThreeColorSort(arr, 6);
    for(int i = 0; i < arr.size(); ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;
    return 0;
}

```
