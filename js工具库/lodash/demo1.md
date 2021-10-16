# [lodash](https://javasoho.com/lodash/docs/4.16.1.html)

## Array
```javascript
        
//chunk()   把数组拆分成一个二维数组，拆分后的第1个数组的长度为第二个参数的值
        
console.log(_.chunk(['a', 'b', 'c', 'd'], 2));  //[["a", "b"],["c", "d"]]
 
        
//compact() 过滤掉原数组里的非真（转布尔值后为false）数据
        
console.log(_.compact([0, 1, false, 2, '', 3, null, NaN, undefined]));  //[1, 2, 3]
 
        
//concat()  合并数组，与Array对象的方法一样
 
        
//difference()  在第一个数组中把第二个数组里的数据都排除掉
        
console.log(_.difference([1, 3, 5, 7, 9], [3, 7])); // [1, 5, 9]
 
        
//differenceBy  与上面的方法一样，只不过它可以再接收一个迭代器的函数做为参数
        
console.log(_.differenceBy([3.1, 2.2, 1.3], [4.4, 2.5], Math.floor));   //[3.1, 1.3]
 
        
//differenceWith()  与上面的方法一样，只不过它可以接收一个比较器的函数做为参数，对每个数据都要比较一下
        
var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
        
console.log(_.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual));    //[{ 'x': 2, 'y': 1 }]
 
        
//drop()    切掉数组的前n（第二个参数，默认为1）位
        
console.log(_.drop(['a', 'b', 'c', 'd', 'e'], 2));  //['c', 'd', 'e']
        
//dropRight()   切割数组，切掉数组的后n位
 
        
//dropWhile()   去掉数组中，从起点到第二个方法返回假的数据。与Array对象身上的filter()方法一样
        
//dropRightWhile()  与上面一样，不过它是从右边开始查，查到返回假的那个数据都去除
 
        
//take()    提取数组的前n（第二个参数，默认为1）位。与drop方法相反
        
console.log(_.take(['a', 'b', 'c', 'd', 'e'], 2));
        
//takeRight()/takeWhile()/takeRightWhile()  与上面的一样
 
        
//fill()    填充数组，与Array对象身上的fill()方法一样
        
//findIndex()   查找到第一个满足条件的数据的索引值（从左往右查），没找到返回-1。与Array对象身上的findIndex()方法一样
        
//findLastIndex()   这与上面的findIndex是一样的，区别是它是从右往左的查
 
        
//flatten() 减少一级数组嵌套深度，与Array的flat()这个方法相似
        
console.log(_.flatten(['a', ['b', ['c', ['d']]]]));
 
        
//flattenDeep() 把数组递归为一维数组。相当于[].flat(Infinity)
        
console.log(_.flattenDeep(['a', ['b', ['c', ['d']]]])); //["a", "b", "c", "d"]
 
        
//flattenDepth()    减少n（第二个参数）层数组的嵌套。相当于[].flat(2)
        
console.log(_.flattenDepth(['a', ['b', ['c', ['d']]]], 2)); //["a", "b", "c", "d"]
 
        
//fromPairs()   把数组转换为一个对象，与Object.fromEntries()方法一样
        
//head()/first()    获取数组里第一个元素，就是取下标为0的那个数据
        
//last()    取数组里的最后一位数据，取下标为length-1的那个数据
 
        
//indexOf() 查找数据，并返回数据对应的索引值，与Array对象身上的indexOf()方法一样
        
//lastIndexOf() 查找数据，并返回数据对应的索引值，与Array对象身上的lastIndexOf()方法一样
        
//initial() 获取数组里除了最后一位的所有数据。相当于删除数组里的最后一个数据，与Array对象身上的pop()方法一样。区别在于pop方法会改变原数组，而这个方法不会改变原数组
        
//tail()    获取除了array数组第一个元素以外的全部元素，想当于Array对象身上的shift()，与initial()相反
 
        
//intersection()    取数组的交集
        
console.log(_.intersection(['a', 'b'], ['b', 'c'], ['e', 'b']));    //['b']
 
        
//union()   取数组的并集（合并起来，去掉重复的）
        
console.log(_.union([2], [1, 2]));  //[2, 1]
 
        
//xor() 删除数组的交集，留下非交集的部分
        
console.log(_.xor(['a', 'b'], ['b', 'c'], ['e', 'b'])); //["a", "c", "e"]
 
        
//join()    把数组转成字符串，这个方法原生的Array对象也有
 
        
//nth() 取数组里的某个数据，就是通过下标取到某个数据。只不过它的数字可以为负。表示倒着找
        
var array = ['a', 'b', 'c', 'd'];
        
console.log(
            
_.nth(array, 1),    //b
            
_.nth(array, -3),   //c
        
);
 
        
//以下这几个方法，用后面remove的方法代替
        
//pull()    根据给的参数（参数为数据）删除原数组里的对应数据
        
//pullAll() 与上面的方法一样，就是参数为数组（好比call,apply这两个方法）
        
//pullAllBy()\pullAllWith() 与前面方面的语法一样
        
//pullAt()  根据给的参数（参数为索引）删除原数组里的对应数据
 
        
//remove()  根据函数删除原数组里的数据
        
var arr = ['a', 'b', 'c', 'd', 'e'];
        
_.remove(arr, function (value, index, array) {
            
return index > 2;
        
});
        
console.log(arr);   //["a", "b", "c"]
 
        
//without() 根据给的参数（参数为数据）删除原数组里的对应数据
        
var arr = ['a', 'b', 'c', 'd', 'e'];
        
console.log(
            
_.without(arr, 'b', 'c'),
            
arr
        
);
 
        
//reverse() 颠倒数组，这个方法原生的Array对象也有
        
//slice()   截取数组，这个方法原生的Array对象也有
 
        
//uniq()
        
console.log(_.uniq([1, 2, 2, 1]));  //[1, 2]
        
//uniqBy()/uniqWith() 与前面的一样
 
        
//zip() 把各数组中索引值相同的数据放到一起，组成新数组
        
console.log(_.zip(['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]));  //[["小明", "男", 12],["小红", "女", 13],["小刚", "男", 14]]
 
        
//zipObject()   与上面方法一样，区别是它输出的是对象
        
console.log(_.zipObject(['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]));    //{小明: "男", 小红: "女", 小刚: "男"}
 
        
//zipWith()
 
        
//unzip()   这个方法与zip相反，把每个数组里索引值一样的数据放在一起
        
console.log(_.unzip([["小明", "男", 12],["小红", "女", 13],["小刚", "男", 14]]));    //[['小明', '小红', '小刚'], ['男', '女', '男'], [12, 13, 14]]
        
//unzipWith()   与zipWidth()一样，接收了一个迭代器的函数

```

