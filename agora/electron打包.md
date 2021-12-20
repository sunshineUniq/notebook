Electron 目录下执行命令

方法一：默认所有依赖包都下一遍， 太慢

```
npm run package
```

 方法二：

在taobao npm 镜像上下载指定版本的electron到本地， 我的存放地址： ～/.electron/cache/

```
electron-packager . 'RTEStudio' --platform=darwin --arch=arm64 --electron-version=13.1.4 --overwrite --out=./out --electron-zip-dir=/Users/xiaqin/.electron/cache 
```

note： app包打开提示损坏执行

```
// xattr -cr ${RTEStudio.app path}
xattr -cr /path/to/RTEStudio.app
```



http服务分享本地文件

- 分享的文件目录下面

```bash
python -mSimpleHTTPServer
```

- 查看自己的ip

```
ifconfig
```

查找en0 找到ip地址

访问ip地址： 10.103.2.154：8000

"fileheader.tpl": "/**\r\n *\r\n * Agora Real Time Engagement \r\n * Created by {author} in {createTime}. \r\n * Copyright (c) 2015 Agora IO. All rights reserved. \r\n *\r\n */\r\n"

