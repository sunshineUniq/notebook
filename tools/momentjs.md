# momentjs

```javascript
npm install moment
```

webpack 配置

默认情况下，webpack 会打包所有的 Moment.js 语言环境（在 Moment.js 2.18.1 中，最小为 160 KB）。 若要剥离不必要的语言环境且仅打包使用的语言环境，则添加 [`moment-locales-webpack-plugin`](http://nodejs.cn/s/kATSRF)：

```javascript
// webpack.config.js
const MomentLocalesPlugin = require('moment-locales-webpack-plugin');

module.exports = {
    plugins: [
        // 剥离除 “en” 以外的所有语言环境。
        new MomentLocalesPlugin(),

        // 或者：剥离除 “en”、“es-us” 和 “ru” 以外的所有语言环境。
        //（“en” 内置于 Moment 中，无法移除）
        new MomentLocalesPlugin({
            localesToKeep: ['es-us', 'ru'],
        }),
    ],
};
```

##### 动态引入语言包 - 让你的 moment 库更小https://zhuanlan.zhihu.com/p/56103483

APIS

```javascript
// 日期格式化
moment('20210127').format('YYYY-MM-DD') // 2021-01-27
moment('20210127').format('YYYY-MM-DD HH:mm:ss') // 2021-01-27 00:00:00
// 加，减
moment().add(1, 'months').format('YYYY-MM-DD') // 当前时间加1个月并格式化成YYYY-MM-DD形式
moment('20210127').add(2, 'days').format('YYYY-MM-DD') // 输入的日期加2天，并格式化
moment().subtract(7, 'days') // 当前时间减去7天
// 获取星期几
moment().day()
moment('20210127').day() // 3 当前日期/指定日期 是星期几
// 获取毫秒数
moment('20210127').valueOf() // 1611750522029
// 获取时间差 注意：计算时间差时，可以以 “years”、“days”、“hours”、“minutes” 以及 "seconds" 为单位输出！
 moment('20220127').diff(moment(date),'days' ) // 365 开始时间和结束时间的时间差，以“天”为单位
moment('20220127').diff(moment(date),'minutes' )  // 525600  开始时间和结束时间的时间差，以“分钟”为单位
// 获取时、分、秒
原理：利用字符串的 split 方法拆分时分秒，然后分别用moment的 hour、minute 和 second 方法；带有日期的可以用 .valueof() 方法。
const fixStart = '08:00:00'
 
const getHour = this.moment().hour(Number(fixStart.split(':')[0]));
const getMinute = this.moment().minute(Number(fixStart.split(':')[1]));
const getSecond = this.moment().second(Number(fixStart.split(':')[2]));
            
// 描述为0，直接写出second(0)
const getHour_Minute_Second = this.moment().hour(Number(fixStart.split(':')[0])).minute(Number(fixStart.split(':')[1])).second(0);       
 
console.log('=====输出',getHour,getMinute,getSecond,getHour_Minute_Second);

// 将毫秒数转为时分秒
注意：毫秒转为其他单位时，达到你想要转的单位时，为1，超过时不管，不足时为0；
const msTime = 4800000;        //80分钟
 
moment.duration(msTime).hours();       //转为小时，值为1
moment.duration(msTime).minutes();     //转为分钟，值为20
moment.duration(msTime).seconds();     //转为秒，值为0
转为其他单位：

moment.duration(msTime, 'seconds');        //转为秒
moment.duration(msTime, 'minutes');        //转为分
moment.duration(msTime, 'hours');          //转为小时
moment.duration(msTime, 'days');           //转为天
moment.duration(msTime, 'weeks');          //转为周
moment.duration(msTime, 'months');         //转为月
moment.duration(msTime, 'years');          //转为年

// 判断一个日期是否在两个日期之前  isBetween
语法： this.moment().isBetween(moment-like, moment-like, String, String);
a. 不包含起始这两个日期（只有两个参数）   ==>> 中文网只有两个参数
this.moment('2010-10-20').isBetween('2010-10-19', '2010-10-25'); // true
this.moment('2010-10-19').isBetween('2010-10-19', '2010-10-25'); // false
this.moment('2010-10-25').isBetween('2010-10-19', '2010-10-25'); // false
b. 自定义是否包含起始日期（四个参数，主要是第四个参数）   ==>> 英文网才有四个参数
    第三个参数，固定为null；
    第四个参数，字符串，( ) 表示不包含，[ ] 表示包含。右括号制开始日期，右括号控制结束日期
    
this.moment('2016-10-30').isBetween('2016-10-30', '2016-12-30', null, '()'); //false
this.moment('2016-10-30').isBetween('2016-10-30', '2016-12-30', null, '[)'); //true
this.moment('2016-10-30').isBetween('2016-01-01', '2016-10-30', null, '()'); //false
this.moment('2016-10-30').isBetween('2016-01-01', '2016-10-30', null, '(]'); //true
this.moment('2016-10-30').isBetween('2016-10-30', '2016-10-30', null, '[]'); //true
```





