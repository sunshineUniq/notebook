Nodejs最大的特点： 异步式I/O与事件紧密结合的编程模式

磁盘读写或网络通信（统称为I/O操作）

阻塞：线程在执行中如果遇到 I/O, 通常需要耗费较长事件，这时操作系统会剥夺这个线程的CPU控制权， 使其暂停执行，同时将资源让给其他的工作线程，这种线性调度方式称为阻塞

异步I/O: 当线程遇到I/O操作时，将I/O请求发送给操作系统，继续执行下一句语句。当操作系统完成I/O操作时，以事件的形式通知执行I/O操作的线程，线程会在特定时候处理这个事件。为了处理异步I/O, 线程必须有事件循环，不断的检查有没有未处理的事件，依次予以处理。

#### 同步式I/O和异步式I/O的特点

| 同步式I/O                           | 异步式I/O                  |
| ----------------------------------- | -------------------------- |
| 利用多线程提供吞吐量                | 单线程即可实现高吞吐量     |
| 通过时间片分割和线程调度利用多核CPU | 通过功能划分利用多核CPU    |
| 需要由操作系统调度多线程使用多核CPU | 可以将单进程 绑定到单核CPU |
| 难以充分利用CPU资源                 | 可以充分利用CPU资源        |
| 内存轨迹大，数据局部性弱            | 内存轨迹小，数据局部性强   |
| 符合线性的编程思维                  | 不符合传统编程思维         |

异步读取文件

// readfile.js

```javascript
const fs = require('fs')
fs.readFile('./helloworld.js', 'Utf-8', (err, data)=> {
    if(err){
        console.log(err);
    }else{
        console.log(data);
    }
})

console.log('end');
// end
// console.log("%s: %d", "hello", 25);
```

同步读取文件

```javascript
const data = fs.readFileSync('./helloworld.js', 'utf-8')
console.log(data);
console.log('endd');
// console.log("%s: %d", "hello", 25);
// endd
```

#### 事件 EventEmitter

```javascript
const EventEmitter = require('events').EventEmitter
const event = new EventEmitter()
event.on('some_event', function () {
    console.log('sone_event occured');
})

setTimeout(()=> {
    event.emit('some_event')
}, 1000)

// sone_event occured
```

#### Nodejs的事件循环机制

![](..\img\node事件循环.jpg)



