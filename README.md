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
2. 冒泡排序算法

思路：设排序序列的记录个数为n，进行n-1次遍历，每次遍历从开始位置依次往后比较前后相邻元素，这样较大的元素往后移，n-1次遍历结束后，序列有序。
```
//冒泡排序算法
function sortByBubble(data){
	var flag = true;
	for(var i = 0;i < data.length-1 && flag;i++){
		flag = false;
		for(var j=0;j<data.length-1-i;j++){
			if(data[j]>data[j+1]){
				var temp = data[j];
				data[j] = data[j+1];
				data[j+1] = temp;
				flag = true;
			}
		}

	}
	console.log(data);
}
sortByBubble([5,4,2,4,1,4,6]);

```
3. 简单选择排序算法

思路：设排序序列的记录个数为n，进行n-1次选择，每次在n-i+1(i = 1,2,...,n-1)个记录中选择关键字最小的记录作为有效序列中的第i个记录。
```
function sortBySelect(data){
	for(var i=0;i<data.length-1;i++){
		var minIndex = i;
		for(var j=i+1;j<data.length;j++)
		{
			if(data[j]<data[minIndex]){
				minIndex = j;
			}
		}
		if(minIndex!=i){
			var temp = data[minIndex];
			data[minIndex] = data[i];
			data[i] = temp;
		}
	}
	console.log(data);
}
// sortBySelect([1,3,6,2,4,5]);
```
4. 插入排序

思路：是将一个记录插入到已排好序的有序表中，从而得到一个新的、记录数增1的有序表。
```
//插入排序
function sortByInsert(data){
	var j;
	for(var i=1;i<data.length;i++){
		var temp = data[i];
		j = i-1;
		while(j>-1&&temp<data[j]){
			data[j+1] = data[j];
			j--;
		}
		data[j+1] = temp;
	}

	console.log(data);
}
sortByInsert([1,2,3,6,4,2,5])
```
5. 希尔排序

思路：把记录按下标的一定增量分组，比如两组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至1时，整个文件恰被分成一组，算法便终止
```
//希尔排序
function sortByXier(data){
var len = data.length;
for(var n = Math.floor(len/2);n>0;n = Math.floor(n/2)){
	for(var i = n;i<len;i++){
		for(j=i-n;j>=0&&data[j]>data[n+j];j-=n){
			var temp = data[j];
			data[j] = data[n+j];
			data[n+j] = temp;
		}
	}
   }
   console.log(data);
}
sortByXier([49,38,65,97,76,13,27,49,55,04]);
```
6. 归并排序

思路：将待排序序列分为两部分，对每部分递归地应用归并排序，在两部分都排好序后进行合并。
```
//归并排序
function sortByMerge(data){
	if(data.length>1){
		var mid = Math.floor(data.length/2);
		for(var data1=[],i=0;i<mid;i++){
			data1.push(data[i]);
		}
		for(var data2=[],i=mid;i<data.length;i++){
			data2.push(data[i]);
		}
		return merge(sortByMerge(data1),sortByMerge(data2));

	}else{
		return data;
	}
}

function merge(arr1,arr2){
	var result = [],count1=0,count2=0,count3=0;
	while(count1<arr1.length&&count2<arr2.length){
		if(arr1[count1]<arr2[count2]){
			result.push(arr1[count1++]);
		}else{
			result.push(arr2[count2++]);
		}

	}
	while(count1<arr1.length){
		result.push(arr1[count1++]);
	}
	while(count2<arr2.length){
		result.push(arr2[count2++]);
	}
	return result;
}

console.log(sortByMerge([1,5,4,2,9,8]));


```
7. 快速排序

思路：在待排序的序列中选择一个称为主元的元素，将数组分为两部分，使得第一部分中的所有元素都小于或等于主元，而第二部分中的所有元素都大于主元，然后对两部分递归地应用快速排序算法
```
function sortByQuick(arr){
    //如果数组<=1,则直接返回
    if(arr.length<=1){return arr;}
    var pivotIndex=Math.floor(arr.length/2);
    //找基准，并把基准从原数组删除
    var pivot=arr.splice(pivotIndex,1)[0];
    //定义左右数组
    var left=[];
    var right=[];

    //比基准小的放在left，比基准大的放在right
    for(var i=0;i<arr.length;i++){
	if(arr[i]<=pivot){
	    left.push(arr[i]);
	}
	else{
	    right.push(arr[i]);
	}
    }
    //递归
    return quickSort(left).concat([pivot],quickSort(right));
}           
```
