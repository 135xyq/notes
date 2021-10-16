# [moment](http://momentjs.cn/)   [官网](https://momentjs.com/)
----------
## 解析方法
```javascript
  //解析
        //moment() 
        console.log(moment());
        //moment(String)
        console.log(moment('2013-02-08')); //返回2013年2月8号的日期对象
        console.log(
            moment('2013-039'), //返回2013年的第39天，2013年2月8号
            moment('2013050'), //返回2013年的第50天，2013年2月19号
            moment('2013W065'), //返回2013年的第6个星期的第5天，2013年2月8号（W表示星期）
            moment('2013-02-08T09'), //返回2013年2月8号9点（T表示时间）
        );
        console.log(moment('kaivon')); //警告，同时照样能返回那个对象，不过对象里的参数的值是不正确的
        //moment(String) 带格式 
        console.log(moment("12-25-1995", "MM-DD-YYYY"));
        console.log(moment("12/25/1995", "LL"));
        //moment(String) 多个格式 
        console.log(moment("29-06-1995", ["MM-DD-YYYY", "DD-MM", "DD-MM-YYYY"]));
        //moment(String) 特殊格式 
        console.log(moment("2010-01-01T05:06:07", moment.ISO_8601));
        //moment(Object) 
        console.log(moment({
            year: 2010,
            month: 3,
            day: 5,
            hour: 15,
            minute: 10,
            second: 3,
            millisecond: 123
        })); //注意：这里的月份也是从0开始，此时对应的是4月
        //moment(Number) 
        console.log(moment(1318781876406)); //这个参数为毫秒数
        //unix()
        console.log(moment.unix(1318781876406 / 1000)); //这个参数为秒数
        //moment(Date)
        console.log(moment(new Date(2011, 9, 16)));
        //moment(Number[])  参数为一个数组 [year, month, day, hour, minute, second, millisecond]
        console.log(moment([2010, 1, 14, 15, 25, 50, 125])); //注意月份是从0开始的，这里对应的是2月
        //moment(JSONDate) 
        console.log(moment("/Date(1198908717056-0700)/")); //前面一串数字为时间戳，-后面的是时区
        //moment(Moment) 参数为一个moment对象，用于克隆
        var a = moment([2012]);
        var b = moment(a);
        console.log(a.valueOf() === b.valueOf());
        //clone()   也可以使用clone去克隆
        var a = moment([2008]);
        var b = a.clone();
        console.log(a, b);
        /*
            GMT 世界时，格林尼治标准时间 
            UTC 协调世界时，世界统一时间、世界标准时间
         */
        //utc()
        console.log(moment().format()); //GMT //默认为本地当前时间，东八区的时间（+08:00）
        console.log(moment.utc().format()); //UTC       //UTC的时间（世界标准时间，位于0时区，时区用Z表示，它与北京时间相差8个小时）
        //isValid()
        console.log(
            moment([2015, 25, 35]).isValid(), //false
            moment([2015, 10, 35]).invalidAt(), //2
        );
```

