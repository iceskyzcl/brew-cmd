# brew-cmd
Homebrew常用命令

## SYNOPSIS
```
brew --version
brew command [--verbose|-v] [options] [formula] …
```

## GLOBAL OPTIONS
1. `-q, --quiet`: Suppress any warnings.
2. `-v, --verbose`: Make some output more verbose.
3. `-d, --debug`: Display any debugging information.
4. `-f, --force`: Override warnings and enable potentially unsafe operations.

## COMMANDS
- `brew update`: Update Homebrew
- `brew list [formulae]`: 显示已安装formula
- `brew deps [--tree] (formulae|--installed)`: 显示依赖
- `brew missing [formulae]`: 检查缺失依赖
- `brew uses <formulae>`: 显示被依赖


- `brew search (text|/text/)`: 查找formula
- `brew info <formula>`: 显示formula信息
- `brew install <formula> [options …]`: 安装formula
- `brew reinstall <formula>`: 重装formula


- `brew outdated`: 显示过时期formula
- `brew upgrade [formulae [options …]]`: 更新formula


- `brew uninstall <formula>`: 卸载(当前版本)formula
- `brew cleanup [-n] [formula/cask …]`: 清理[查看]过时文件


- `brew pin <formulae>`: 固定formula版本
- `brew unpin <formulae>`: 取消固定formula版本


- `brew switch <formulae> <version>`: 切换formula版本
- `brew unlink <formulae>`: 停用formula
- `brew link <formulae>`: 启用formula


- `brew commands`: 显示Homebrew命令
- `brew info`: 显示Homebrew信息
- `brew doctor`: Homebrew自检
- `brew home`: 打开Homebrew网站
- `brew home <formulae>`: 打开formula网站


- `brew tap`: 显示已安装仓库
- `brew tap <user/repo>`: 安装仓库
- `brew untap <user/repo>`: 卸载仓库
- `brew update-reset [repositories]`: 重置仓库


- `brew cask [install | uninstall | list | info | cleanup | outdated | upgrade | doctor | home]`: Cask仓库

## Install own staff to the Cellar
```
$ cd foo-0.1
$ brew diy
./configure --prefix=/usr/local/Cellar/foo/0.1
$ ./configure --prefix=/usr/local/Cellar/foo/0.1
[snip]
$ make && make install
$ brew link foo
Linking /usr/local/Cellar/foo/0.1… 17 symlinks created
```