## collection
```javascript

        
//countBy() 按照一定规则统计数量，key循环次数，value为匹配到的数量
        
console.log(_.countBy(['one', 'two', 'three'], 'length'));  //{3: 2, 5: 1}  按每个字符串的length进行统计，length为3的有两个数据。length为5的有1个数据
 
        
//groupBy() 按照一定规则进行分组，key为循环次数，value为匹配到的数组
        
console.log(_.groupBy(['one', 'two', 'three'], 'length'));  //{3: ["one", "two"], 5: ["three"]}
 
        
//each()/forEach()  循环，与原生Array.forEach一样
        
//eachRight()/forEachRight()    倒着循环
        
//every()   与原生Array.every方法一样
        
//filter()  过滤数组，与Array对象上的filter()方法一样
        
//find()    查找数据，与Array对象上的find()方法一样
        
//findLast()    与上面一样，区别在于它是从右往左查
        
//flatMap()     生成一个扁平化的数组，与原生的flatMap()方法一样        
        
//flatMapDeep() 与上面一样，不过它可以递归
        
//flatMapDepth()    与上面一样，它可以递归，并且可以指定递归的深度
        
//includes()    与Array对象上的includes()方法一样
 
        
//invokeMap()   使用第二个参数（方法）去处理数组，返回处理后的结果（数组）
        
console.log(
            
_.invokeMap([[5, 1, 7], [3, 2, 1]], 'sort'),    //[ [1, 5, 7],[1, 2, 3]]
            
_.invokeMap([123, 456], String.prototype.split, ''),    //[["1", "2", "3"],["4", "5", "6"]]
        
);
 
        
//keyBy()   创建一个对象，里面的key由第二个参数决定。value为原数组里对应的那条数据
        
var array = [
            
{ 'dir': 'left', 'code': 97 },
            
{ 'dir': 'right', 'code': 100 }
        
];
        
var result = _.keyBy(array, function (o) {
            
return String.fromCharCode(o.code); //key为使用fromCharCode解析后的字符。value为它所在数组里的那条数据
        
});
        
console.log(result);
 
        
//key为dir，value为key所在原数组里的那条数据
        
console.log(_.keyBy(array, 'dir'));
 
        
//orderBy() 排序，既能升序又能降序
        
var users = [
            
{ 'user': 'fred', 'age': 48 },
            
{ 'user': 'barney', 'age': 34 },
            
{ 'user': 'fred', 'age': 40 },
            
{ 'user': 'barney', 'age': 36 }
        
];
        
console.log(
            
_.orderBy(users, 'age', 'asc'), //以age属性的值进行升序排序
            
_.orderBy(users, 'user', 'desc'),   //以user属性的值进行降序排序
        
);
 
        
//sortBy()      排序，只能升序
        
console.log(
            
_.sortBy(users, function (o) {
                
return o.user;
            
}),
        
);
 
        
//partition()   根据第2个参数把一个数组分拆成一个二维数组
        
var users = [
            
{ 'user': 'barney', 'age': 36, 'active': false },
            
{ 'user': 'fred', 'age': 40, 'active': true },
            
{ 'user': 'pebbles', 'age': 1, 'active': false }
        
];
        
console.log(
            
_.partition(users, function (o) {   //active为true的放在一起，active为false的放在一起
                
return o.active;
            
}),
            
_.partition(users, { 'age': 1, 'active': false }),//把第二个参数对应的数据放一起，其余的放一起
        
);
         
        
//reduce()  与Array对象上的reduce()方法一样
        
//reduceRight() 与Array对象上的reduceRight()方法一样
         
        
//reject()
        
var users = [
            
{ 'user': 'barney', 'age': 36, 'active': false },
            
{ 'user': 'fred', 'age': 40, 'active': true }
        
];
        
console.log(
            
_.reject(users, function (o) {
                
return o.active;    //barney
            
}),
            
_.reject(users, { 'age': 36, 'active': false }),    //fred
            
_.reject(users, ['user', 'fred']),  //barney
            
_.reject(users, 'age'), //[]
        
);
 
        
//sample()  从数组中随机取一个数据
        
console.log(_.sample(['a', 'b', 'c', 'd', 'e']));
 
        
//sampleSize()  获得 n 个随机数据
        
console.log(_.sampleSize(['a', 'b', 'c', 'd', 'e'], 3));
 
        
//shuffle() 随机排序
        
console.log(_.shuffle(['a', 'b', 'c', 'd', 'e']));
 
        
//size()    返回集合长度
        
console.log(
            
_.size(['a', 'b', 'c', 'd', 'e']),  //5
            
_.size({ a: 1, b: 2 }), //2
            
_.size('kaivon'),   //6
        
);
 
        
//some()    与Array对象上的some()方法一样
    
```

