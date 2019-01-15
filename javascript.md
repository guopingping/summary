 1. 数组方法

```JavaScript
let arr=[1,2,3]

arr.push(4)		 	//push:在数组尾部添加元素 arr=[1,2,3,4];

arr.unshift(0) 		//unshift:在数组头部添加元素 arr=[0,1,2,3,4];

arr.shift() 		 //shift:删除数组的第一个元素	 arr=[1,2,3,4];

arr.pop()			 //pop:删除数组最后一个元素 arr=[1,2,3];

arr.reverse()		 //reverse:数组翻转 arr=[3,2,1];

arr.join(',') 		//join:数组转化为字符串 arr="3,2,1";

arr.slice(0,1)		 //slice(start,end):截取数组，从开始start到结束end（不包含）
			        //返回的是新数组，原来的数组是不变的，arr=[3,2,1];

let b=[7,8,9]
arr.concat(b)		 //concat:数组合并 [1,2,3,7,8,9];

arr.splice()		//splice(开始下标，个数，a1,a2......):剪接数组
				  	//  一个参数：从参数的位置开始截取，arr.splice(1) arr=[2,3];
					// 		 参数为负数，类似slice arr.splice(-1) arr=[3];
				  	//  二个参数：(开始位置，个数)  
				   	// 				let arr=[1,2,3,4,5,6,7]
				   	// 				arr.splice(1,3) arr=[2,3,4];
				   	//  三个参数添加：arr.splice(1,0,8)  arr=[1,8,5,6,7];
				    //  四个参数替换：arr.splice(1,2,9,0)  arr=[1,9,0,6,7];
			
arr.sort() 			//sort:数组排序	arr=[0,1,6,7,9);

arr.indexOf() 	//indexOf:从开始查找索引，两个参数：要查找的项和开头索引所在的位置；

arr.lastIndexOf() 	//lastIndexOf:从结尾部分开始查找索引；

arr.every()		    //运行函数，只有每一项都返回true，结果才返回true；
arr.some()		    //有一项为true，结果就返回true;
arr.filter() 		//返回满足条件的数组
						// let numArr=[1,2,3,4,9,7,8]
						// function checkNum(num){
						// 				return num>=5
						// }
						// console.log(numArr.every(checkNum))  //false
						// console.log(numArr.some(checkNum))  //true
						// console.log(numArr.filter(checkNum))  // [9,7,8]
					
arr.forEach() 		//数组遍历，没有返回值return；

arr.map()		  //返回每次函数调用的结果组成的数组；

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

 ```javascript
 let str="abcdefg"
str.substring(1)			//bcdefg 
							//substring(start,end):不包含结束位置  str.substring(1,4)= bcd;

str.slice()      			 //slice():和substring类似

// slice和substring的区别：
	// 	输入参数为负数的时候,
	// 	substring将负值变为0，小的作为开始位置
	// 		str.substring(-1,1)=str.substring(0,1)=a
	// 	slice输入负值的时候，将值与字符串长度相加,若绝对值大于字符串长度，则取0
	// 		str.slice(1,-3)=str.slice(1,4)=bcd
	// 		str.slice(-9)=str.slice(0)=abcdefg

str.substr(1，2)				//substr(start,end):start开始位置，end需要返回的字符串的个数；ab
								//substr(1) abcdefg
								//输入负值，值与字符串长度相加，end为负值时，值为0；
					
str.charAt(1)					//charAt(index):返回指定索引处的字符.b 
								//超出有效范围，返回空；

str.indexOf('a')				//indexOf(String):返回string对象内，第一次出现子字符串的位置. 0
								//如果没有出现，返回-1；
				
str.lastIndexOf()				//倒序查找

let str="abcadaef"
str.split('a')					//split():将字符串以参数分隔为数组。["", "bc", "d", "ef"];

str.toLowerCase()				//转换为小写；
str.toUpperCase()				//转换为大写；"ABCADAEF"

let a="xyz"
let b="abc"
a.concat(b)						//concat():连接字符串。xyzabc；


