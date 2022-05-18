### 命令

**clear** 清屏
**git config --global user.name 'xy'** 设置用户名
**git config --global user.email '18636313739@163.com'** 设置邮箱
**ll** 查看有什么文件(不包括隐藏文件)
**ll -la** 查看有什么文件(包括隐藏文件)
**git add 文件名** 添加文件到缓存区
**git commit -m '注释'** 提交文件到本地库
**git status** 查看本地仓库暂存区的文件状态(上传的没有)
{
**git log** 查看 git 提交的最近到最远的日志(**空格向下翻译** **b 向上翻页** 到尾页**q**退出)
**git log --oneline**
**git log --pretty=oneline** 更漂亮的历史日志
**git reflog** 带下标的历史日志
}
**git reset --hard 索引**前进或者后退到历史版本
**rm 文件名**删除本地某个文件(再执行一遍 add,commit 就可以删除缓存区和本地库里的了)
**cat 文件名**查看文件名
**mkdir 文件夹名** 创建文件夹

`别名`
**git remote -v**查看别名(别名就是你修改的库的地址)
**git remote add 别名称**给你的 git 设置别名(库地址或者常用命令)
**git remote rm 别名称** 删除 git 别名

`diff命令`
**git diff 文件名**比较本地和暂存区的文件不一致的地方(**git diff**可以比对所有的文件)
**git diff HEAD 文件名**比较暂存区和本地库文件不一致的地方(**git diff HEAD 历史索引 文件名**可以对比历史版本不一样的地方)

`分支`
**git branch -v** 查看分支
**git branch 文件名** 创建一个分支
**git checkout 分支名**切换到其他分支

`拉取`
**git clone 远程仓库地址**把远程仓库的克隆到本地
**git fetch 远程库地址 远程库的分支**拉取远程仓库
**git merge 想合并分支**把拉取的远程仓库合并到本地分支
**git pull**直接就合并到本地分支了

---

### 版本控制系统(回到以前的版本)

`集中式版本控制系统`
把代码放在一台云服务器中,公司每个人都可以在云服务器中下载代码上传
`分布式版本控制系统`
每个电脑就是一台服务器,把代码下载下来会把所有版本的代码镜像到电脑上

### git 原理

工作区—缓存区 命令**git-add**
缓存区—本地库 命令**git commit**

### 初始化本地仓库

一.创建一个 GitResp 文件夹
二.打开 git 终端(Git Bash Here)
三.设置用户名和邮箱
设置用户名:**git config --global user.name 'xy'**
设置邮箱:**git config --global user.email '18636313739@163.com'**
`进入本地仓库的文件(GitResp)使用 git`
`初始化 **git init** (.git 是隐藏文件夹)`
`查看.git 下的内容"ll"(.git 下的文件不要删除,不要胡乱修改)`
`在 GitResp 里放入你想要上传的文件(放在暂存区 GitResp)`
`想要上传的文件必须要在gitResp本地仓库里面`
四、把文件暂存到暂存区里**git add 文件名**
五、把暂存区里的内容提交到本地库里**git commit -m '可以写一些注释'**
**git status**查看 git 本地仓库各个文件的状态(是否上传)
**git log**查看提交的历史记录
**git reset --hard 索引**可以前进或回退到历史版本
**rm 文件名**删除本地某个文件(再执行一遍 add,commit 就可以删除缓存区和本地库里的了))
六、创建一个远程仓库
七、给 仓库地址 设置一个别名
**git remote -v**查看别名(别名就是你修改的库的地址)
**git remote add 别名称 命令或者库的地址**给你的 git 设置别名(库地址或者常用命令)
**git remote rm 别名称** 删除 git 别名
八、**git push 仓库地址 远程仓库分支名**把本地库上传到远程仓库
九、**git clone 远程仓库地址**把远程仓库的克隆到本地(1.初始化本地库.2.将远程仓库内容完整的克隆到本地、3.可以创建远程库的别名)

十、**git fetch 仓库地址 远程仓库分支名**抓取远程仓库想要合并的数据(只是将远程仓库的内容下载到本地，在文件里还是找不到的状体)
十一、**git checkout 仓库地址/远程仓库分支(默认的 master)** 查看拉取里的内容是否正确(使用 ll 查看有什么文件 cat 文件查看文件内容)
十二、**git merge 仓库地址 本地仓库分支**远程仓库更新的代码合并到本地(如果报不能合并不相关历史的错可以
**git merge xy master--allow-unrelated-histories**把两段不相干的 分支进行强行合并

### 加入团队

在云端仓库有一个设置进入拉别人进来，把链接给别人
别人登陆自己的 git 账号 把链接输入网址进入

### SSH 免密操作

进入到主目录当中在 c 盘里**cd ~**
git 执行命令，生成一个 SSH 目录**ssh-keygen -t rsa -C 18636313739@163.com**(三次确认回车就行)
在你的主目录里有一个 ssh 文件夹，打开里面的 id_rad.pub 复制
在 git 官网里头像里的设置找到 ssh 密钥复制进去

### 分支(可能一些代码还在试错阶段||团队可以并行开发,互不影响)

**git branch -v** 查看分支
**git branch 文件名** 创建一个分支
**git checkout 分支名**切换到其他分支
**git merge 想合并的分支**合并分支(合并分支的时候遇到冲突的时候认为去修改)

### 解决 push 到云端冲突，在团队协作中可能两个人修改了同一行代码

先把云端的拉取到本地，人为的去删除掉不想要的内容(他会把冲突的代码都写在文件夹里)
再重新 add commit(commit 的时候不能加文件名字要不 commit 失败) push

### 跨团队合作

一、先得到 A 公司远程库的地址
二、B 公司的人在自己 git 账号里复制 A 公司的地址放在网址栏进行 fork 的操作(有一个 fork 按钮)
三、B 公司的人修改完代码后进行 pull requests 操作