## 赋值取值方法
```javascript
        console.log(moment().seconds() === new Date().getSeconds()); //true
        console.log(moment.utc().seconds() === new Date().getUTCSeconds()); //true
        //millisecond()/milliseconds()  获取或设置毫秒
        console.log(moment().millisecond());
        console.log(moment().milliseconds());
        console.log(moment().millisecond(100).valueOf());
        console.log(moment().milliseconds(100).valueOf());
        //second()/seconds()    获取/设置秒
        //minute()/minutes()    获取/设置分
        //hour()/hours()        获取/设置小时
        //date()/dates()        获取/设置日期
        //day()/days()          获取/设置星期
        console.log(
            moment().day(), //1
            moment().day('Sunday'), //设置星期的时候可以传入一个星期的英文单词
        );
        //weekday() 根据语言环境获获取/设置星期，根据语言环境获取或设置星期几
        moment.locale('zh-cn'); //把当前的语言环境设置为中文
        console.log(
            moment().weekday(), //0 
            moment().weekday(0), //0 //英文下是周日，中文下是周一
        );
        //dayOfYear()   获取或设置年份的日期（今天是今年的第几天）
        console.log(moment().dayOfYear()); //111
        console.log(moment().dayOfYear(1));
        //week()/weeks()    获取或设置年份的星期（当前星期是今年的第几个星期）
        console.log(moment().week()); //17
        console.log(moment([2021, 4, 20]).week()); //20
        //month()/months()  获取或设置月份，设置时范围为0-11，还支持月份名称
        console.log(moment().month()); //3
        console.log(moment().month('July')); //3
        //quarter()/quarters()  获取或设置季度
        console.log(moment().quarter()); //2 
        console.log(moment().quarter(4)); //2 
        //year()/years()    获取或设置年份
        console.log(moment().year());
        console.log(moment().year(2088));
        //weekYear()
        console.log(moment([2020, 0, 1]).weekYear());
        console.log(moment([2020, 11, 31]).weekYear());
        //weeksInYear() 根据语言环境获取当前 moment 年份的周数
        console.log(moment().weeksInYear()); //52
        //get() 获取日期
        console.log(moment().get('year'));
        console.log(moment().get('M'));
        console.log(moment().get('date'));
        //set() 设置日期
        console.log(
            moment().set('year', 2030),
            moment().set('month', 8),
            moment().set({
                'year': 2008,
                'month': 7,
                'date': 8
            }),
        );
        //max() 对比多个日期，返回最大的那个日期
        //min() 对比多个日期，返回最小的那个日期
        var a = moment('2019-10-15');
        var b = moment({
            year: 2010,
            month: 3,
            date: 5
        });
        var c = moment([2020, 10, 20]);
        console.log(moment.max(a, b, c)); //c
        console.log(moment.min(a, b, c)); //b
```

## 查询方法

```javascript
       //isBefore()    检查一个时间是否在另一个时间之前，默认是都转成毫秒数进行计算
        console.log(moment('2010-10-20').isBefore()); //true  没给参数默认为现在的时间
        console.log(moment('2010-10-20').isBefore('2010-10-19')); //false 第一个日期是否在第二个日期之前
        console.log(moment('2009-10-20').isBefore('2010-10-19', 'year')); //false 二个参数为对比的单位，可以给的有year month week isoWeek day hour minute second
        console.log(moment('2010-10-20').isBefore('2008-12-31', 'month')); //false
        //isSame()  检查两个时间是否相同
        console.log(moment('2010-10-20').isSame('2010-10-20'));
        console.log(moment('2010-10-20').isSame('2010-12-20', 'year'));
        //isAfter() 检查一个时间是否在另一个时间之后
        console.log(moment('2010-10-20').isAfter('2010-09-19')); //true
        //isSameOrBefore()  检查一个时间是否在另一个时间之前或者与之相同（<=）
        console.log(
            moment('2010-10-20').isSameOrBefore('2010-10-21'), //true
            moment('2010-10-20').isSameOrBefore('2010-10-20'), //true
            moment('2010-11-20').isSameOrBefore('2010-10-20'), //false
        );
        //isSameOrAfter() 检查一个时间是否在另一个时间之后或者与之相同（>=）
        console.log(
            moment('2010-11-20').isSameOrAfter('2010-10-21'), //true
            moment('2010-10-20').isSameOrAfter('2010-10-20'), //true
            moment('2010-10-19').isSameOrAfter('2010-10-20'), //false
        );
        //isBetween()   检查一个时间是否在其他两个时间之间
        console.log(
            moment('2010-10-20').isBetween('2010-10-19', '2010-10-25'), //true
            moment('2010-10-20').isBetween('2010-10-19', undefined), //true undefined等于moment(),就是当前的时间
            moment('2010-10-20').isBetween('2009-10-19', '2012-01-01', 'year'), //true
            //第四个参数为包容性，第三个参数为null，表示对比单位为默认毫秒数
            moment('2016-10-30').isBetween('2016-10-30', '2016-12-30', null, '(]'), //false
        );
        //isLeapYear()  检测是否为闰年
        console.log(
            moment().isLeapYear(), //true
            moment([2019]).isLeapYear(), //false
        );
        //isMoment() 检测变量是否为moment对象
        console.log(
            moment.isMoment(), //false
            moment.isMoment(new Date()), //false
            moment.isMoment(moment()), //true
        );
        //isDate()  检测变量是否为原生的Date对象
        console.log(
            moment.isDate(), //false
            moment.isDate(new Date()), //true
            moment.isDate(moment()), //false
        );
```

