# Mac使用指南


# Mac使用指南



## 系统快捷指令

- `cmd+shift+4`截图
- `Option-Command-Esc`强制退出 App
- `Command-M`将最前面的窗口最小化至“程序坞”。要最小化最前面的 App 的所有窗口，请按 `Option-Command-M`。
- `Command-Tab`在打开的 App 中切换到下一个最近使用的 App
- `cmd+Q`退出程序(所有窗口)；`cmd+W`退出该窗口(相当于按到窗口的x)
- `cmd+N`新建一个窗口，包括Google浏览器，终端，finder
- `ctrl+cmd+F`全屏
- `Command + H `隐藏(Hide)当前正在运行的应用程序窗口。
- `Ctrl+cmd+.`在finder中输入指令可以显示隐藏的文件
- `ifconfig | grep "inet"`查看ip地址，inet的第一个ip就是，不是后面的broadcast 

## Item快捷键

在keys中配置ESC

- `ctrl+a`移动到行首；`+e`移动到行尾
- `ctrl+u`删除光标之前的所有字符；`+k`光标之后的所有
- `opt+f`向后跳一个单词；`+b`向前跳一个单词

## Google浏览器快捷键

- `cmd+W`关闭当前页面
- `cmd+↕️`箭头是回到顶部和底部
- `cmd+L`光标指向地址栏
- ctrl+tab下一个页面；`+shift`上一个页面

## Typora快捷键

- `option+cmd+U`无序列表，+O是有序；+X任务列表
- `cmd+数字`几级标题
- `cmd+option+C`插入代码块
- `cmd+F`查找；再`+option`查找替换
- `cmd+opt+T`插入表格
- `cmd+K`插入链接

## Goland快捷键

- `cmd+R`查找替换，`+F`是查找
- `cmd+E`最近打开的文件
- `cmd+Shift+U`大小写转化
- `Alt+Shift`对比最近修改的代码
- `cmd+c`复制当前行，`cmd+D`复制行到下一行，`cmd+x`剪切删除
- `cmd+`展开代码，`cmd-`折叠代码

## VSCode快捷键

- `cmd+,`打开设置
- `cmd+Shift+F`全局文件查找内容，`cmd+P`查找文件
- 文件内`cmd+F`查找，`cmd+opt+F`查找替换
- `cmd+Shift+Y`打开debug终端，其实就是打开终端，因为终端没有快捷键

## 网页版飞书快捷键

- `cmd+Shift+8`无序列表
- `cmd+opt+数字` 几级标题

## 重要程序

### Homebrew

安装

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

卸载

```shell
$ cd `brew --prefix`
$ rm -rf Cellar
$ brew prune
$ rm `git ls-files`
$ rm -r Library/Homebrew Library/Aliases Library/Formula Library/Contributions
$ rm -rf .git
$ rm -rf ~/Library/Caches/Homebrew
```

- 查看Homebrew版本 `brew -v`

- 更新Homebrew `brew update`

- 查询可用包 `brew search <packagename>`

- 安装任意包 `brew install <packagename>` 比如说可以按照 `git`，`mysql`，``

  ```
  安装的程序包所在位置
  1.配置文件在/usr/local/etc中
  2.安装文件在/usr/local/Cellar中
  3.二进制可执行程序的软连接在/usr/local/bin中
  ```

- 查找安装软件的路径 `brew list <packagename>`

- 卸载任何包 `brew uninstall <packagename>`

- 查看已安装包列表 `brew list`

- 查看任意包信息 `brew info <packagename>`

- 更新go语言版本 

/usr/local/等系统目录下的文件读写是需要系统root权限的,导致有些指令需要添加sudo前缀来执行,两种解决方式

1. 对/usr/local 目录下的文件读写进行root用户授权 `$ sudo chown -R $USER /usr/local`
2. 安装Homebrew时对安装路径进行指定，直接安装在不需要系统root用户授权就可以自由读写的目录下

```shell
<install path> -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```



## 参考资料

- [Homebrew介绍和使用](https://www.jianshu.com/p/de6f1d2d37bf)
- [homebrew安装的文件在哪？怎么查看？已解决]

