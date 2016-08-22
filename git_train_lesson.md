## 关于SVN与git搭配使用的思路
* 1、稳定版本工程使用svn管理，即svn上的版本是用于发布的版本，团队成员checkout该版本在本地；
* 2、团队成员本地安装git，window系统请到github上下载桌面安装软件安装，mac自行查找按照方法
> 附初级教程：http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
* 3、安装git完成后，打开git shell控制台

`
# 定位到工程根目录下
> cd projectDir
# 使用git init进行git仓库初始化
> git init
# 然后在该目录下新建.gitignore文件添加需要忽略的文件列表
============================================================
例：需要忽略.svn文件夹、build文件夹、所有的class文件
-----------------
# Folders
# .svn文件夹会自动忽略
.svn
build

# class files
*.class
============================================================
`

*************************************************
注：如果开始没有创建忽略文件清单，而执行了后面的添加于提交后，想忽略部分文件或目录
例：追加忽略log.log文件、所有.class为文件、build目录、main目录下的output文件夹
# 首先需要先创建忽略清单文件

# 然后需要清空需要忽略的对象在仓库的缓存记录
> git rm -r --cached log.log
> git rm -r --cached *.class
> git rm -r --cached build
> git rm -r --cached main/output

# 然后查看下状态，可以看到需要忽略的内容已经从仓库中删除了
> git status

# 然后提交
> git commit -m "追加忽略相关内容" 

*************************************************

然后
# 将文件需要管理的文件添加到暂存区
> git add *
# 对添加到暂存区的文件提交的仓库
> git commit -m "初始化git仓库，实现本地git管理"
# 对改稳定版本打上对应的版本标签，便于查找，比如当前版本为1.0
> git tag v1.0 

打标签是为了快速找到commit的版本编号

# 查看所有标签
> git tag
> 查看具体标签对应的版本信息
> git show v1.0


然后
# 创建用于开发的分支，确保不操作主分支“master”
> git branch feature
# 切换到新分支
> git checkout feature

# 或者直接 创建并且切换
> git checkout -b feature


这个时候就可以在feature分支上进行开发了，在这个分支上的修改可以执行添加到暂存区与提交到仓库，始终都是在这个分支上变化的

当这个开发分支的开发的内容开发测试完成后，需要发布，这时就可以将该分支合并到主分支“master”上
第一步
# 首先要将feature分支上的内容进行提交
# 先查看哪些内容需要提交
> git status
# 然后将需要提交的内容，添加到暂存区
> git add 需要提交的内容
# 最后执行提交
> git commit -m "提交log"

第二步
# 切换到主分支上
> git checkout master
# 将feature分支内容合并到master上，不建议使用这个命令快速合并“Fast-forward”
> git merge feature

# 最好使用这个命令进行合并，这样就可以在版本日志中看到相关的日志
> git merge --no-ff -m "合并log" feature

# 最后就可以删除feature分支
> git branch -d feature
# 在查看下分支
> git branch


第三步
# 在master分支上，进行发布版本的打包，然后给这个版本打上对应的版本标签比如v1.1
> git tag v1.1

第四步
将master分支内容提交到svn上，其他成员同步更新
# 这里是从svn更新下新内容时需要处理的
# 查看状态，哪些更新内容需要提交给git仓库
> git status
# 添加到暂存区
> git add 更新的内容
# 提交
> git commit -m "提交日志"


第五步
如果还有正在开发的分支，想与master保持同步，需要更新master分支内容
# 切换到具体分支，然后从master分支更新内容
> git merge --no-ff -m "从主分支上合并内容" master



bugs修复分支
master发布的版本存在bugs，但是现在已经在做dev分支上做开发，还没好，不能提交
# 查看当前分支状态
> git status
# 有内容未提交，这里可以使用命令将当前的工作现场进行保存，然后需要的时候可以恢复现场 完整命令 git stash save "message"
> git stash
# 在查看状态，发现已经干净，可以进行分支切换了
# 创建bugs分支 issue-001
> git checkout -b issue-001
# 现在就可以进行bugs修复，完成后提交、合并、删除分支、给master打标签，然后svn同步，与上面的步骤一样
# bugs修复完成后，要继续原来的开发，恢复前面保存的工作现场
# 先查看现场清单
> git stash list
# 恢复现场有两种方式pop 与 apply
# 按列表清单顺序pop出现场，同时删除，可执行多次
> git stash pop
# 恢复具体的现场编号
> git stash apply stash@{1}
# 然后删除具体的现场编号
> git stash drop stash@{1}



这里由于我们使用的是本地git仓库，只有我们自己在操纵，所以不会出现冲突问题，如果出现冲突，与svn差不多，也是要解决冲突，然后再提交，然后合并。




补充操纵：
1、查看日志的时候，需要使用q进行命令退出
2、现场恢复不管在那个分支上都可以进行恢复，这个恢复是需要在当前分支上，所以恢复现场需要注意下，需要在哪个分支上进行恢复，如果恢复错了，就再保存一次现场，然后切换到对应分支上进行恢复。
3、打包命令git archive 
4、从远程git仓库更新并且合并
    方式一：
    # 首先从远程的origin的master主分支下载最新的版本到origin/master分支上
    > git fetch origin master
    或者
    # 在对应的分支上直接
    > git fetch
    # 查看本地版本与远程版本的差异
    > git log -p master..origin/master
    # 确认后合并下载下来的远程版本到本地版本
    > git merge origin/master

    方式二：
    # 直接粗暴的从远程拉取最新版本
    > git pull origin master
    相当于方式一的fetch与merge的合并
5、从某个分支中更新具体某个文件
比如：在master分支中有一个test.txt文件需要同步到feature分支中
    # 切换到feature分支
    > git checkout feature
    # 将test.txt文件从master分支中取到feature
    > git checkout master -- test.txt
    # 然后就添加于提交
    > git add test.txt
    > git commit -m "从master更新test.txt文件"