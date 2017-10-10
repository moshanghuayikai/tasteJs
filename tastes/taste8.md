## JavaScript-流程控制

JavaScript是单线程的，一个语句一个语句的执行。语句是执行过程中的流程、限定与约定，形式上可以是单行语句，或者由一对大括号"{}"括起来的复合语句，复合语句整体可以作为一个单行语句处理。那么，代码中，流程控制就显得格外重要了。JavaScript也规定了一些语句和一些关键字用于流程控制。

## if语句

### if (条件表达式) {语句}

    if(2 > 1){
    	console.log('xzavier win');
    }
    
javascript会判断括号里的条件表达式的值。如果值为truthy类型的值，也就是真，则执行后面的一条语句，否则不执行。这个语句无可厚非，使用率也是极高的，有时候会使用短连接来替代：

    2 > 1 && console.log('xzavier win');

想了解此运算符以及更多运算符参考： [运算符详解][1]

关于判断参见本系列文章：[代码中的那些判断][2]

### if (条件表达式) {语句;} else {语句;}

if为真值（Boolean转换），则执行if里的代码，否则执行else里的代码。

    if (2 > 1) {
    	console.log('xzavier win'); 
    } else {
    	console.log('xzavier fail'); 
    }

这个语句的使用也无需多说，有时候会使用三目运算符代替：

    2 > 3 ? console.log('xzavier win') : console.log('xzavier fail');

有时候设计到赋值的if...else，也可以使用短连接。同参考上面一篇文章。

### if (条件表达式) {语句;} else if (条件表达式) {语句;} ... else {语句;}

    if (1 > 2) {
    	console.log('xzavier win'); 
    } else if(3 > 2){
    	console.log('xzavier win2'); 
    } else {
    	console.log('xzavier fail'); 
    }

JavaScript其实是没有else if的，else if算是一种封装。看这里的js判断：

    var a = 3, b = 2;
    a > b // true
    a > b // false
    a = b // false

额(⊙o⊙)…这不是在逗我吗？不，我只是用最简单的判断说一下js的判断：

    a >= b // true  
    //其实它是先判断了 a < b 为false 再用“非正即反” 来返回 a >= b 的值

不信？看这个：

    var a = {};  // 你可以添加任意属性 {x:3};
    var b = {};  // 你可以添加任意属性 {z:2};;
    a < b;    // false
    a == b;   // false
    a > b;    // false

对象的比较，可以参见本系列判断相关的文章。

看上面没问题是吧，但是用 >= 就不一样了：

    a <= b;    // true
    a >= b;    // true

我...所以，也根据语言规范，先对 <= 的另一面求值，再“非正即反”。

那么回到else if呢，上面的代码其实最终是这样的：

    if (1 > 2) {
    	console.log('xzavier win'); 
    } else {
    	 if(3 > 2){
    		console.log('xzavier win2'); 
    	} else {
    		console.log('xzavier fail'); 
    	}
    }

把它拆分为多个if...else... 这只是个探究，因为else if司空见惯，代码又少，语义很好，所以使用得多。
所以，尽情的使用吧，我的意思是别避开写else...if...，不是写一大堆else...if...，如果有一堆else...if...，那还是用下面的switch吧

## switch语句

switch 语句是多重条件判断，用于多个值相等的比较。

    var xzavier = 'boy';
    switch (xzavier) {
    	case 'girl' :
    		console.log('xzavier is a girl');
    		break;
    	case 'boy' :
    		console.log('xzavier is a boy');
    		break;
    	case 'man' :
    		console.log('xzavier is a man');
    		break;
    	default : 
    		console.log('time error');
    }

if和switch之间可以转换，当条件过多时，使用switch可以让代码更清晰，更好看。

