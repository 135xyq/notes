# 文件IO

## [fs文件系统](http://nodejs.cn/api/fs.html)

内置模块

###  readFile(path,[, options], callback) 

异步地读取文件的全部内容，有回调函数。得到的是字节，可以使用toString('utf-8')将其编码成正常字符串;还可以在第二个参数进行配置如‘utf-8',直接可以得到字符串。

```js
// test.txt  :  I am a Chinese.

读取test.txt文件内容

const path = require('path');
const fs = require('fs');

const filename = path.resolve(__dirname, './test.txt');

fs.readFile(filename, (error, content) => {
    console.log(content);
    console.log(content.toString('utf-8'))
})

输出：<Buffer 49 20 61 6d 20 61 20 20 43 68 69 6e 65 73 65 2e>
	I am a  Chinese.
```

###  fs.promises.readFile(path[, options])

异步地读取文件的全部内容，返回promise

```js

// test.txt  :  I am a Chinese.

const path = require('path');
const fs = require('fs');

const filename = path.resolve(__dirname, './test.txt');

fs.promises.readFile(filename, 'utf-8').then((resp) => {
    console.log(resp)
})

输出：   I am a Chinese.

```

### fs.readFileSync(path[, options])

同步返回 path 的内容。(会导致JS运行阻塞，影响性能)

```js
// test.txt  :  I am a Chinese.

const path = require('path');
const fs = require('fs');

const filename = path.resolve(__dirname, './test.txt');


console.log(fs.readFileSync(filename, 'utf-8'))

输出： I am a Chinese.
```

### fs.promises.writeFile(file, data[, options])

写文件,默认会覆盖原来的内容；可以设置配置参数flag的值为 
-  a : 追加 ，在原有内容后面追加
-  w: 写；覆盖原有内容

```js

//test.txt:  I am a Chinese.
const path = require('path');
const fs = require('fs');

const filename = path.resolve(__dirname, './test.txt');

fs.promises.writeFile(filename, 'I am xyq!');

// test.txt: I am xyq!

```
### fs.stat(path[, options])

获取文件或目录的信息

- size: 占用字节
- atime：上次访问时间
- mtime：上次文件内容被修改时间
- ctime：上次文件状态被修改时间
- birthtime：文件创建时间
- isDirectory()：判断是否是目录
- isFile()：判断是否是文件


### fs.readdir 

获取目录中的文件和子目录

### fs.mkdir

创建目录

```js
//在当前目录创建1-5,5个目录

for (let i = 1; i <= 5; i++) {
    fs.promises.mkdir(path.resolve(__dirname) + `/${i}`);
}

```

### fs.exists

判断文件或目录是否存在