## 国际化、自定义方法
```javascript
       //设置语言环境 (全局) 
        //moment.locale('zh-cn');
        console.log(moment.locale()); //en //返回当前的语言环境
        console.log(
            moment().weekday(0), //根据语言环境获取或设置（传参）星期几。英文环境为星期天，中文环境为星期一
            moment().format('LLLL'), //格式化时间，参数为本地化格式。英文环境与中文环境都不同
            moment().month(),
        );
        //设置语言环境 (局部) 
        var myMoment = moment();
        myMoment.locale('ar-dz');
        console.log(moment().format('LLLL'));
        console.log(myMoment.format('LLLL'));
        //months()/weekdays() 
        /* moment.locale('ru');
        moment.locale('zh-hk'); */
        console.log(
            moment.months(),
            moment.monthsShort(),
            moment.weekdays(),
            moment.weekdaysShort(),
            moment.weekdaysMin(),
        );
        //localeData()
        console.log(
            moment.localeData(),
            moment.localeData().monthsShort(),
        );
        //自定义
        moment.updateLocale('zh-cn', {
            //设置月份名称
            months: '一月_二月_三月_四月_五月_六月_七月_八月_九月_十月_十一月_十二月'.split('_'),
            //设置月分名称的缩写
            monthsShort: '1月_2月_3月_4月_5月_6月_7月_8月_9月_10月_11月_12月'.split('_'),
            //设置星期名称
            weekdays: '星期日_星期一_星期二_星期三_星期四_星期五_星期六'.split('_'),
            //设置星期名称的缩写
            weekdaysShort: '周日_周一_周二_周三_周四_周五_周六'.split('_'),
            //设置星期名称的最小缩写
            weekdaysMin: '日_一_二_三_四_五_六'.split('_'),
            //设置长日期格式，是个对象
            longDateFormat: {
                LT: 'Ah点mm分',
                LTS: 'Ah点m分s秒',
                L: 'YYYY-MM-DD',
                LL: 'YYYY年MMMD日',
                LLL: 'YYYY年MMMD日Ah点mm分',
                LLLL: 'YYYY年MMMD日ddddAh点mm分',
                l: 'YYYY-MM-DD',
                ll: 'YYYY年MMMD日',
                lll: 'YYYY年MMMD日Ah点mm分',
                llll: 'YYYY年MMMD日ddddAh点mm分'
            },
            //设置相对时间，from()与to()的方法返回的值就是从这里取的
            relativeTime: {
                future: '%s内',
                past: '%s前',
                s: '几秒',
                m: '1 分钟',
                mm: '%d 分钟',
                h: '1 小时',
                hh: '%d 小时',
                d: '1 天',
                dd: '%d 天',
                M: '1 个月',
                MM: '%d 个月',
                y: '1 年',
                yy: '%d 年'
            },
            //设置时间段，参数：小时,分钟,大小写
            meridiem: function(hour, minute, isLower) {
                const hm = hour * 100 + minute;
                if (hm < 600) {
                    return '凌晨';
                } else if (hm < 900) {
                    return '早上';
                } else if (hm < 1130) {
                    return '上午';
                } else if (hm < 1230) {
                    return '中午';
                } else if (hm < 1800) {
                    return '下午';
                } else {
                    return '晚上';
                }
            },
            //设置日历
            calendar: {
                sameDay: function() {
                    return this.minutes() === 0 ? '[今天]Ah[点整]' : '[今天]LT';
                },
                nextDay: function() {
                    return this.minutes() === 0 ? '[明天]Ah[点整]' : '[明天]LT';
                },
                lastDay: function() {
                    return this.minutes() === 0 ? '[昨天]Ah[点整]' : '[昨天]LT';
                },
                nextWeek: function() {
                    let startOfWeek, prefix;
                    startOfWeek = moment().startOf('week');
                    prefix = this.diff(startOfWeek, 'days') >= 7 ? '[下]' : '[本####]';
                    return this.minutes() === 0 ? prefix + 'dddAh点整' : prefix + 'dddAh点mm';
                },
                lastWeek: function() {
                    let startOfWeek, prefix;
                    startOfWeek = moment().startOf('week');
                    prefix = this.unix() < startOfWeek.unix() ? '[上]' : '[本]';
                    return this.minutes() === 0 ? prefix + 'dddAh点整' : prefix + 'dddAh点mm';
                },
                sameElse: 'LL'
            },
            week: {
                dow: 1, //星期的第一天是周1
                doy: 4
            }
        });
        console.log('今天是：' + moment().format('MMMM') + ' ' + moment().format('dddd'));
        console.log('今天是：' + moment().format('MMM') + ' ' + moment().format('ddd'));
        console.log(moment().format('LLLL'));
        console.log(moment([2008]).from());
        console.log(moment().calendar(moment([2020, 3, 15])));
```

