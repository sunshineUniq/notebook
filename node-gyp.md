node-gyp，是由于node程序中需要调用一些其他语言编写的 工具 甚至是dll，需要先编译一下，否则就会有跨平台的问题，例如在windows上运行的软件copy到mac上就不能用了，但是如果源码支持，编译一下，在mac上还是可以用的。node-gyp在较新的Node版本中都是自带的（平台相关），用来编译原生C++模块。

步骤：

1- 安装环境依赖

npm install --global --production windows-build-tools

　解释：　1、[python](https://www.python.org/downloads/)(v2.7 ，3.x不支持);

　　　　　　2、[visual C++ Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools),或者 （[vs2015](https://www.visualstudio.com/vs/community/)以上（包含15))

　　　　　　3、.net framework 4.5.1

2- 安装node-gyp

npm install -g node-gyp

3- 设置变量 npm_config_node_gyp

安装报错：if not defined npm_config_node_gyp

npm config set node_gyp "node C:\Users\me\AppData\Roaming\npm\node_modules\node-gyp\bin\node-gyp.js" 

这边设置成你的存放路径

