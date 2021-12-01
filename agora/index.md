- 安装开发环境

  - vscode、node、git、python3.10 + pip、typora、xmind
  - 配置终端，vscode插件

- 项目运行

  - 配置ssh（公司和个人仓库）

  - git clone

  - npm i

  - 安装项目运行需要的环境

    - 需要安装docker（需要开通docker hub 账号, 密码是docker-hub 地址用户设置里的cli密码）

      ```
      docker login hub.agoralab.co
      docker pull hub.agoralab.co/server/apass_demo_server:5
      ```

    - Python 3.x (python多版本管理: pyenv, 不需要管理使用的时候指定python版本就可以了)

      ```shell
      python3.x -m pip install --upgrade pip
      pip3 install -U setuptools
      // pip3 install 'python-language-server[all]' 遇到超时的报错：修改超时时间
      pip --default-timeout=1000 install -U 'python-language-server[all]'
      ```

    - 安装Homebrew(mac安装包工具) https://zhuanlan.zhihu.com/p/90508170 （非必要）

    - 安装Java (不影响项目运行)

      

11-1 安装环境，运行项目

11-2 熟悉项目结构和技术栈，查漏补缺完善技术栈，明确具体工作内容

- 确认项目是否头部和侧边栏一直显示，根据路由切换container部分的内容 --- 路由分发
- resize 频繁触发有出现堆栈溢出--- 添加防抖和截流（list频繁触发）
- 组件重复build

装饰器的妙用 https://blog.csdn.net/qq_35561857/article/details/102643019

11-3 项目架构梳理, 业务功能熟悉

- 修改成路由分发
  - 项目结构调整 
    - 入口文件 index.tsx  Router包裹
    - 页面根组件 App.tsx  页面固定不动的元素都放到这个文件， 通过路由控制右侧内容（flex布局代替js高度计算， 去掉resize事件监听）
    - FunctionBar组件修改：添加路由跳转， functionBar 走配置
    - 路由分发走配置(未做，有bug， 路由更改组件没有更改，需要查看原因)
      - 解决堆栈一溢出的bug
      - 解决list重复调用的问题: ManageServiceDialog 组件默认加载，请求接口，didUpdate里面调用了这个接口所有只要组件渲染就会被调用，resize会触发组件重复渲染
- 熟悉代码

https://jira.agoralab.co/browse/RTE-125 开发

11-8 上午熟悉代码，梳理需求 下午开发menuItem组件开发（熟悉material-ui组件库的样式重定制）

11-9 继续开发menuItem （custom-icon, custom-menu-item, custom-menu-list) 使用menuList

11-10 上午熟悉项目业务，下午开发分组组件，完善menuList, FileExplore的icon配置功能

补充分组功能，菜单栏UI 更改（去掉home), 调整functionBar的UI

11-11 FileExplore的icon配置功能

- 文件夹支持不同的图标, 不同颜色
  - Box
    - folderType: "box"
  - Group
    - folderType: "group"
  - proc
    - folderType: "proc"
- 文件支持不同的图标， 不同颜色
- 右键菜单支持分组，子菜单，icon

字体颜色 #E1e1e1， 背景颜色：#1e1e1e

11-12 RTE-125 pr 合并代码添加build, 文件支持icon font

接入iconfont

11-15  https://jira.agoralab.co/browse/RTE-126  Service管理界面的优化

- 解决split-pan 拖拽堆栈溢出的问题，添加ErrorBoundary防止页面白屏

- 交互描述

  - 点击menu-bar 下拉窗

  - 点击service 弹窗-- list + create（删除+ select）

  - 创建service后需要更新list

    - 遇到的问题： 类组件如何使用context

    ```react
    组件名.contextType = contexName
    组件内部通过this.context获取
    ```

- 合并service弹窗
- 添加select选中效果和关闭弹窗重新打开默认选中的交互
- 输入serviceName后支持esc和enter快捷键
- addFetchLoading ui

11-16 pr 126

Delete : btn -> icon , hover时出现

点击选中整条代替select btn

service dropList. add blur hide 

add min-width to rightcontainer for show the file-explorer

11-17 127

Status-bar UI开发

11-18 add mobx and mobs-react to project for 响应式交互

File-explorer组件的功能

- service 和 file-explorer是怎么交互的？
  - 创建的container和选择的container
    - 利用的是context 的方法设置的

- 选择文件
  - 文件夹--获取子菜单 api folders
  - 文件-- 
    - 选择的文件需要在tabs里面展示
      - 选中过更新activeIndex
      - 没选中过push
    - 文件的内容需要在editor里面展示

- tabs
  - 展示打开过的文件列表
  - 选中的文件标记选中，展示内容

