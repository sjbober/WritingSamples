# Quicksort

Quicksort works by picking an element at random which will act as the **pivot**. The goal is to **partition** the array, which means that all elements less than the pivot are moved to the left side of the array, and all elements greater than the pivot are moved to the right side of the array. When the iteration is over, the elements on either side of the pivot will not necessarily be sorted, but the pivot will be in the correct position. Once the array is partitioned, the algorithm uses either side of the partition to create subarrays, which it recursively partitions and divides further until the subarrays contain only one element, which is already sorted. At this point, the entire array has been sorted (Shaffer, 2011, ch. 7.5).

To really understand how the partition process of quicksort works, it might be best to visualize what is happening with an example. Let's say we want to sort the following array:

![Array to be sorted](/images/qs1.png)

We pick the pivot at random, and for this example we will move the pivot to the beginning of the array. Then, we have pointers point to the first element (not including the pivot) and last element in the array.

![Move pivot to beginning and set pointers](/images/qs2.png)

The first thing we do is traverse the "low" pointer over the list until it finds an element that is greater than the pivot. We know this needs to be moved to the right side of the partition, but where exactly does the right side start? We don't actually know yet, because we don't know exactly how many elements will end up on the right and left side of the pivot. And, we won't know this until we finish partitioning! So, what do we do? Well, we don't want to move the element to the far right side, as this will be a costly operation to shift all elements before it over one. We also don't want to arbitrarily swap the element with one on the far right side (or vice versa), because we don't want to accidentally swap with an element that is already on the correct side of the partition. So, we iterate the "high" pointer until it points to an element that is less than the pivot. Now we have two elements that are on opposite wrong sides of the partition.

![Low pointer finds element greater than pivot and High pointer finds greater than](/images/qs3.png)

Once we have this, we can swap these elements, knowing that in doing so we move them both to their correct sides of the partition.

![Swap high and low](/images/qs4.png)

We keep traversing the low and high pointers, looking for elements that we can swap. When the low and high pointers point to the same element, we have finished partitioning the array.

![High and Low meet](/images/qs5.png)

Now, we just traverse the high pointer once more, and then swap its element with that of the pivot.

![Traverse high once more](/images/qs6.png)

Now, the pivot is in its correct location in the array, with all the elements less than it on its left side, and all elements greater than it on its right side.

![Pivot is in correct position](/images/qs7.png)

Once an iteration is complete, the algorithm will continue to recursively divide each array/subarray and partition them.

The pivot is extremely important to the time efficiency of quicksort. Like I mentioned before, when we pick a pivot, we don't know how many elements come before or after it until we have already partitioned the array. However, in the best case, we want to pick a pivot that exactly divides the array into two equal pieces. That way, the array is halved each time we divide the array. This ensures that we only need to make approximately log n recursive calls. Since each iteration requires approximately n traversals until the low and high pointers meet, this means that the algorithm is O (n log n) in the best case (Shaffer, 2011, ch. 7.5). 

In the worst case however, we pick a pivot that is the lowest or highest element in the array or subarray. As a result, we have to partition a subarray of one element and a subarray of n-1, n-2,... etc. This means we are making roughly n recursive calls, which leads to a performance of O(n^2). To avoid this, the easiest solution is to randomly pick an element or pick the element in the middle of the array to be the pivot. This won't guarantee we pick a good pivot, but it will give us a good chance especially if the array happens to be sorted or mostly sorted already (Shaffer, 2011, ch. 7.5). 

## References

Shaffer, C. (2011). A Practical Introduction to Data Structures and Algorithm Analysis. Blacksburg: Virginia Tech.

Quicksort partition animation by Y. Daniel Liang. (n.d.). Retrieved from [https://www.cs.armstrong.edu/liang/animation/web/QuickSortPartition.html](https://www.cs.armstrong.edu/liang/animation/web/QuickSortPartition.html)