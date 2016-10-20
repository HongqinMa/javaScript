#sum.common.js
- 冒泡排序
- 事件相关
- 随机数相关（一个随机数、随机数组、随机颜色）
- 





#1. 冒泡排序
>
	MHQ.sortArr = function (arr) {
	    for (var i = 0; i < arr.length - 1; i++) {
	        var flag = true;
	        for (var j = 0; j < arr.length - 1 - i; j++) {
	            if (arr[j] > arr[j + 1]) {
	                var tempValue = arr[j + 1];
	                arr[j + 1] = arr[j];
	                arr[j] = tempValue;
	                flag = false;
	            }
	        }
	        if (flag) {
	            break;
	        }
	    }
	    return arr;
	};



#2. 得到诸如[{attr1:2,attr2:3}, {attr1:1,attr2:2}]数组中各对象的attr1属性中最大的一个（一个在特殊场合用的方法）
>**用到apply方法、ES5的map方法（☆☆☆☆）**
> 
	/**
	 * @param arr [{attr1:2,attr2:3}, {attr1:1,attr2:2}]
	 */
	MHQ.getObjArrMax = function (arr) {
	    Math.max.apply(null, arr.map(function (v) {
	        return v.attr1;
	    }));
	};



#3. 给一个元素同时多个事件
>
	/**
	 * 给一个元素同时多个事件
	 * @param element 需要绑定事件的元素 Dom Object
	 * @param eventNameStr 需要绑定的事件类型名称 string
	 * @param fn 回调函数 function
	 */
	MHQ.addEvent = function (element, eventNameStr, fn) {
	    var oldEvent = element["on" + eventNameStr];
	    if (oldEvent == null) {//表示该事件没有处理函数
	        element["on" + eventNameStr] = fn;//注册事件了
	    } else {
	        //有事件了---先调用原来的事件,再重新注册新的事件
	        element["on" + eventNameStr] = function () {
	            //调用原来的事件-注册新的事件
	            oldEvent();
	            fn();
	        };
	    }
	};


#4. 获取随机数数组（使用了闭包，防止变量污染）
>
	/**
	 * 获取n个随机数的数组 object.getRandomArr 得到随机数的数组
	 * @param count 需要得到的随机数组中随机数的个数
	 * @param min 随机数的最小值
	 * @param max 随机数的最大值
	 * @returns {{getRandomArr: getRandomArr}}
	 */
	MHQ.getRandomObj = function (count, min, max) {
	    var arr = [];
	    return {
	        getRandomArr: function () {
	            while (arr.length < count) {
	                var num = MHQ.getRandom(min, max);
	                if (arr.indexOf(num) === -1) {
	                    arr.push(num);
	                }
	            }
	            return arr;
	        }
	    }
	};

#5. 获取一个随机整数 Math.random(); 中的参数可以是一个，考虑了参数是一个的情况
>
	/**
	 * OBJECT 获取n个随机数 最终得到数组  object.getRandomArr 得到随机数的数组
	 * 说明：因为要传递参数，所以不能用立即执行函数
	 * @type {{getRandomArr}}
	 */
	MHQ.getRandomObj = (function () {
	    var arr = [];
	    return {
	        /**
	         * 
	         * @param count 需要得到的随机数组中随机数的个数
	         * @param min 随机数的最小值
	         * @param max 随机数的最大值
	         * @returns {Array}
	         */
	        getRandomArr: function (count, min, max) {
	            while (arr.length < count) {
	                var num = MHQ.getRandom(min, max);
	                if (arr.indexOf(num) === -1) {
	                    arr.push(num);
	                }
	            }
	            return arr;
	        }
	    }
	})();
# 6. 随机的颜色
>
	/**
	 * METHOD 获取随机的颜色数组
	 * @param count 需要获取的颜色数目
	 * @returns {Array}
	 */
	MHQ.getColor = function (count) {
	    var colorSingle;
	    var colorArr = [];
	    var color = "#";
	    for (var i = 0; i < count; i++) {
	        for (var j = 0; j < 6; j++) {
	            var colorRandom = MHQ.getRandom(16);
	            switch (colorRandom) {
	                case 10:
	                    colorSingle = "A";
	                    break;
	                case 11:
	                    colorSingle = "B";
	                    break;
	                case 12:
	                    colorSingle = "C";
	                    break;
	                case 13:
	                    colorSingle = "D";
	                    break;
	                case 14:
	                    colorSingle = "E";
	                    break;
	                case 15:
	                    colorSingle = "F";
	                    break;
	                default:
	                    colorSingle = colorRandom;
	            }
	            color += colorSingle;
	        }
	        colorArr.push(color);
	        color = "#";
	    }
	    return colorArr;
	};






























































