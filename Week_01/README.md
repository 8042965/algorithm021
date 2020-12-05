## 本周作业

### 简单：

- 用 add first 或 add last 这套新的 API 改写 Deque 的代码
- 分析 Queue 和 Priority Queue 的源码
- [删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)（Facebook、字节跳动、微软在半年内面试中考过）
- [旋转数组](https://leetcode-cn.com/problems/rotate-array/)（微软、亚马逊、PayPal 在半年内面试中考过）
- [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)（亚马逊、字节跳动在半年内面试常考）
- [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)（Facebook 在半年内面试常考）
- [两数之和](https://leetcode-cn.com/problems/two-sum/)（亚马逊、字节跳动、谷歌、Facebook、苹果、微软在半年内面试中高频常考）
- [移动零](https://leetcode-cn.com/problems/move-zeroes/)（Facebook、亚马逊、苹果在半年内面试中考过）
- [加一](https://leetcode-cn.com/problems/plus-one/)（谷歌、字节跳动、Facebook 在半年内面试中考过）

### 中等：

- [设计循环双端队列](https://leetcode.com/problems/design-circular-deque)（Facebook 在 1 年内面试中考过）

### 困难：

- [接雨水](https://leetcode.com/problems/trapping-rain-water/)（亚马逊、字节跳动、高盛集团、Facebook 在半年内面试常考）

## 下周预习

### 预习题目：

- [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/description/)
- [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
- [最小的 k 个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)







## 本周作业提交内容

### 简单：

#### 1、【×】用 add first 或 add last 这套新的 API 改写 Deque 的代码

**时间不太够，待补**

#### 2、【×】分析 Queue 和 Priority Queue 的源码

**时间不太够，待补**

#### 3、【√】[删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)（Facebook、字节跳动、微软在半年内面试中考过）



**自己****做的：**

> 可以看到题目中提到了给出的数组是有序的，所以重复的数据一定是挨着的，所以可以顺序查找，那么就需要遍历
>
> 整个数组以此达到目的。
>
> 在遍历的过程中使用一个一个指针始终记录着前一个不是重复的位置。
>
> 以此遍历。
>
> 如果与N+1个位置都是重复的那么就跳过，继续寻找下一个不是重复的位置，并把此数据记录在前一个不是重复位置的后面即可。
>
> 最终返回不是重复位置的指针+1即是这个范围。
>
> 
>
> 也是双指针，但是不如别人的简洁



```java
    public int removeDuplicates(int[] nums) {
        int oldLen = nums.length;

        int newIndex = 0; //前一个
        for (int i = 1; i < oldLen; i++) {
            //如果前一个等于后一个数，就
            while (nums[newIndex] == nums[i]){
                i++;

                //如果i到头了，说明整个数组都是重复的，就返回1即可
                if(i==oldLen){
                    return ++newIndex;
                }
            }

            //走到这，说明nums[j] != nums[i]
            nums[++newIndex]=nums[i];
        }

        //最终的索引长度+1就是需要的范围
        return ++newIndex;
    }
```

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1101539/1606832314962-4ffe6a75-c8ee-496b-83a3-b275d6d37f1e.png)



看到一个赞同数比较高的：

```java
 static public int removeDuplicates2(int[] nums) {

       if(nums==null || nums.length == 0) return 0;

       int oldLen = nums.length;

       int i = 0;//始终指定着前一个不是重复的位置
       int j = 1;//一直向后走，找到不是重复的位置

       while (j < oldLen){

           //如果不相等
           if(nums[i] != nums[j]){
               nums[i+1] = nums[j];
               i++;
           }
           j++;
       }

       return i+1;

    }
```





#### 4、【√】[旋转数组](https://leetcode-cn.com/problems/rotate-array/)（微软、亚马逊、PayPal 在半年内面试中考过）



自己写的：



```java
    public void rotate(int[] nums, int k) {
        int len = nums.length-1;

        //从第k个开始旋转,如果k=3，说明要循环3次
        for (int i = k ; i > 0 ; i--) {
            //临时记录下来需要提到前面的数字
            int temp = nums[len];

            //向后挪动，从第1个位置开始往后挪动
            for (int j = len-1 ; j >= 0 ; j--) {
                nums[j+1] = nums[j];
            }
            nums[0] = temp;
        }
    }
```

![image.png](https://cdn.nlark.com/yuque/0/2020/png/1101539/1606836279744-4cc07fe5-07a8-40d5-a77b-55c6ae9d3994.png)



虽然成功了，但是耗时时间复杂度太高



时间复杂度达到了O(kn)级







#### 5、【√】[合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)（亚马逊、字节跳动在半年内面试常考）



```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        
        if(l1==null){
            return l2;
        } 

        if(l2==null){
            return l1;
        }

        int v1 = l1.val;
        int v2 = l2.val;
        
        if(v1<v2){
            l1.next = mergeTwoLists(l1.next,l2);
            return l1;
        }else{
            l2.next = mergeTwoLists(l1,l2.next);
            return l2;
        }

    }
}
```



#### 6、【√】[合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)（Facebook 在半年内面试常考）



```java
//给你两个有序整数数组 nums1 和 nums2，请你将 nums2 合并到 nums1 中，使 nums1 成为一个有序数组。 
//
// 
//
// 说明： 
//
// 
// 初始化 nums1 和 nums2 的元素数量分别为 m 和 n 。 
// 你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。 
// 
//
// 
//
// 示例： 
//
// 
//输入：
//nums1 = [1,2,3,0,0,0], m = 3
//nums2 = [2,5,6],       n = 3
//
//输出：[1,2,2,3,5,6] 
//
// 
//
// 提示： 
//
// 
// -10^9 <= nums1[i], nums2[i] <= 10^9 
// nums1.length == m + n 
// nums2.length == n 
// 
// Related Topics 数组 双指针 
// 👍 704 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if (m == 0) {
            nums1[0] = nums2[0];
        }
        m--;
        n--;

        while (m >= 0 && n >= 0) {
            if (nums1[m] > nums2[n]) {
                nums1[m + n + 1] = nums1[m];
                m--;
            } else {
                nums1[m + n + 1] = nums2[n];
                n--;
            }
        }

        int index = m + n + 1;
        if (m == -1 && n >= 0) {
            while (n >= 0) {
                nums1[index--] = nums2[n--];
            }
        }

        if (m >= 0 && n == -1) {
            while (m >= 0)
                nums1[index--] = nums1[m--];
        }
    }
}
//leetcode submit region end(Prohibit modification and deletion)
```



#### 7、【√】[两数之和](https://leetcode-cn.com/problems/two-sum/)（亚马逊、字节跳动、谷歌、Facebook、苹果、微软在半年内面试中高频常考）

```java
package 算法训练营.第一周.练习;

import java.util.Arrays;

public class 两数之和 {
    static public int[] twoSum(int[] nums, int target) {


        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i+1; j < nums.length ; j++) {
                if(nums[i] + nums[j] == target){
                    return new int[]{i,j};
                }
            }
        }

        return new int[]{};
    }

    public static void main(String[] args) {
        int [] nums = {3,3};
        int target = 6;

        int[] ints = twoSum(nums, target);
        System.out.println(Arrays.toString(ints));
    }
}
```



#### 8、【√】[移动零](https://leetcode-cn.com/problems/move-zeroes/)（Facebook、亚马逊、苹果在半年内面试中考过）



```java
package 算法训练营;

public class moveZeroes {
    static public void moveZeroes(int[] nums) {
        int j = 0;

        for (int i = 0; i < nums.length; i++) {
            //如果遇到的数据为0，就把后面的往前移动。例如：[0,1,0,3,12] -> [1,0,3,12,0]
            if(nums[i]!=0){
                //向前移动
                nums[j] = nums[i];
                if(i != j){
                    nums[i] = 0;
                }
                j++;
            }
        }
    }

    static public int maxArea(int[] height) {

        int max = 0;

        for(int i = 0; i < height.length -1 ; i++){
            for(int j = i + 1 ; j < height.length; j++){
                int area = ( j - i) * Math.min(height[i],height[j]);
                max = Math.max(area,max);
            }
        }

        return max;
    }

    public static void main(String[] args) {

//        int[] array = {4,3,2,1,4};
//        System.out.println(maxArea(array));
        int [] ints = {0,1,0,3,12};
//        int [] ints = {0,0,1};
        moveZeroes(ints);

        for (int anInt : ints) {
            System.out.print(anInt+",");
        }

    }
}
```





#### 9、【√】[加一](https://leetcode-cn.com/problems/plus-one/)（谷歌、字节跳动、Facebook 在半年内面试中考过）





```java
package 算法训练营.第一周.练习;

import java.util.Arrays;

public class 加一 {

   static public int[] plusOne(int[] digits) {

        for (int i = digits.length-1; i >= 0; i--) {
            //从尾部开始+1
            digits[i]++;

            digits[i] %= 10;

            //如果模10之后不等于0，说明不需要进位了，就直接返回现在的数组极客
            if(digits[i]  != 0)
                return digits;
        }

        //说明[9,0,0]出现这种情况了，第1个数为9
        int newIntArray[] = new int[digits.length+1];
        newIntArray[0]=1;

        return newIntArray;
    }

    public static void main(String[] args) {
        System.out.println(Arrays.toString(plusOne(new int[]{9,9})));
    }
}
```



### 中等：

#### 1、[设计循环双端队列](https://leetcode.com/problems/design-circular-deque)（Facebook 在 1 年内面试中考过）



自己做了好久，都不太行，而且设计的还比较复杂：

```java
package 算法训练营.第一周.练习;

import java.util.Arrays;

public class 设计循环双端队列 {
    public static void main(String[] args) {
        MyCircularDeque myCircularDeque = new MyCircularDeque(3);

        boolean b = myCircularDeque.insertLast(1);
        boolean b1 = myCircularDeque.insertLast(2);
        boolean b2 = myCircularDeque.insertFront(3);
        boolean b3 = myCircularDeque.insertFront(4);
        int rear = myCircularDeque.getRear();
        boolean full = myCircularDeque.isFull();
        boolean b4 = myCircularDeque.deleteLast();
        boolean b5 = myCircularDeque.insertFront(4);
        int front = myCircularDeque.getFront();
        System.out.println(b);

    }
}

class MyCircularDeque {

    static int[] data = null;
    static int len = 0;
    static int add_len = 0;//插入的数据计数器

    static int fornt_index = 0;//记录前面插入的位置
    static int last_index = 0;//记录后面插入的位置

    /** Initialize your data structure here. Set the size of the deque to be k. */
    public MyCircularDeque(int k) {
        data = new int[k];
        Arrays.fill(data,-1);
        len = k;
        last_index = k-1;
    }

    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    public boolean insertFront(int value) {

        if(add_len >= len ){
            return false;
        }else{

            //1、挪动位置(向后)
            for (int i = fornt_index+1; i > 0 ; i--) {
                data[i+1] = data[i];
                fornt_index--;
                data[i]=-1;
            }
//            for (int i = fornt_index ; i < last_index-1 ; i++) {
//                System.out.println("--->"+data[i]);
//                data[i+1] = data[i];
//                fornt_index--;
//                data[i]=-1;
//            }

            //2、把数据写入第一个位置
            data[0] = value;

            fornt_index++;

            add_len++;//计数

            return true;
        }
    }

    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    public boolean insertLast(int value) {
        //1、把数据写入最后一个位置
        try {
            
            //1、挪动位置
            if(last_index < len-1){
                for (int i = len-1  ; i > last_index; i--) {
                    System.out.println("--->"+data[i]);
                    data[i-1] = data[i];
                    last_index++;
                    data[i]=-1;
                }
            }

            data[last_index--] = value;
            add_len++;//计数

            return true;
        }catch (Exception e){
            return false;
        }
    }

    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    public boolean deleteFront() {
        try {
            //1、从第1个位置 向前挪
            for (int i = 0 ; i < len - 1  ; i++) {
                data[i] = data[i+1];
            }

            //2、数量-1
            add_len--;
            return true;
        }catch (Exception e){
            return false;
        }
    }

    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    public boolean deleteLast() {
        try {
            //1、从第last_index个位置 向前挪
            for (int i = last_index ; i < len - 1  ; i++) {
                data[i+1] = data[i];
            }

            //恢复-1
            data[last_index] = -1;

            last_index--;
            add_len--;

            return true;
        }catch (Exception e){
            return false;
        }
    }

    /** Get the front item from the deque. */
    public int getFront() {
        return fornt_index==0 ? -1 : data[0];
    }

    /** Get the last item from the deque. */
    public int getRear() {
        return data[len-1];
    }

    /** Checks whether the circular deque is empty or not. */
    public boolean isEmpty() {
        return add_len==0;
    }

    /** Checks whether the circular deque is full or not. */
    public boolean isFull() {
        return add_len==len;
    }
}
```



学习的比较经典的一个：



https://leetcode-cn.com/problems/design-circular-deque/solution/shu-zu-shi-xian-de-xun-huan-shuang-duan-dui-lie-by/



```java
//设计实现双端队列。 
//你的实现需要支持以下操作： 
//
// 
// MyCircularDeque(k)：构造函数,双端队列的大小为k。 
// insertFront()：将一个元素添加到双端队列头部。 如果操作成功返回 true。 
// insertLast()：将一个元素添加到双端队列尾部。如果操作成功返回 true。 
// deleteFront()：从双端队列头部删除一个元素。 如果操作成功返回 true。 
// deleteLast()：从双端队列尾部删除一个元素。如果操作成功返回 true。 
// getFront()：从双端队列头部获得一个元素。如果双端队列为空，返回 -1。 
// getRear()：获得双端队列的最后一个元素。 如果双端队列为空，返回 -1。 
// isEmpty()：检查双端队列是否为空。 
// isFull()：检查双端队列是否满了。 
// 
//
// 示例： 
//
// MyCircularDeque circularDeque = new MycircularDeque(3); // 设置容量大小为3
//circularDeque.insertLast(1);                  // 返回 true
//circularDeque.insertLast(2);                  // 返回 true
//circularDeque.insertFront(3);                 // 返回 true
//circularDeque.insertFront(4);                 // 已经满了，返回 false
//circularDeque.getRear();                  // 返回 2
//circularDeque.isFull();                       // 返回 true
//circularDeque.deleteLast();                   // 返回 true
//circularDeque.insertFront(4);                 // 返回 true
//circularDeque.getFront();             // 返回 4
//  
//
// 
//
// 提示： 
//
// 
// 所有值的范围为 [1, 1000] 
// 操作次数的范围为 [1, 1000] 
// 请不要使用内置的双端队列库。 
// 
// Related Topics 设计 队列 
// 👍 65 👎 0


import java.util.Arrays;

//leetcode submit region begin(Prohibit modification and deletion)
class MyCircularDeque {


    private int capacity;
    private int [] arr;
    private int front;
    private int rear;


    /** Initialize your data structure here. Set the size of the deque to be k. */
    public MyCircularDeque(int k) {
        capacity = k +1;
        arr = new int[capacity];
        front = 0;
        rear = 0;
    }

    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    public boolean insertFront(int value) {
        if(isFull()){
            return false;
        }

        front = (front -1 + capacity) % capacity;
        arr[front] = value;
        return true;
    }

    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    public boolean insertLast(int value) {
        if (isFull()) {
            return false;
        }

        arr[rear] = value;

        rear = (rear +1) %capacity;
        return true;
    }

    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    public boolean deleteFront() {
        if (isEmpty()) {
            return false;
        }

        front = (front+1) % capacity;
        return true;
    }

    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    public boolean deleteLast() {
        if (isEmpty()) {
            return false;
        }
        rear = (rear - 1 + capacity) % capacity;
        return true;
    }

    /** Get the front item from the deque. */
    public int getFront() {
        if (isEmpty()) {
            return -1;
        }
        return arr[front];
    }

    /** Get the last item from the deque. */
    public int getRear() {
        if (isEmpty()) {
            return -1;
        }
        return arr[(rear - 1 + capacity) % capacity];
    }

    /** Checks whether the circular deque is empty or not. */
    public boolean isEmpty() {
        return front == rear;
    }

    /** Checks whether the circular deque is full or not. */
    public boolean isFull() {
        return (rear + 1) % capacity == front;
    }
}

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque obj = new MyCircularDeque(k);
 * boolean param_1 = obj.insertFront(value);
 * boolean param_2 = obj.insertLast(value);
 * boolean param_3 = obj.deleteFront();
 * boolean param_4 = obj.deleteLast();
 * int param_5 = obj.getFront();
 * int param_6 = obj.getRear();
 * boolean param_7 = obj.isEmpty();
 * boolean param_8 = obj.isFull();
 */
//leetcode submit region end(Prohibit modification and deletion)
```



### 困难：

#### 1、[接雨水](https://leetcode.com/problems/trapping-rain-water/)（亚马逊、字节跳动、高盛集团、Facebook 在半年内面试常考）