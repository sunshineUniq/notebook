- 脚手架：？

- 技术栈

  - react ^17.0.2 、typescript、express、docker、material-ui
  - 其他用到的node-modules
    - Backend
      - tsyringe（构造函数依赖性注入器）、reflect-metadata(ES7提案，在声明的时候添加和读取元数据--装饰器)
      - async-mutex(管理异步任务执行顺序)
      - body-parser(http请求体解析器，解析JSON、Raw、文本、URL-encoded格式的请求体)
      - dockerode(docker + nodejs)
      - ejs + @types/ejs + art-template(模板)
      - express +express-promise-router(express4 路由器的轻量级包装，允许中间件返回承诺）+express-validator（验证数据）+express-ws(实现websocket协议)
      - moment-timezone(时区处理类库)
      - multer(nodejs中间件，处理表单提交数据,主要用于上传文件)
      - ncp(cli工具)
      - node-json-db(数据库)
      - set-interval-async（setInterval的现代版本，用于Promise和异步功能）
      - typescript-language-server(typescript和javascript语言服务器)
      - vscode-debugadapter + vscode-languageserver+vscode-ws-jsonrpc
      - websocket-stream（use websockets api)
      - winston(日志打印)
      - ws (websocket server and client)
      - yaml(写配置文件的语言)
    - frontend
      - @antv/x6 + @antv/x6-react-shape 用于在react中画流程图关系图等
      - @codingame/monaco-jsonrpc 利用websocket实现jsonrpc客户端和服务端的通信
      - @material-ui/core + @material-ui/icons + @material-ui/lab  ui组建库
      - @paciolan/remote-module-loader 远程加载commonjs模块
      - @vscode/codicons 获取vscode的图标并将其转换成字体
      - chartjs HTML5图标工具 + react-chartjs-2 两者结合可以画饼状图
      - material-ui-nested-menu-item 组件
      - monaco-editor-core + monaco-languageclient + react-monaco-editor    monaco编辑器
      - prometheus-query 查询
      - react + react-router-dom
      - react-helmet 组件：管理对文档头的所有修改 meta  + react-iframe组件 引入iframe页面
      - reflect-metadata + tsyringe 
      - sortablejs 拖拽插件
      - ts-md5 md5加密
      - vscode-debugprotocol
      - xterm(标准虚拟终端) + xterm-addon-attach（支持web socket) + xterm-addon-fit + xterm-addon-web-links

- 项目目录

  - backend

  - common

  - frontend

    - withRouter： 把不是通过路由切换过来的组件中，将react-router 的 history、location、match 三个对象传入props对象上

    

  