# suanfa
js实现一些常见算法

1. 二分法查找算法

   思路：将n个元素分成大致相等的两部分，取a[n/2]与x做比较，如果x=a[n/2],则找到x，算法中止；如果x<a[n/2]，则只要在数组a的左半部分继续搜索x，如果x>a[n/2]，则只要在数组a的右半部搜索x。二分查找的时间复杂度为O(logn)。实现：

```
//二分法查找有序数组算法	 
function findByTwoWay(data,value){

	var low = 0;
	var high = data.length-1;
	while(low<=high){
		var mid = parseInt((low+high)/2);	 			
		if(value==data[mid]){
			return mid;
		}else if(value<data[mid]){
			high = mid-1;
		}else{
			low = mid+1;
		}
	}
	return -1;
}
console.log(findByTwoWay([1,2,3,4,5,6],3));
```
