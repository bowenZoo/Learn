#排序算法

##冒泡排序
冒泡排序，简单的排序算法，重复遍历要排序的数列，一次比较两个元素，顺序错误就交换。遍历到没有需要再交换为止。
1.思路：
    *   按照（升序/降序）规则比较两个相邻的元素，满足条件就交换它们。
    *   对所有相邻元素做同样的工作，从开始比较到结尾，然后重新开始再重复上面步骤。
    *   重复次数越来越少，直到没有需要比对的数字后结束。
2.实现：
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
##快速排序
通过排序将要排序的数据分割成独立的两部分，其中一部分的所有数据逗比另外一部分的小，然后按此方法对两部分数据分别再进行快速排序，整个排序过程递归进行，一次达到整个数据变成有序序列。
1.思路:
    *   从数列中跳出一个元素，为基准值。
    *   重新排列数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆放在后面，相同的数随便任意一边。分区结束后，该基准就处于数列的中间，这个就是分区操作。
    *   递归调用分区的数列，递归的最底部是数列的长度小于等于1。
2.实现：
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
        this.sort(list, begin, left - 1); // 递归调用
        this.sort(list, left + 1, end);
    }
```

[时间/空间复杂度相关概念](http://blog.csdn.net/zolalad/article/details/11848739)