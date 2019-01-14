 1. 数组方法

```JavaScript
let arr=[1,2,3]

arr.push(4)		//push:在数组尾部添加元素 arr=[1,2,3,4];

arr.unshift(0) 		//unshift:在数组头部添加元素 arr=[0,1,2,3,4];

arr.shift() 		//shift:删除数组的第一个元素 arr=[1,2,3,4];

arr.pop()	        //pop:删除数组最后一个元素 arr=[1,2,3];

arr.reverse()		//reverse:数组翻转 arr=[3,2,1];

arr.join(',') 		//join:数组转化为字符串 arr="3,2,1";

arr.slice(0,1)		//slice(start,end):截取数组，从开始start到结束end（不包含）
			//返回的是新数组，原来的数组是不变的，arr=[3,2,1];

let b=[7,8,9]
arr.concat(b)		//concat:数组合并 [1,2,3,7,8,9];

arr.splice()		//splice(开始下标，个数，a1,a2......):剪接数组
			//  一个参数：从参数的位置开始截取，arr.splice(1) arr=[2,3];
			// 	参数为负数，类似slice arr.splice(-1) arr=[3];
			//  二个参数：(开始位置，个数)  
			// 		let arr=[1,2,3,4,5,6,7]
			// 		arr.splice(1,3) arr=[2,3,4];
			//  三个参数添加：arr.splice(1,0,8)  arr=[1,8,5,6,7];
			//  四个参数替换：arr.splice(1,2,9,0)  arr=[1,9,0,6,7];
			
arr.sort() 		//sort:数组排序	arr=[0,1,6,7,9);

arr.indexOf() 		//indexOf:从开始查找索引，两个参数：要查找的项和开头索引所在的位置；

arr.lastIndexOf() 	//lastIndexOf:从结尾部分开始查找索引；

arr.every()		//运行函数，只有每一项都返回true，结果才返回true；
arr.some()		//有一项为true，结果就返回true;
arr.filter() 		//返回满足条件的数组
			// let numArr=[1,2,3,4,9,7,8]
			// function checkNum(num){
			// 				return num>=5
			// }
			// console.log(numArr.every(checkNum))  //false
			// console.log(numArr.some(checkNum))  //true
			// console.log(numArr.filter(checkNum))  // [9,7,8]
					
arr.forEach() 		//数组遍历，没有返回值return；

arr.map()		//返回每次函数调用的结果组成的数组；

arr.reduce()或reduceRight()  //缩小数组的方法，迭代数组的所有项，返回新的数组；
				// let sum=arr.reduce(function(a,b){
				// 		return a+b
				// })
				// console.log(sum)  //最终成为一个累加值34（1+2+3+4+9+7+8=34）
	
				// let arr = [ [0, 1],  [2, 3],  [4, 5]];
				// let newArr=arr.reduceRight((a, b) => {
				//     return a.concat(b);
				// }, []);
				//数组的每个值（从右到左）将其减少为单个值
				// console.log(newArr)  [4, 5, 2, 3, 0, 1] 		
		
```

 2. 字符串方法
 3. 日期方法


  未完待续...
