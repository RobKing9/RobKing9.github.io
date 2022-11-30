# Git的研究和使用总结


## Git的安装和配置

1. [下载Git](https://git-scm.com/download)

   ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E5%AE%89%E8%A3%85git.png)

2. 配置环境变量

   ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F.png)

3. 检验安装成功

   <img src="https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/version.png" style="zoom:150%;" />

4. 配置全局信息

   ```golang
   git config --global user.name "RobKing"  //用户名
   git config --global user.email "2768817839@qq.com"  //邮箱
   git config -l //查看全局信息
   ```

### 配置代理

- `git config --global https.proxy http://127.0.0.1:7890  //配置代理`
- `git config --global --unset http.proxy  //取消http代理` 

## Git指令的使用

- `git log`查看`commit`日志

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20log.png)

- `git log --oneline --graph --decorate --all`查看节点树

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20log%20tree.png)

- `git reset --hard commit_id`  回退到指定id （指定版本）

<img src="https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20reset.png" style="zoom:110%;" />

​	此操作结束之后 本地代码和远程仓库代码 都会回退到 原来的版本

- `git reset --hard origin/dev` 取消当前改动(回退指定id的改动），重置到库的最新版本（取消回退）

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E5%8F%96%E6%B6%88%E5%9B%9E%E9%80%80%E7%89%88%E6%9C%AC.png)

## 将项目上传到`Github`上

1. 进入`Github`首页，点击`New repository`新建一个项目（添加一个`Readme`）

2. 在项目的根路径下`git clone` + 项目名（下载指定分支 git clone -b dev ***）

3. 更新代码提交

   - `git add .`

     ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20add.png)

   - `git commit -m "first commit"`

     ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20commit.png)

   - `git push  origin master(main)`

     ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20push%20first.png)

## 本地项目与`Github`同步

### 添加`SSH KEY`

1. `ssh-keygen -t rsa -C “2768817839@qq.com”`

   ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/ssh%20key.png)

   成功生成`SSH key`了，可以到`C:/Users/`你的用户账号`/.ssh`文件夹下看

   `Linux`下可以`cd ~./ssh`

2. 复制`.ssh`文件夹下`id_rsa.pub`文件的内容添加到`github`

   ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/ssh%20github.png)

3. 测试`ssh`连接

   ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/ssh%20test.png)

### 关联本地库和远程库

- `git remote add origin git@github.com:RobKing9/CargoManageSystem.git` 

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20remote%20add.png)

- 如果`ssh`被占用 将导致或者如果项目是`http`协议

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20remote%20exist.png)

- 需要删除远程`git`仓库，执行`git remote rm origin`

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20remote%20rm.png)

- 执行指令 `git remote -v`查看当前情况

  

### 拉取最新代码

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/fetch.png)

参看版本差异可直接 `git log -p master`

## `Git`分支管理

- 将远程仓库的分支信息拉取到本地仓库`git fetch`

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20fetch%20fresh.png)

- 在本地创建新分支 `git branch [分支名]`

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20branch.png)

- 切换分支 `git checkout [分支名]`

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20switch.png)

- git branch 查看本地分支

- git branch -a 查看所有分支

- `git checkout -b main origin/main` 创建并切换分支

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20checkout.png)

- 删除分支

本地：`git branch -d master`

远程库：`git push -d origin master`或者`git push origin :master`

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20branch%20-d.png)

## `.gitignore`文件的使用

如果项目已经`push`上去了 但是没有忽略 ，增加 `.gitignore` 文件

`.gitignore`只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改`.gitignore`是无效的。

解决方法就是先把本地缓存删除（改变成未track状态），然后再提交:

- `git rm -r --cached .`

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/cache.png)

- 再次执行 `git add . -->git commit -m "update .gitignore" --> git push origin dev`