## function
```javascript
    //defer()   推迟调用函数，在第二次事件循环的时候调用 
        _.defer(function(text) {
            console.log(text);
        }, '第二次事件循环');
        console.log('第一次事件循环');
        //delay()
        _.delay(function(text) {
            console.log(text);
        }, 1000, '延迟一秒执行');
        //flip()    调用函数时翻转参数
        function fn1() {
            console.log(arguments);
        }
        fn1 = _.flip(fn1);
        fn1(1, 2, 3);
        //negate()  结果取反函数
        function fn2(n) {
            return n % 2 == 0;
        };
        console.log(_.filter([1, 2, 3, 4, 5, 6], _.negate(fn2))); //[1, 3, 5]
        //once()    函数只能调用一次
        function fn3() {
            console.log('fn3');
        }
        var newFn3 = _.once(fn3);
        newFn3();
        newFn3();
```

## Lang
```javascript
        //castArray()   强制转为数组，其实就是在外面加一层方括号
        console.log(
            _.castArray('a'), //["a"]
            _.castArray({
                a: 1,
                b: 2
            }), //[{a: 1, b: 2}]
        );
        //clone()   浅拷贝
        var obj1 = {
            a: 1,
            b: {
                c: 2
            }
        };
        var obj2 = _.clone(obj1);
        console.log(obj1, obj2);
        obj2.b.c = 3, console.log(obj1, obj2);
        //cloneDeep()   深拷贝
        var obj3 = _.cloneDeep(obj1);
        obj3.b.c = 4, console.log(obj1, obj3);
        //conformsTo()  通过第二个参数来检测对象的属性值是否满足条件
        var object = {
            'a': 1,
            'b': 2
        };
        console.log(
            _.conformsTo(object, {
                'b': function(n) {
                    return n > 1
                }
            }), //true
            _.conformsTo(object, {
                'b': function(n) {
                    return n > 2
                }
            }), //false
        );
        //ea()  比较两个值是否相等。与Object.is()这个方法一样
        console.log(
            _.eq(12, 12), //true
            _.eq({
                a: 1
            }, {
                a: 1
            }), //false
            _.eq(NaN, NaN), //true
        );
        //gt()  第一个值是否大于第二个值
        console.log(
            _.gt(3, 1), //true
            _.gt(3, 3), //false
        );
        //gte() 第一个值是否大于等于第二个值
        //lt()  小于
        //lte() 小于等于
        //isArray()
        console.log(
            _.isArray([1, 2, 3]), //true
            _.isArray(document.body.children), //false
            _.isObject({}), //true
            _.isObject(null), //false
        );
        //toArray()
        console.log(
            _.toArray({
                a: 1,
                b: 2
            }), //[1, 2]
            _.toArray('abc'), //["a", "b", "c"]
            _.toArray(null), //[]

```