这里说一下switch，它对括号里的语句求值一次，然后将返回值与每个case表达式进行匹配。
如果找到一个匹配，就会开始执行那个匹配的case里的代码，直到遇到一个break或者直到switch块末尾。
所以，写好`break`，很重要：

    var xzavier = 'boy';
    switch (xzavier) {
    	case 'girl' :
    		console.log('xzavier is a girl');
    		break;
    	case 'boy' :
    		console.log('xzavier is a boy');
    	case 'man' :
    		console.log('xzavier is a man');
    		break;
    	default : 
    		console.log('time error');
    }
    VM293:7 xzavier is a boy
    VM293:9 xzavier is a man

没有break掉，你的业务代码可能就出现bug.使用switch就需要好好的考虑业务场景，该break的地方切勿忘记。

另外，表达式的返回值和每一个case表达式之间的匹配判断使用的是全等运算符`===`：

    var xzavier = '1';
    switch (xzavier) {
    	case 1 :
    		console.log('xzavier is a girl');
    		break;
    	case 2 :
    		console.log('xzavier is a boy');
    	case 3 :
    		console.log('xzavier is a man');
    		break;
    	default : 
    		console.log('type error');
    }
    // type error

还有一点就是 `default` 非必需，位置也可以不固定。因为js总是先去匹配表达式的返回值和每一个case表达式，最终没有找到匹配的case，就会寻找default，找到了则执行default里的语句。没找到则执行到switch块末尾。

## do...while语句

do...while 语句是一种先运行，后判断的循环语句。也就是说，不管条件是否满足，至少先运行一次循环体。

    var xzavier = 1; 
    do {
    	console.log(xzavier);
    	xzavier++;
    } while (xzavier <= 10); 
    // 1 2 3 4 5 6 7 8 9 10
    
    var xzavier = 1; 
    do {
        console.log(xzavier);
        xzavier++;
    } while (xzavier <= 0);//先运行一次，再判断
    // 1
    
## while语句

while 语句是一种先判断，后运行的循环语句。

    var xzavier = 1; 
    while (xzavier <= 10) {  //先判断，再运行
    	console.log(xzavier);
    	xzavier++;
    }
    // 1 2 3 4 5 6 7 8 9 10
    
    var xzavier = 1; 
    while (xzavier <= 0) {  //先判断，再运行
    	console.log(xzavier); // 不会执行
    	xzavier++;
    } 
    
## for语句

for 语句也是一种先判断，后运行的循环语句。但它具有在执行循环之前初始变量和定义循环后要执行代码的能力。

    for (var i = 0; i <= 10 ; i++) { 
    	console.log(i); 
    } 

第1步: 声明变量var i = 1; 

第2步: 判断i <= 10

第3步: console.log(i);

第4步: i++

第5步: 重复2-5，直到判断为false