- ```
  *.a             表示忽略所有 .a 结尾的文件
  !lib.a          表示但lib.a除外
  /TODO           表示仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
  build/          表示忽略 build/目录下的所有文件，过滤整个build文件夹； .idea/
  doc/*.txt       表示会忽略doc/notes.txt但不包括 doc/server/arch.txt
   
  bin/:           表示忽略当前路径下的bin文件夹，该文件夹下的所有内容都会被忽略，不忽略 bin 文件
  /bin:           表示忽略根目录下的bin文件
  /*.c:           表示忽略cat.c，不忽略 build/cat.c
  debug/*.obj:    表示忽略debug/io.obj，不忽略 debug/common/io.obj和tools/debug/io.obj
  **/foo:         表示忽略/foo,a/foo,a/b/foo等
  a/**/b:         表示忽略a/b, a/x/b,a/x/y/b等
  !/bin/run.sh    表示不忽略bin目录下的run.sh文件
  *.log:          表示忽略所有 .log 文件
  config.php:     表示忽略当前路径的 config.php 文件
   
  /mtk/           表示过滤整个文件夹
  *.zip           表示过滤所有.zip文件
  /mtk/do.c       表示过滤某个具体文件
   
  被过滤掉的文件就不会出现在git仓库中（gitlab或github）了，当然本地库中还有，只是push的时候不会上传。
   
  需要注意的是，gitignore还可以指定要将哪些文件添加到版本管理中，如下：
  !*.zip
  !/mtk/one.txt
   
  唯一的区别就是规则开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中。为什么要有两种规则呢？
  想象一个场景：假如我们只需要管理/mtk/目录中的one.txt文件，这个目录中的其他文件都不需要管理，那么.gitignore规则应写为：：
  /mtk/*
  !/mtk/one.txt
   
  假设我们只有过滤规则，而没有添加规则，那么我们就需要把/mtk/目录下除了one.txt以外的所有文件都写出来！
  注意上面的/mtk/*不能写为/mtk/，否则父目录被前面的规则排除掉了，one.txt文件虽然加了!过滤规则，也不会生效！
   
  ----------------------------------------------------------------------------------
  还有一些规则如下：
  fd1/*
  说明：忽略目录 fd1 下的全部内容；注意，不管是根目录下的 /fd1/ 目录，还是某个子目录 /child/fd1/ 目录，都会被忽略；
   
  /fd1/*
  说明：忽略根目录下的 /fd1/ 目录的全部内容；
   
  /*
  !.gitignore
  !/fw/ 
  /fw/*
  !/fw/bin/
  !/fw/sf/
  说明：忽略全部内容，但是不忽略 .gitignore 文件、根目录下的 /fw/bin/ 和 /fw/sf/ 目录；注意要先对bin/的父目录使用!规则，使其不被排除。
  
  ```

  

## `git commit message` 编写指南

Head+Body+Footer  ；Head:
type 
• feat：新功能（feature）
• fix：修补bug
• docs：文档（documentation）
• style： 格式（不影响代码运行的变动）
• refactor：重构（即不是新增功能，也不是修改bug的代码变动）
• test：增加测试
• chore：构建过程或辅助工具的变动

scope
subject

## 使用`tree`命令生成项目目录树

1. 下载 `tree` 命令的二进制包，安装 `tree` 命令工具;[地址](http://gnuwin32.sourceforge.net/packages/tree.htm )，选择下载 `Binaries zip` 文件

2. 解压压缩包，找到压缩包内的 `bin` 目录，将 `bin` 目录下的 `tree.exe` 复制；

3. 找到`Git`的`Bin`目录，将 tree.exe 粘贴到该目录下，安装即完成

4. `tree -L 5 -I "node_modules|dist|dist.zip" >tree.txt` 将目录结构导出

   ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E7%9B%AE%E5%BD%95%E6%A0%91.png)

5. [参考链接](https://blog.csdn.net/sandy_sweet/article/details/84873053)

   

## 使用`Git`遇到的`Bug`及解决方法

### 解决git clone速度慢的方法

//这是我们要clone的

`git clone https://github.com/Hackergeek/architecture-samples`

//使用镜像

`git clone https://github.com.cnpmjs.org/Hackergeek/architecture-samples`

//或者使用镜像

`git clone https://git.sdut.me/Hackergeek/architecture-samples`

几个可用的镜像源

- `https://hub.fastgit.org](https://hub.fastgit.org/)`
- `https://github.com.cnpmjs.org](https://github.com.cnpmjs.org/)`
- `https://github.bajins.com](https://github.bajins.com/)`
- `https://github.rc1844.workers.dev](https://github.rc1844.workers.dev/)`

### 合并代码遇到error: Your local changes to the following files would be overwritten by merge

<img src="https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/20220725231147.png" style="zoom:120%;" />

#### 解决方法

- 执行`git stash` 本地刚才修改的代码将会被暂时封存起来

<img src="https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/stash" style="zoom:110%;" />

- `git merge origin/feature-feed-user` 重新合并

<img src="https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20merge.png" style="zoom:120%;" />

- `git stash pop`  服务器上的代码更新到了本地，而且你本地修改的代码也没有被覆盖

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/stash%20pop.png)

- [参考链接](https://blog.csdn.net/misakaqunianxiatian/article/details/51103734)

### 提交代码遇到To github.com:RobKing9/ByteGopher_SimpleDouyin.git ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'github.com:RobKing9/ByteGopher_SimpleDouyin.git'

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/git%20push%20error.png)

#### 解决方法

说明远程仓库的代码比本地先更新 遇到了冲突 无法提交 

- 首先把远程仓库最新的代码拉下来 （参考上面 本地项目与`Github`同步的拉取代码）

- 手动解决冲突 留下需要的代码 删除不需要的

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/%E8%A7%A3%E5%86%B3%E5%86%B2%E7%AA%81.png)

- 再次执行 `git add . -->git commit -m "" --> git push origin dev`

  ![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/20220725232317.png)

### git-修改commit信息

- [参考链接](https://blog.csdn.net/Muscleape/article/details/105637401)

### 添加远程仓库遇到fatal: unsafe repository ('D:/AGolang/src/Aproject/ByteGopher_SimpleDouyin' is owned by someone else)

![](https://raw.githubusercontent.com/RobKing9/Blog_Pic/master/Git/20220725235414.png)

#### 解决方法

- `git config --global --add safe.directory *`
- [参考链接](https://blog.csdn.net/qq_38292379/article/details/124613747)

