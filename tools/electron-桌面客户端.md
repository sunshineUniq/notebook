`electron` 模块所提供的功能都是通过命名空间暴露出来的

`electron.app`负责管理Electron 应用程序的生命周期

`electron.BrowserWindow`类负责创建窗口。

```react
const { app, BrowserWindow } = require('electron')
function createWindow () {   
  // 创建浏览器窗口
  let win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true
    }
  })
  // 加载index.html文件
  win.loadFile('index.html')
}
app.on('ready', createWindow)
```

#####  `main.js` 中创建窗口，并处理程序中可能遇到的所有系统事件

启动项目出现报错

```bash
  throw new Error('Electron failed to install correctly, please delete node_modules/electron and try installing again')
```

翻遍了资料都解决不了，自闭了！！！

最终的解决方案：

```
npm i electron-fix
electron-fix start 
```

使用electron-fix 帮忙下载electron成功后重新启动项目成功了，想哭