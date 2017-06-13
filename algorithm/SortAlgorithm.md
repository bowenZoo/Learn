# 排序算法

## 冒泡排序
冒泡排序，简单的排序算法，重复遍历要排序的数列，一次比较两个元素，顺序错误就交换。遍历到没有需要再交换为止。
1. 思路：
    *   按照（升序/降序）规则比较两个相邻的元素，满足条件就交换它们。
    *   对所有相邻元素做同样的工作，从开始比较到结尾，然后重新开始再重复上面步骤。
    *   重复次数越来越少，直到没有需要比对的数字后结束。
2. 实现：

javascript:
```
    function sort(list)
    {
        var len = list.length;
        for(var i = 0; i < len-1; i++)
            for(var j = 0; j < len-i; j++)
            {
                if(list[j] > list[j+1])//升序
                {
                    var temp = list[j];
                    list[j] = list[j+1];
                    list[j+1] = temp;
                }
            }
    }
```

## 选择排序
和冒泡差不多的排序方法，区别在于冒泡一直换，而选择每次遍历只换一次。
1. 思路：
    *   首先遍历一遍数组找到最大/小的值，存放在起始/结尾位置。
    *   再在数组剩余的值里，找到最大/小的值，放到数组剩余值的起始/结尾位置。
    *   以此类推，数组排列完毕。
2. 实现：

javascript:
```
    function sort(list)
    {
        var len = list.length;
        for(var i = 0; i < len - 1; i++)
        {
            var min = i; 
            for(var j = i + 1; j < list.length; j++)
            {
                if(list[min] > list[j])
                    min = j;
            }
            var temp = list[min];
            list[min] = list[i];
            list[i] = temp;
        }
    }
```

## 插入排序
构建有序数组，从后向前比对插入。
1. 思路：
    *   构建有序数组，然后对未排序的值从后向前进行比对插入。
2. 实现：

javascript:
```
    function sort(list)
    {
        var len = list.length;
        for (var i = 1; i < len; i++)
        {
            if (list[i - 1] > list[i])
            {
                var temp = list[i];
                var j = i;
                while (j > 0 && list[j - 1] > temp)
                {
                    list[j] = list[j - 1];
                    j--;
                }
                list[j] = temp;
            }
        }
    }
```

## 希尔排序
插入排序的改进版，会优先比较较远的元素。核心在于间隔数列的设定。增量序列特征：最后一个增量必须为1，尽量避免序列中的值互为倍数。- -0这样就麻烦了，还是gap = length / 2吧。
1. 思路:
    *   根据增量序列划分数组，对每个数组进行排序。
    *   直到增量序列为1时，插入排序一波，就完成了。
2. 实现：

javascript:
```
    function sort(list, len)
    {
        var gap = len /2;
        while(gap > 0)
        {
            for (var i = 0; i < gap; i++)
            {
                //插入排序
                for (var j = i + gap; j < len; j += gap)
                {
                    if (list[j - gap] > list[j])
                    {
                        var temp = list[j];
                        var k = j;
                        while (k > 0 && list[k - gap] > temp)
                        {
                            list[k] = list[k - gap];
                            k -= gap;
                        }
                        list[k] = temp;
                    }
                }
            }
            gap = parseInt(gap / 2);
        }
    }
```

## 快速排序
通过排序将要排序的数据分割成独立的两部分，其中一部分的所有数据逗比另外一部分的小，然后按此方法对两部分数据分别再进行快速排序，整个排序过程递归进行，一次达到整个数据变成有序序列。
1. 思路:
    *   从数列中跳出一个元素，为基准值。
    *   重新排列数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆放在后面，相同的数随便任意一边。分区结束后，该基准就处于数列的中间，这个就是分区操作。
    *   递归调用分区的数列，递归的最底部是数列的长度小于等于1。
2. 实现：

javascript:
```
    
    function sort(list, begin, end)
    {
        if(begin >  end)return;
        var left = begin;
        var right = end;
        var pivot = list[begin];
        while (left < right)  
        {
            while(left < right && list[right] > pivot)right--;
            list[left] = list[right];
            while(left < right && list[left] < pivot)left++;
            list[right] = list[left];
        }
        list[left] = pivot;
        this.sort(list, begin, left - 1);
        this.sort(list, left + 1, end);
    }
```

## 归并排序
归并排序不受输入数据影响，和选择排序时间复杂度相同，但是内存消耗多。
将已有序的自序列合并，得到完全有序的序列；即先使每个字序列有序，再使子序列段间有序

## 堆排序




## 计数排序

## 桶排序

## 基数排序


[时间/空间复杂度相关概念](http://blog.csdn.net/zolalad/article/details/11848739)