这里我们经常会遇到这样的写法：

    for (var i = 0; i <= data.length ; i++) {

建议先缓存data.length 为一个变量：

    for (var i = 0, l = data.length; i <= l ; i++) {

这样做的目的并不是一定能提升程序的性能，因为length属性是一个字典属性，读取它和读取变量的复杂度都为`O(1)`。

这样做主要是为了防止在for循环中改变了data.length，具体使用还应视具体代码而定。

当然，如果涉及到DOM，那么缓存变量就一定能提升代码性能了。

    for (var i = 0; i <= $('.item').length ; i++) {

每循环一次都`$('.item')` 就相对耗费性能了，与DOM有关的读取大多情况都应先用变量缓存，特殊业务视情况而定。

    var ietm_l = $('.item').length;
    for (var i = 0; i <= ietm_l ; i++) {

## for...in语句

for...in 语句可以用来枚举对象的属性。

    var xzavier = { 
    	'name' : 'xzavier', 
    	'age' : 23,
    	'job' : 'Jser',
    	'width' : 100,
    	'height' : 100,
    	'border' : 10
    };
    for (var i in xzavier) { 
    	console.log(i);
    }
    //name age job width height border
    for (var i in xzavier) { 
    	console.log(xzavier[i]);
    }
    //xzavier 23 Jser 100 100 10

for...in是为遍历对象属性设计的，但是它可以遍历数组，我去，因为数组也是对象啊。 不过，for...in 循环遍历的是对象的属性，而不是数组的索引。我们看一下打印的结果就知道了：
    
    var arr = [1,2,3];
    for(var i in arr) {
    	console.log(typeof(i));
    }
    // string string string

而经典的for语句遍历是数组的索引：

    var arr = [1,2,3];
    for(var i = 0; i < arr.length; i++) {
    	console.log(typeof(i));
    }
    // number number number

我们用for...in遍历数组时，取arr[i]时是我们期望得到的结果：

    var arr = [1,2,3];
    for(var i in arr) {
    	console.log(i + '--' + arr[i]);
    }
    // 0--1 1--2 2--3

但是：

    var arr = [1,2,3];
    arr.name = 'xzavier';
    for(var i in arr) {
    	console.log(i + '--' + arr[i]);
    }
    VM230:4 0--1
    VM230:4 1--2
    VM230:4 2--3
    VM230:4 name--xzavier

它访问了数组新增的 "name" 属性，因为 for-in 遍历了对象的所有属性。

甚至包括原型链上的所有可枚举的属性：

    var arr = [1,2,3];
    arr.name = 'xzavier';Array.prototype.oname = 'xzavier.chris'
	for(var i in arr) {
		console.log(i + '--' + arr[i]);
	}
    VM236:4 0--1
    VM236:4 1--2
    VM236:4 2--3
    VM236:4 name--xzavier
    VM236:4 oname--xzavier.chris

显然，我们习惯的数组遍历的结果是只有1,2,3 这样的结果的。

所以，综合来说：

for...in 循环遍历的是对象的属性，而不是数组的索引。正如例子，输出的索引值 "0"、 "1"、 "2"不是 Number 类型的，而是 String 类型的，因为是对象的属性都是string类型。

这样看来，for...in是不适合遍历数组的。确实，for...in本来就是为遍历对象属性设计的。

不过，在对于比较特殊的数组，for...in或许有用：

    var arr = Array(1000), count = 0;
    arr[100] = 100;
    arr[200] = 200;
    arr[300] = 300;
    for(var i in arr) {
    	count += 1;
    	console.log(i + '--' + arr[i]);
    }
    console.log(count);
    VM242:7 100--100
    VM242:7 200--200
    VM242:7 300--300
    VM242:9 3   // 只循环了3次额

而for循环：

    var arr = Array(1000), count = 0;
    arr[100] = 100;
    arr[200] = 200;
    arr[300] = 300;
    for(var i = 0; i < arr.length; i++) {
    	count += 1;
    	console.log(i + '--' + arr[i]);
    }
    console.log(count);
    // count 1000  循环了这么多次
    // 打印出100 200 300 和一堆的undefined

so :

for...in 只会遍历对象中存在的实体，而for 循环则会遍历 1000 次。如果你的业务刚好有这样的需要，那么合适的使用for..in遍历数组将会发挥更奇妙的作用。
但是一般来看，这样用到的机会很少，上面的指定索引是一种，另外你使用了delete去删除数组元素之后（非特殊，不要用delete去删除），也是可以这样遍历的：

    var arr = [1,2,3];
    delete arr[1]
    for(var i in arr) {
    	console.log(i + '--' + arr[i]);
    }
    VM246:4 0--1
    VM246:4 2--3

但是，一般情况谁允许你用delete去删除数组元素呢。关于数组可以参考我的另一篇对数组详解的文章。

## forEach循环

for...in是为遍历对象属性设计的，当然也可以遍历数组。后来，ES5也为素组设计了一个forEach方法来遍历。

forEach方法为数组中含有有效值的每一项执行一次 callback。callback有三个参数：

callback（数组当前项的值，数组当前项的索引，数组对象本身）

    var arr = [1,2,3,4,5,'xzavier',7];
    arr.forEach(function (value, index, arr) {
    	console.log(value);
    });
    // 1 2 3 4 5 xzavier 7

注意：

1.使用forEach循环的时候，需要注意，forEach 遍历的范围在第一次调用 callback 前就会确定。调用forEach 后添加到数组中的项不会被 callback 访问到。

在数组后面添加：

    var arr = [1,2,3,4,5,'xzavier',7];
    arr.forEach(function (value, index, arr) {
        if (value == 3) {
    	    arr.push(8);
    	}
    	console.log(value);
    });
    // 1 2 3 4 5 xzavier 7

在数组前面添加：

    var arr = [1,2,3,4,5,'xzavier',7];
    arr.forEach(function (value, index, arr) {
    	if (value == 3) {
    		arr.unshift(0);
    	}
    	console.log(index + '--' +value);
    });
    VM316:6 0--1
    VM316:6 1--2
    VM316:6 2--3
    VM316:6 3--3
    VM316:6 4--3
    VM316:6 5--3
    VM316:6 6--3

什么情况？因为你在数组前添加1项后，遍历下一项的值，发现值还是3，所以后面的遍历一直都走到if语句里了。
但是数组的遍历范围是不可变的。

2.如果已经存在的值被改变，则传递给 callback 的值是 forEach 遍历到他们那一刻的值。

    var arr = [1,2,3,4,5,'xzavier',7];
    arr.forEach(function (value, index, arr) {
    	arr[5] = 'xx';
    	console.log(value);
    });

3.已删除的项不会被遍历到（使用delete方法等情况，或者直接置为undefined）。

    var arr = [1,2,3,4,5,'xzavier',7];
    arr.forEach(function (value, index, arr) {
    	if (value == 3) {
    		delete arr[5];;
    	}
    	console.log(value);
    });
    // 1 2 3 4 5 7

但是使用别的方法删除就就会出错哦：

    var arr = [1,2,3,4,5,'xzavier',7];
    arr.forEach(function (value, index, arr) {
    	if (value == 3) {
    		arr.shift(0);
    	}
    	console.log(value);
    });
    // 1 2 3 5 xzavier 7   

第四个值不在了，因为forEach记住了最开始的length，但是shift却改变了length。其他的方法同理。

而delete并没有把数组项删掉，只是把值置为了undefined，所以length未变。

4.不能使用break或continue中断或跳出循环，报错。不过可以return false 跳出当前循环，达到一定效果：
    var arr = [1,2,3,4,5,'xzavier',7];
    arr.forEach(function (value, index, arr) {
    	if (value == 3) {
    		return false;
    	}
    	console.log(value);
    });
    // 1 2 4 5 xzavier 7

## for...of语句

for...in循环，只能获得对象的键名，不能直接获取键值，并且遍历数组不友好。

forEach中又不能使用break语句中断循环，也不能使用return语句返回到外层函数。

ES6提供for...of循环，允许遍历获得键值。如果要通过for...of循环，获取数组的索引，可以借助数组实例的entries方法和keys方法。它还可以正确响应break、continue和return语句。for-of 还可以遍历 Map 和 Set （ES6 中新增数据集合类型），以及其他可迭代对象。

    var arr = ['a', 'b', 'c', 'd'];   
    for (let i in arr) {
      	console.log(i); // 0 1 2 3
    }
    for (let i of arr) {
      	console.log(i); // a b c d
    }
    for (var i of arr) {
	    if(i == 'c'){
		    break;
	    }
  	    console.log(i); // a b
    }
    
    let str = 'xzavier';
    for (let i of str) {
          console.log(i); // x z a v i e r
    }
    
## break和continue语句

break 和continue 语句用于在循环中精确地控制代码的执行。其中，break 语句会立即退出循环，强制继续执行循环体后面的语句。而continue 语句退出当前循环，继续后面的循环。

    for (var i = 1; i <= 10; i++) {
    	if (i == 5) break; //如果i等于5，就退出循环
    	console.log(i); //1 2 3 4
    }
    for (var i = 1; i <= 10; i++) {
    	if (i == 5) continue; //如果i等于5，就退出当前循环
    	console.log(i); // 1 2 3 4 6 7 8 9 10
    }

## 标记跳转

我们程序员应该都知道有个字段叫：`goto`，可以让你的程序跳到指定的地方执行。由于goto遭到非议太多，使用这类编码形式会使你的代码难以理解和维护，基本不建议使用，如果JavaScript也有goto语句，那么在上面continue的基础上我们还可以让程序的执行跳转到指定的代码中的那个位置。不过，幸好，JavaScript没有这个标识，所以，我们的世界很欢畅。不过，你要是想这样做，我们还是有类似的实现的：

    xzavier: for (var i = 1; i <= 10; i++) {
    	if (i == 5) {
    		continue xzavier; // 一层循环，与continue无异
    	}
    	console.log(i);
    }
    // 1 2 3 4 6 7 8 9 10

在多层循环的时候作用就区别出来了：

    xzavier: for (var i = 1; i <= 10; i++) {
        for( var j = 1; j <= 10; j++) {
            if (i == j) {
                continue xzavier;
            }
            console.log(i + '>' + j);
        }
    }

    VM123:6 2>1
    VM123:6 3>1
    VM123:6 3>2
    VM123:6 4>1
    VM123:6 4>2
    VM123:6 4>3
    VM123:6 5>1
    VM123:6 5>2
    VM123:6 5>3
    VM123:6 5>4
    VM123:6 6>1
    VM123:6 6>2
    VM123:6 6>3
    VM123:6 6>4
    VM123:6 6>5
    VM123:6 7>1
    VM123:6 7>2
    VM123:6 7>3
    VM123:6 7>4
    VM123:6 7>5
    VM123:6 7>6
    VM123:6 8>1
    VM123:6 8>2
    VM123:6 8>3
    VM123:6 8>4
    VM123:6 8>5
    VM123:6 8>6
    VM123:6 8>7
    VM123:6 9>1
    VM123:6 9>2
    VM123:6 9>3
    VM123:6 9>4
    VM123:6 9>5
    VM123:6 9>6
    VM123:6 9>7
    VM123:6 9>8
    VM123:6 10>1
    VM123:6 10>2
    VM123:6 10>3
    VM123:6 10>4
    VM123:6 10>5
    VM123:6 10>6
    VM123:6 10>7
    VM123:6 10>8
    VM123:6 10>9

`continue xzavier`表示跳到标记为`xzavier`的循环，并继续下一次迭代。如果不使用这个标识符的话只会在内层循环中跳出当次循环并继续下一次循环。

当然，我们也不建议使用这样的写法，并没有那么好用。举例很随意，并非要实现一个这样的业务。如果要实现类似的功能，用continue换个写法就OK了。这里主要说明下我们还是有这样的写法存在的，用不用看你心情，看你的场景，以及你的团队同不同意。
  
## with语句

with语句的作用是将代码的作用域设置到一个特定的对象中。当代码运行到with语句时，执行上下文的作用域链临时被改变了。一个新的可变对象被创建，它包含了参数指定的对象的所有属性。这个对象将被推入作用域链的头部，这意味着函数的所有局部变量现在处于第二个作用域链对象中，因此访问代价更高了。如果，再挖深一点，JavaScript 引擎在编译阶段遇到with字段都不能好好的干活儿了，因为它不知道这个with最后会怎么改变作用域，本想把变量作用域都安置好都不行了。所以，一般不建议使用。


  [1]: https://segmentfault.com/a/1190000005927342
  [2]: https://segmentfault.com/a/1190000006672446
