- [Homebrew](#homebrew)
  - [Homebrew 的安装](#homebrew-的安装)
  - [Homebrew 自动更新](#homebrew-自动更新)
  - [Homebrew 相关路径](#homebrew-相关路径)
  - [Homebrew 常用命令](#homebrew-常用命令)
    - [搜索](#搜索)
    - [更新](#更新)
    - [列出已安装的包](#列出已安装的包)
    - [列出可以更新的包](#列出可以更新的包)
    - [锁定某个不想更新的包](#锁定某个不想更新的包)
    - [清理旧包](#清理旧包)
    - [查看已经安装包的依赖](#查看已经安装包的依赖)
    - [查看包的信息](#查看包的信息)
    - [包的安装、卸载、重装](#包的安装卸载重装)

# Homebrew


> Homebrew 是 macOS 和 Linux 上非常流行的开源包管理器，可以理解为一个命令行版本的应用商店。



## Homebrew 的安装

    $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

如果没有🪜可能很慢，可以使用国内的安装脚本

    $ /bin/bash -c "$(curl -fsSL https://mirrors.ustc.edu.cn/misc/brew-install.sh)"

安装完成之后，可以使用`brew -v`查看版本


    qintian@qintiandeMacBook-Pro ~ % brew -v
    Homebrew 4.4.27
    Homebrew/homebrew-core (git revision 7db08748b16; last commit 2023-04-13)
    Homebrew/homebrew-cask (git revision 57e86a7b59; last commit 2023-04-12)

## Homebrew 自动更新

默认情况下，在执行 `brew install`、`brew upgrade`、`brew tap` 之前，每隔第一段时间会自动执行 `brew update` 以获取最新的 Homebrew 版本。
在 4.0 起自动执行频率为 24h，如果开启了 HOMEBREW_NO_INSTALL_FROM_API=1 频率为 5min。可通过以下环境变量完全禁用、设置时间间隔。

    echo '
    export HOMEBREW_NO_AUTO_UPDATE=1
    export HOMEBREW_AUTO_UPDATE_SECS=86400
    ' >> ~/.zshrc

## Homebrew 相关路径

    # 显示 Homebrew 本地的 Git 仓库
    $ brew --repo

    # 显示 Homebrew 安装路径
    $ brew --prefix

    # 显示 Homebrew Cellar 路径
    $ brew --cellar

    # 显示 Homebrew Caskroom 路径
    $ brew --caskroom

    # 缓存路径
    $ brew --cache

Homebrew 默认安装路径如下：
- macOS ARM: /opt/homebrew
- macOS Intel: /usr/local

可以通过`uname -m` 查看 Mac 的硬件架构是 arm 还是 x86

以 `brew install git` 为例：

1. Homebrew 将 git 下载至 /usr/local/Cellar/git/<version>/ 目录下，其二进制文件在 /usr/local/Cellar/git/<version>/bin/git。
2. Homebrew 为 /usr/local/Cellar/git/<version>/bin/git 创建了一个软链文件至 /usr/local/bin 里。


macOS ARM 的路径对应是：

    /opt/homebrew/Cellar/git/<version>/
    /opt/homebrew/Cellar/git/<version>/bin/git
    /opt/homebrew/bin。
这也是 macOS ARM 要将 `/opt/homebrew/bin` 添加到 PATH 环境变量的原因。



当执行 `brew uninstall` 时，会将 `/usr/local/Cellar` 下对应包目录删除，对应的链接关系也会移除。 当执行 `brew cleanup` 时，会将 `/usr/local/Cellar` 所有包里的旧版本，只保留最新版本。

## Homebrew 常用命令

### 搜索

    $ brew search <keyword>			# 支持模糊搜索

### 更新

    $ brew upgrade                  # 更新所有已安装的包
    $ brew upgrade <package-name>   # 更新指定包

### 列出已安装的包

    $ brew list                     # 所有的软件，包括 Formulae  和 Cask
    $ brew list --formulae          # 所有已安装的 Formulae
    $ brew list --cask              # 所有已安装的 Casks
    $ brew list <package-name>      # 列举某个 Formulate 或 Cask 的详细路径

### 列出可以更新的包

    $ brew outdated			# 列出可以更新的包

### 锁定某个不想更新的包

    $ brew pin <package-name>       # 锁定指定包
    $ brew unpin <package-name>     # 取消锁定指定包

### 清理旧包

    $ brew cleanup                  # 清理所有旧版本的包
    $ brew cleanup <package-name>   # 清理指定的旧版本包
    $ brew cleanup -n               # 查看可清理的旧版本包

### 查看已经安装包的依赖

    $ brew deps --installed --tree		# 查看已经安装包的依赖

### 查看包的信息
    $ brew info <package>           # 显示某个包信息
    $ brew info                     # 显示安装的软件数量、文件数量以及占用空间

### 包的安装、卸载、重装
    $ brew install <package-name>    # 安装
    $ brew uninstall <package-name>  # 卸载
    $ brew reinstall <package-name>  # 重装

如安装的是 GUI 应用，加上 `--cask` 参数; 如需强制卸载，则加上 `--force`参数




使用 brew search 命令可以看到「Formulae」和「Casks」两类：
- Formulae：一般是那些命令行工具、开发库、字体、插件等不含 GUI 界面的软件。
- Casks：是指那些含有 GUI 图形化界面的软件，比如 Chrome、FireFox 等。



