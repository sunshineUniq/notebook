# 新mac需要安装的软件

```
node
vscode vscode插件： CSS Peek，   Open-In-Browser Prettier  SVG Viewer  TODO Highlight  Themes
```





# Mac 配置命令行打开vscode

```
vscode
- 在vscode安装code命令
command + shift + P
选择shell Command: Install 'code' command in PATH
```



## MAC 配置命令别名

```shell
echo $SHELL
# /bin/zsh
# 如果不是上面的路径
chsh -s /bin/zsh
touch .zshrc
open ~/.zshrc
# 添加下面配置
cd /Users/sunshine/Desktop/
alias gpr='git pull --rebase'
alias gck='git checkout'
alias gpp='git push private HEAD:dev'
alias desk='cd /Users/sunshine/Desktop'
alias root='cd ~'

source .zshrc
```

扩展：windows

git bash 

```
vim ~/.bash_profile

在文件里配置别名即可
alias open="explorer"

esc=>:wq=>enter
source ~/.bash_profile
```