## object
```javascript
        //assign()  合并对象，与Object.assign()方法一样
        //assignIn()/extend()   与上面一样，不过它能继承原型身上的属性
        //assignInWith()/extendWith()   与上面一样，接收一个比较器的函数做为参数
        //assignWith()  也是接收一个比较器的函数做为参数
        //at()  根据传入的属性创建一个数组
        var object = {
            'a': [{
                'b': {
                    'c': 3
                }
            }, 4]
        };
        console.log(_.at(object, ['a[0].b.c', 'a[1]'])); //[3, 4]
        //create()  与Object.create()一样
        //defaults()    合并对象，与assign()一样，不过assign方法合并时遇到相同的属性，后面的会覆盖前面的。defaults刚好相反，前面的覆盖后面的
        console.log(
            _.defaults({
                'a': 1
            }, {
                'b': 2
            }, {
                'a': 3
            }), //{a: 1, b: 2}
            _.assign({
                'a': 1
            }, {
                'b': 2
            }, {
                'a': 3
            }), //{a: 3, b: 2}
        );
        //defaultsDeep()    与defaults一致，不过它会深递归
        //toPairs()/entries()   把对象里可枚举的属性(不包括继承的)创建成一个数组，与Object.entities()的方法一样
        //toPairsIn()/entriesIn()   与上面的一样，但它包括继承的属性
        //findKey() 与前面讲的find方法一样，只不过它返回的是key
        var users = {
            'barney': {
                'age': 36,
                'active': true
            },
            'fred': {
                'age': 40,
                'active': false
            },
            'pebbles': {
                'age': 1,
                'active': true
            }
        };
        console.log(_.findKey(users, {
            'age': 1,
            'active': true
        })); //pebbles
        //findLastKey() 与上面一样，只不过它从反方向开始遍历
        //forIn()   与原生 的for...in循环一样，只不过它是一个函数，语法与forEach一样。它遍历的是自己的属性与继承的属性
        //forInRight()  与上面一样，只不过是反方向遍历
        //forOwn()  与forIn()一样，只不过forOwn只能遍历到自己的属性
        //forOwnRight() 与上面一样，只不过是反方向遍历
        //functions()/functionsIn() 这两个没有说？？？？？？
        //get() 获取属性的值，与Object.defineProperty() 属性描述对象上的get方法一致
        //set() 设置属性的值，与Object.defineProperty() 属性描述对象上的set方法一致
        //setWith() 与上面的一样，只不过可以给一个参数决定返回的是对象还是数组
        console.log(_.setWith({}, '[0][1]', 'a', Array));
        //has() 检查属性是否为对象的直接属性，与Object.hasOwnProperty()方法返回true一样
        //hasIn()   检查属性是对象的直接属性还是继承属性，也与Object.hasOwnProperty()一样，true表示直接属性，false表示继承属性
        //invert()  把对象的key与value颠倒，后面的属性会覆盖前面的属性
        var object = {
            'a': 1,
            'b': 2,
            'c': 1
        };
        console.log(_.invert(object)); //{1: "c", 2: "b"}
        //invertBy()    与上面一样，它遇到相同的值后不会覆盖，而是会把所有放在一个数组里。另外它多了一个遍历器方法
        //invoke()  调用方法去处理取到的属性值
        var object = {
            'a': [{
                'b': {
                    'c': [1, 2, 3, 4]
                }
            }]
        };
        console.log(_.invoke(object, 'a[0].b.c.slice', 1, 3)); //[2, 3]    用slice方法去截取a[0].b.c的1-3位
        //keys()    把对象的key放到一个数组里，与Object.keys()的方法一样
        //keysIn()  与上面一样，只不过它包含继承到的属性
        //values()  把对象的value放到一个数组里，与Object.value()的方法一样
        //valuesIn()    与上面一样，只不过它包含继承到的属性
        //mapKeys() 修改对象的key，value不会变
        var result = _.mapKeys({
            'a': 1,
            'b': 2
        }, function(value, key) {
            return key + value;
        });
        console.log(result); //{a1: 1, b2: 2}
        //mapValues()   与上个方法一样，只不过它修改的是value，key不会变
        //merge()   它与assign一样，不过它遇到相同的属性名后并不会覆盖，它会合并
        var object = {
            'a': [{
                'b': 2
            }, {
                'd': 4
            }]
        };
        var other = {
            'a': [{
                'c': 3
            }, {
                'e': 5
            }]
        };
        console.log(_.merge(object, other));
        //mergeWith()   与上面的方法一致，不过多了接收一个比较器的函数做为参数
        //omit()    删除对象里的属性
        console.log(_.omit({
            'a': 1,
            'b': '2',
            'c': 3
        }, ['a', 'c'])); //{b: "2"}
        //_.omitBy  与上面一样，不过是接收一个迭代器的函数做为参数
        //pick()    筛选对象里的属性
        console.log(_.pick({
            'a': 1,
            'b': '2',
            'c': 3
        }, ['a', 'c'])); //{a: 1, c: 3}
        //pickBy()  与上面一样，不过是可接收一个迭代器的函数做为参数
        //result()  获取对象属性，它与get一样。只不过它遇到函数的属性时会调用函数，并且把this指向对象本身
        var obj = {
            a: 12,
            b: function() {
                console.log(this.a);
            }
        };
        console.log(_.result(obj, 'a')); //12
        _.result(obj, 'b'); //12
        console.log(_.get(obj, 'b')); //它只能取到这个函数，并不能执行
        //toPairs() 把对象的key与value一起放到数组里
        function Foo() {
            this.a = 1;
            this.b = 2;
        }
        Foo.prototype.c = 3;
        console.log(_.toPairs(new Foo()));
        console.log(_.toPairsIn(new Foo()));
        //unset()   删除属性
        var object = {
            'a': [{
                'b': {
                    'c': 7
                }
            }]
        };
        _.unset(object, 'a[0].b.c'), console.log(object);
        //update()  这个与set一样，不过它可以接收一个函数的参数
        var object = {
            a: 10
        };
        _.update(object, 'a', function(n) {
            return n * n
        });
        console.log(object); ///{a: 100}
        //updateWith()  与上面的一样，不过可以接收一个路径的参数，决定生成的属性放在哪里
        var object = {};
        _.updateWith(object, '[a][b]', function() {
            return 12;
        }, Object);
        console.log(object);
```

