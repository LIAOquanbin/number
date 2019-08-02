注意: Git 版本仓库的路径中不能包含任何中文
     如果使用windos电脑不要使用默认文本文档创建txt文件,因为Windows文本文档utf-8编码集有问题.推荐使用notepad++
创建版本库 $ git init
创建成功时: Initialized empty Git repository in E:/newproject/git/demo1/.git/
这时候我们看到 git bash 中显示路径 /e/newproject/git/demo1 (master) 多出一个 master 一段文字,代表当前git仓库所在分支名

当用户在git仓库中新建了文件或者是更新了某个文件都需要通过git命令将文件添加到git仓库中去

$ git add <file name> // 将指定文件添加值暂存区

$ git commit -m "一段当前文件更新描述"  // 将当暂存区的文件提交到当前分支中
                                      // -m是一个命令 用来描述为什么将本次文件提交到git版本库中
$ git status 查询git当前仓库的状态

$ git log   打印当版本仓库提交日志

$ git log --pretty=oneline 将版本日志一行展示

  git返回的结果:
  6a0d85755247503b829be522a70fb1abe8da7bde (HEAD -> master) readme add git log
  ad8889a15380ec5964eadcae56aa6557d59cedb8 readme.txt add new line git status
  92175ab96c0b33234d2dfc88a2d324ffd698143c create readme file
  日志中,前面一长串哈希编码是当前日志的commit id,是每个版本的身份证每个id都是不同的
  (HEAD -> master) 代表当前master分支现在所在的版本日志
  后面的文本就是用户提交文件到git仓库时 -m的那段提交描述

版本回退相关命令
$ git reset --hard HEAD^ 从当前日志版本后退一个版本(HEAD 后的^符号数量代表回退的版本数)
                         $ git reset --hard HEAD^^^ 从当前版本回退3个版本
我们发现上面的命令在回退版本时,尤其要回退多个版本是很麻烦,所以git提供了一个根据commit id跳转到指定日志版本的命令
$ git reset --hard <commit id>      // eg. $ git reset --hard 6a0d8 TODO:commit id 不需要全写只需要写前6位左右就可以了

TODO: 我们发现 git只能打印当前日志之前的所有日志,有时候我们回退版本后电脑关机了,下次开机我们又后悔回退了版本,这时候打印log又无法显示回退之前的版本号
解决方法 $ git reflog 这个命令可以打印出当前版本仓库中用户的所有操作日志,可以操作日志中找到回退之前的对应日志的版本号

撤销操作的方法
  $ git checkout -- <filename> 当文件还未被添加到暂存区时,可以通过此命令让指定文件的内容回退到上一次提交的版本
  如果用户已经把内容提交到了暂存区 只能通过
  $ git reset HEAD <filename> 删除已经添加到暂存区的指定文件

将删除文件操作添加到暂存区的方法
 $ git rm <filename>