```

 3.常见的日期方法

```JavaScript
 -1） Moment.js
 	moment官网有很多比较简洁和实用的写法可供参考。(http://momentjs.cn)
 	不过需要首先安装moment插件
 		npm install moment
 	引用
 		import moment from "moment"
 
 
 - 2）Date
 	date官网也有很多原始的方法可以获取想要的日期。（https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date）
 	
 	
 -3） JavaScript
 	/**********获取两个时间间隔的月份 *****************/
 	function getDate(start,end){
	 	var result = [];
	    var s = start.split("-");
	    var e = end.split("-");
	    var min = new Date();
	    var max = new Date();
	    min.setFullYear(s[0], s[1]);
	    max.setFullYear(e[0], e[1]);
	    var curr = min;
	    while (curr <= max) {
	        var month = curr.getMonth();
	        if (month > 0 && month <= 9) { month = "0" + month }
	        var str = curr.getFullYear() + "-" + (month);
	        var s = curr.getFullYear() + "-0";
	        if (str == s) {
	            str = curr.getFullYear() + "-12";
	        }
	        result.push(str);
	        curr.setMonth(curr.getMonth() + 1);
	    }
    	return result
    }

	/**************获取两个日期间的所有日期,默认start<end ***************/
	Date.prototype.format = function() {
	    var s = '';
	    var mouth = (this.getMonth() + 1) >= 10 ? (this.getMonth() + 1) : ('0' + (this.getMonth() + 1));
	    var day = this.getDate() >= 10 ? this.getDate() : ('0' + this.getDate());
	    s += this.getFullYear() + '-'; // 获取年份。
	    s += mouth + "-"; // 获取月份。
	    s += day; // 获取日。
	    return (s); // 返回日期。
	};
	function getDiffDate(begin, end) {
	    var result = []
	    var ab = begin.split("-");
	    var ae = end.split("-");
	    var db = new Date();
	    db.setUTCFullYear(ab[0], ab[1] - 1, ab[2]);
	    var de = new Date();
	    de.setUTCFullYear(ae[0], ae[1] - 1, ae[2]);
	    var unixDb = db.getTime();
	    var unixDe = de.getTime();
	    for (var k = unixDb; k <= unixDe;) {
	        result.push(
	            new Date(parseInt(k)).format());
	        k = k + 24 * 60 * 60 * 1000;
	    }
	    return result
	}
	
	/**************格式化日期******************/
	function getFormatDate(date, fmt) { 
	    var o = {
	        "M+": date.getMonth() + 1, //月份 
	        "d+": date.getDate(), //日 
	        "h+": date.getHours(), //小时 
	        "m+": date.getMinutes(), //分 
	        "s+": date.getSeconds(), //秒 
	        "q+": Math.floor((date.getMonth() + 3) / 3), //季度 
	        "S": date.getMilliseconds() //毫秒 
	    };
	    if (/(y+)/.test(fmt))
	     	fmt = fmt.replace(RegExp.$1, (date.getFullYear() + "").substr(4 - RegExp.$1.length));
	    for (var k in o)
	        if (new RegExp("(" + k + ")").test(fmt)) 
	        	fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
	    return fmt;
	}
	
	/***************比较时间*********************/
	 function compareTime(date1, date2) {
	    var start_time = date1.replace(new RegExp("-", "gm"), "/");
	    var end_time = date2.replace(new RegExp("-", "gm"), "/");
	    var starttime = (new Date(start_time)).getTime(); //得到毫秒数
	    var endtime = (new Date(end_time)).getTime(); //得到毫秒数
	    return (starttime < endtime) ? true : false;
	}

```

4.常见的正则校验

```JavaScript
//处理特殊字符  正则校验
//只能输入汉字
let reg = "^[\u4e00-\u9fa5]{0,}$";

//url校验
let reg = "^http://([\w-]+\.)+[\w-]+(/[\w-./?%&=]*)?$";

//tel校验
let reg  = "^(\d{3,4}-)\d{7,8}$";

//匹配首尾空格
let reg = "(^\s*)|(\s*$)";

//去除两边的空格
function deleteTrims(ctx) {
    return ctx.replace(/(^\s*)|(\s*$)/g, "");
}

//按照固定位数，从左边不足补0
function PadLeft(str, len, c) {
    while (str.length < len) {
        str = c + str;
    }
    return str;
}

//删除前面为0的字符窜
function deleteLeft (str, c) {
        var num;
        for (var s = 0; s < str.length; s++) {
           if (str.charAt(s) !== c) {
               num = str.substr(s);
               break;
         }
      }
 	return num
 }
 
//特殊字符窜（验证是否含有^%&',;=?$"等字符）
let reg  = "[^%&',;=?$]+";

//匹配首尾空白字符(可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)
let reg = "^\s*|\s*$";

```




  未完待续...
