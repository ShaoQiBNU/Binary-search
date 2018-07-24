二分查找
=======

# 一. 问题描述

> 有一个排过序的数组，包含n个整数，但是这个数组向左进行了一定长度的移位，例如，原数组为[1,2,3,4,5,6]，向左移位5个位置即变成了[6,1,2,3,4,5],现在对于移位后的数组，需要查找某个元素的位置。请设计一个复杂度为log级别的算法完成这个任务。给定一个int数组A，为移位后的数组，同时给定数组大小n和需要查找的元素的值x，请返回x的位置(位置从零开始)。保证数组中元素互异。测试样例：[6,1,2,3,4,5],6,6，返回：0。

# 二. 求解

> 二分查找的加强版，主题思路还是二分，再加上一些限制条件。代码如下：

```java
import java.util.*;

public class Finder {
    public static void main(String []args){
        int[] A={6,1,2,3,4,5};
        int n=6;
        int x=6;

        int res=findElement(A,n,x);
        System.out.println(res);
    }
    public static int findElement(int[] A, int n, int x) {
        int left=0;
        int right=n-1;
        int mid;
        
        while(left<=right){

            mid=(left+right)/2;

            if(A[mid]==x)
                return mid;

            if(A[mid]<x) {

            //A[mid]<A[left] 说明右边是有序的，且x>A[right]说明x在mid左边
                if(A[mid]<A[left]&& x>A[right]) right=mid-1;
                else left=mid+1;
            }

            else {

                //A[mid]>A[left]说明左边是有序的，且x<A[left]，说明x在mid右边
                if(A[mid]>A[left]&&x<A[left]) left=mid+1;
                else right=mid-1;
            }
        }
        return -1;
     }
}
```
