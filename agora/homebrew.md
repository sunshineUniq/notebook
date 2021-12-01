```
- 安装
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install.sh)"
- 配置环境， 一般安装完会有提示
// 查看终端类型
 echo $SHELL
// /bin/bash => bash => .bash_profile
// /bin/zsh => zsh => .zprofile

 echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/xiaqin/.zprofile
 eval "$(/opt/homebrew/bin/brew shellenv)"
- 设置镜像
# brew
git -C "$(brew --repo)" remote set-url origin https://mirrors.ustc.edu.cn/brew.git

# core
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git

# cask
git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git

# bottles for zsh 和下面2选1
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/bottles' >> ~/.zprofile
source ~/.zprofile

# bottles for bash 和上面2选1
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/bottles' >> ~/.bash_profile
source ~/.bash_profile
```