## string
```javascript
        //camelCase()   转换字符串为驼峰格式
        console.log(
            _.camelCase('kaivon_chen'),
            _.camelCase('kaivon chen'),
        );
        //capitalize()  首字母为大写
        console.log(_.capitalize('kaivon')); //Kaivon
        //endsWith()    查检结尾的字符
        console.log(_.endsWith('abc', 'c')); //true
        //escape()  把特殊字符转义成真正的HTML实体字符
        console.log(_.escape('ka<iv>on')); //ka<iv>on
        //unescape()    与上面相反
        console.log(_.unescape('ka<iv>on')); //ka<iv>on
        //kebabCase()   转换字符为加-的形式
        console.log(_.kebabCase('k a i')); //k-a-i
        //lowerCase()/toLower() 转小写
        //upperCase()/toUpper() 转大写
        //lowerFirst()  首字符转小写
        //upperFirst()  首字符转大写
        //pad() 填充字符串到指定的长度(左右填充)
        console.log(_.pad('abc', 8, '-')); //--abc---
        //padEnd()
        console.log(_.padEnd('abc', 8, '-'));
        //padStart()
        console.log(_.padStart('abc', 8, '-'));
        //parseInt()    把字符串类型的数字转成数字，
        //repeat()  重复字符串
        console.log(_.repeat('kaivon', 2)); //kaivonkaivon
        //replace() 替换字符串
        console.log(_.replace('kaivon', 'von', '***')); //kai***
        //snakeCase()   转换字符串为_的形式
        console.log(_.snakeCase('k a i')); //k_a_i
        //split()   分隔字符串为数组，与原生String.split()一样
        //startCase()   转换字符串为+空格的形式，并且首字符大写
        console.log(
            _.startCase('kaivon-chen'), //Kaivon Chen
            _.startCase('kaivonChen'), //Kaivon Chen
            _.startCase('kaivon_chen'), //Kaivon Chen
        );
        //startsWith()  检查字符串的开始字符
        console.log(_.startsWith('kaivon', 'k')); //true
        //template()    编译模板
        var compiled = _.template('hello <%= user %>!'); //user为一个占位符
        console.log(compiled({
            'user': 'kaivon'
        })); //拿到数据后，给user赋值，它就能正确解析出内容了
        //trim()    去除首尾空格，或者指定字符
        console.log(_.trim('kaivon-', '-')); //kaivon
        //trimEnd() 去除后面的空格，或者指定字符
        //trimStart()   与上面的一样，只不过去除的是左边的
        //truncate()
        console.log(_.truncate('Hi kaivon! How are you feeling today? I am felling great!')); //Hi kaivon! How are you feel...
        console.log(_.truncate('Hi kaivon! How are you feeling today? I am felling great!', {
            //'length': 10, //限制固定的字符个数
            'separator': /!/ //加个正则，遇到第一个空格后就加三个点
        }));
        //words()   把字符串的单词拆分成数组
        console.log(_.words('kaivon chen')); //["kaivon", "chen"]
```