##时长方法
```javascript
        //时长
        console.log(moment.duration());
        console.log(
            moment.duration(100), //给一个参数表示为毫秒
            moment.duration(2, 'seconds'), //时长为2s
            moment.duration(3, 'minutes'), //时长为3min
            moment.duration(1, 'M'),
            //参数也可以是一个对象
            moment.duration({
                seconds: 1,
                minutes: 2,
                hours: 3,
                days: 4,
                weeks: 5,
                months: 6,
                years: 7
            }),
            //ASP.NET 风格的时间跨度
            moment.duration('23:59:59'), //时:分:秒
        );
        //clone() 克隆一个时长对象
        var d1 = moment.duration();
        var d2 = d1.clone();
        d1.add(1, 'second');
        console.log(d1, d2);
        moment.locale('zh-cn');
        //humanize()    显示一段时长
        console.log(
            moment.duration(1, 'minutes').humanize(),
            moment.duration(24, 'hours').humanize(),
            moment.duration(1, 'minutes').humanize(true), //1 分钟内
            moment.duration(-1, 'minutes').humanize(true), //1 分钟前
        );
        //milliseconds()    此方法会计算溢出
        //asMilliseconds()
        console.log(
            moment.duration(500).milliseconds(), //500
            moment.duration(1500).milliseconds(), //500
            moment.duration(15000).milliseconds(), //0
            //moment.duration(1500)
            moment.duration(500).asMilliseconds(), //500
            moment.duration(1500).asMilliseconds(), //1500
            moment.duration(15000).asMilliseconds(), //15000
        );
        //seconds()
        //asSeconds()
        console.log(
            moment.duration(500).seconds(), //0
            moment.duration(1500).seconds(), //1
            moment.duration(15000).seconds(), //15
            moment.duration(500).asSeconds(), //0.5
            moment.duration(1500).asSeconds(), //1.5
            moment.duration(15000).asSeconds(), //15
        );
        //add() 增加时长，这个方法可以添加多种类型的参数
        var a = moment.duration(1, 'd'); //时长为1天
        var b = moment.duration(2, 'd'); //时长为2天
        console.log(
            a.add(b).days(),
            moment.duration().add(1, 'd').days() // 1
        );
        //subtract()    减少时长
        var a = moment.duration(3, 'd');
        var b = moment.duration(2, 'd');
        console.log(
            a.subtract(b).days(), //1
            moment.duration(5, 'd').subtract(1, 'd').days() //4
        );
        //duration(x.diff(y))   获取两个时长的差值
        var a = moment([2018, 10, 21, 10, 05]);
        var b = moment([2018, 10, 21, 10, 06]);
        console.log(
            moment.duration(b.diff(a)),
        );
        //as()
        console.log(
            moment.duration(1000).as('milliseconds'), //1000
            moment.duration(1000).as('seconds'), //1
        )
        //get()
        var d = moment.duration({
            seconds: 1,
            minutes: 2,
            hours: 3,
            days: 4,
            months: 5,
            years: 6
        });
        console.log(d);
        console.log(
            d.get('seconds'),
            d.get('minutes'),
            d.get('hours'),
            d.get('days'),
            d.get('months'),
            d.get('years'),
        )
```