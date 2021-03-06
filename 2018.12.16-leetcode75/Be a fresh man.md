## 075_(颜色分类)Sort Colors
## 1 问题描述、输入输出与样例
### 1.1 问题描述
给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。<br>
此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。<br>
__注意__:
不能使用代码库中的排序函数来解决这道题。

__进阶__：
* 一个直观的解决方案是使用计数排序的两趟扫描算法。首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。<br>
* 你能想出一个仅使用常数空间的一趟扫描算法吗？
### 1.2 输入与输出
输入：
* vector<int>& nums: 输入的颜色数组

输出：
* void:原地修改
### 1.3 样例
#### 1.3.1 样例1
输入: [2,0,2,1,1,0]<br>
输出: [0,0,1,1,2,2]<br>
## 2 思路描述与代码	
### 2.1 思路描述（一遍扫描法）
i, j, k分别指向最后的0, 1, 2位置<br>
一趟扫描元素 x :<br>
if(x == 0) i, j, k 位置先后置位相应的元素并位置加1<br>
else if(x == 1) j, k 位置先后置为相应的元素并位置都加1<br>
else k 位置置为相应的元素并位置都加1<br>

比如输入[2,0,2,1,1,0]<br>
i, j, k初始化为-1<br>
x = 2, 下标位置0置2，i = -1, j = -1, k = 0, 此时数组为[2,0,2,1,1,0]<br>
x = 0, 下标位置1置2，下标位置0置0, i = 0, j = 0, k = 1, 此时数组为[0,2,2,1,1,0]<br>
x = 2, 下标位置2置2，i = 0, j = 0, k = 2, 此时数组为[0,2,2,1,1,0]<br>
x = 1, 下标位置3置2，下标位置1置1, i = 0, j = 1, k = 3, 此时数组为[0,1,2,2,1,0]<br>
x = 1, 下标位置4置2，下标位置2置1, i = 0, j = 2, k = 4, 此时数组为[0,1,1,2,2,0]<br>
x = 0, 下标位置5置2，下标位置3置1, 下标位置1置0, i = 1, j = 3, k = 5, 此时数组为[0,0,1,1,2,2]<br>
### 2.2 代码
```cpp
void sortColors(vector<int>& nums) {
    int numsSize = nums.size();
    int i = -1, j = -1, k = -1;//三个指针，i, j, k分别指向最后的0, 1, 2
    //printf("%d %d\n", nums[0], nums[1]);
    for(int l=0; l<numsSize; l++){
        if(0 == nums[l]){
            nums[++k] = 2;
            nums[++j] = 1;
            nums[++i] = 0;
            //printf("%d %d\n", nums[0], nums[1]);
        }
        else if(1 == nums[l]){
            nums[++k] = 2;
            nums[++j] = 1;
        }
        else
            nums[++k] = 2;
    }
}
```
## 3 思考与拓展
### 3.1 思考
本题使用下标记录三种颜色的最后一个位置，可以做到一遍扫描即原地修改。
#### 3.1.1 其他方法
#### 3.1.1.1 两遍扫描
先扫描一遍，记录0、1、2的个数<br>
然后根据个数置0、1、2
#### 3.1.2 复杂度分析
方法|空间复杂度|时间复杂度
--- | --- | ---
一遍扫描法|O(1)|0(n)
两遍扫描法|O(1)|0(n)，时间复杂度的常数C更大
#### 3.1.3 难点分析
1. i, j, k的更新规则

### 3.2 拓展
无。
