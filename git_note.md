# 初始化配置

```shell
git config --global user.name "Nikola Tesla"
git config --global user.email "1428303624@qq.com"
git config --global credential.helper store
```

参数说明

```shell
省略(local): 本地配置，只对本地仓库有效
--global: 全局配置，对所有仓库有效
--system: 系统配置，对所有用户有效
```

# 新建仓库(repository)

repository abbreviation: repo

在电脑本地直接创建一个仓库：

```shell
git init
```

从远程服务器上clone一个已经存在的仓库：

```shell
git clone https/ssh
```

# 工作区域

## 工作区

## 暂存区

## 本地仓库

# 添加和提交文件

```shell
git init		// 创建仓库
git status		// 查看仓库状态
git add			// 添加到暂存区
git commit		// 提交
git commit -m "提交信息"
# 一个命令完成暂存和提交两个动作
# -a 这个参数只对已跟踪的文件有效
# 未跟踪的文件仍需要手动先 add 后 commit
# -a -m 也可以写成 -am
git commit -a -m "提交信息"
```

# 回退版本

```shell
git reset --soft		// 回退到某一版本，并保留工作区和暂存区的所有修改内容
git reset --hard		// 回退到某一版本，并丢弃工作区和暂存区的所有修改内容
git reset --mixed		// 默认情况，回退到某一版本，只保留工作区的修改内容，丢弃暂存区的修改内容
git reset HEAD^			// --mixed 回退上一版本
git reset [版本号]		// --mixed 回退到版本号的版本
git log				// 查看之间的版本（完整版）
git log --oneline	// 快速查看之前的版本，只包括版本号和提交信息
```

# 查看差异

```shell
git diff				// 不加参数默认比较工作区和暂存区的差异
git diff HEAD			// 比较工作区和版本库之间的差异
git diff --cached		// 比较暂存区和版本库之间的差异
git diff <commit_hash> <commit_hash>	// 比较两个版本之间的差异
git diff <branch_name> <branch_name>	// 比较两个分支之间的差异
/***************example***************/
git diff HEAD~ HEAD		// 比较当前版本和上一版本之间的差异
git diff HEAD~2 HEAD	// 比较当前版本和上数两个版本之间的差异
git diff 5af90b8~ 5af90b8	// 比较5af90b8和5af90b8的上一个版本之间的差异
git diff HEAD~ HEAD file_3.txt	// 比较当前版本和上一个版本中file_3.txt之间的差异
```

除了使用版本ID外，还可以使用HEAD来表示当前分支的最新提交。HEAD指向分支的最新提交节点。我们也可以使用某一个版本的提交ID和HEAD来进行比较。HEAD^和HEAD~均可以表示上一个版本。HEAD~index表示HEAD往前数index个版本。同时，~和^也可以用在版本号后面。

注：比较新老版本之间差异时，把老版本放前面，新版本放后面，可以看到相较于老版本，新版本删去了什么，增加了什么。

# 从版本库中删除文件

## 直接删除文件之后添加到暂存区后提交

```shell
rm -i file_1.txt
git add file_1.txt
git commit
```

## 使用git rm命令同时删除工作区和暂存区的文件后再提交

``` shell
git rm file_2.txt
git rm --cached <file>		// 把文件从版本库和暂存区中删除，但保留在当前工作区
git rm -r <dir>			// 递归删除某个目录下的所有子目录和文件
```

使用`git rm`命令删除后不要忘记提交

# .gitignore文件

这个文件的作用是让我们可以忽略一些不应该被加入到版本库中的文件（让这些文件不被纳入到版本控制考虑的范围内），这样可以让我们的仓库体积更小，更干净。

一般情况下应该忽略的文件：

1. 系统或软件自动生成的文件
2. 编译产生的中间文件和结果文件，比如Java编译生成的.class文件、C编译生成的.o文件。
3. 运行时生成的日志文件、缓存文件、临时文件
4. 涉及身份、密码、口令、密钥等敏感信息的文件

忽略规则：

* 在.gitignore文件中列出想要忽略的文件的格式。 

github中列出了常用编程语言的.gitignore文件模板，可以直接下载，在此基础上修改使用。网址：[github/gitignore: A collection of useful .gitignore templates](https://github.com/github/gitignore)

## .gitignore文件的匹配规则

* 空行或者以#开头的行会被Git忽略。一般空行用于可读性的分隔,#一般用作注释
* 使用标准的Blob模式匹配,例如:
  * 星号*通配任意个字符
  * 问号?匹配单个字符
  * 中括号[]表示匹配列表中的单个字符，比如: [abc]表示a/b/c
  * 两个星号**表示匹配任意的中间目录
  * 中括号可以使用短中线连接,比如:
    * [0-9]表示任意一位数字,[a-z]表示任意一位小写字母
  * 感叹号!表示取反

### example

```
# 忽略所有的 .a 文件
*.a

# 但跟踪所有的 lib.a，即便你在前面忽略了.a文件
!lib.a

# 只忽略当前目录下的TOD0文件，而不忽略 subdir/TODO/
/TODO

# 忽略任何目录下名为build 的文件夹
build/

# 忽略doc/notes.txt，但不忽略doc/server/arch.txt
doc/*.txt

# 忽略doc/目录及其所有子目录下的.pdf文件
doc/**/*.pdf
```

# ssh和clone repository

```shell
# 生成ssh key
ssh-keygen -t rsa -b 4096 -C "xxxxxxxx@gmail.com"

# 克隆远程仓库
git clone <repo-address>

# 推送更新内容
git push <remote> <branch>

# 拉取更新内容
git pull <remote> 
```

# 关联本地仓库和远程仓库

```shell
# 将远程仓库起一个别名和本地仓库关联起来
git remote add <shortname> <url>

# 查看当前仓库对应的远程仓库的别名和地址
git remote -v

# 指定主分支的名称为main
git branch -M main

# 将本地的main分支和远程仓库的main分支关联起来
git push -u origin main:main
git push -u <远程仓库名> <远程分支名>:<本地分支名>

# 拉取远程仓库的修改内容
# 作用：把远程仓库的指定分支拉去到本地再合并
# 如果远程仓库中的修改内容和本地的内容有冲突的话，合并操作会因为冲突而失败，此时需要手动解决冲突
git pull <远程仓库名> <远程分支名>:<本地分支名>

# 获取远程仓库的修改，不合并
git fetch 
```

# Gitee的使用和GitLab本地化部署

Geek Hour视频参考：

[13.Gitee的使用和GitLab本地化部署](https://www.bilibili.com/video/BV1HM411377j?p=13&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)

# GUI工具

Git官网介绍了常用的GUI工具：

[Git - GUI 客户端 - Git 中文](https://git.js.cn/downloads/guis)

# 在VsCode中使用Git

VsCode中集成了源代码管理器，基本操作可参看视频链接：

[15.在VSCode中使用Git](https://www.bilibili.com/video/BV1HM411377j?p=15&spm_id_from=pageDriver&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)

# 分支简介和基本操作

```shell
# 查看所有分支
git branch

# 创建新分支
git branch <分支名>

# 切换分支
git checkout <分支名>

# 因为git checkout 命令除切换分支外还用于恢复文件
# 当分支名与文件名相同时会出现歧义
# 此时默认会切换分支而不是恢复文件
# 为避免这种问题，Git官方在2.23版本开始提供一个新命令git switch 专门用于切换分支
git switch <分支名>

# 合并分支
# 将<分支名>的分支合并到当前分支中
# 合并后会默认产生一次commit过程
git merge <分支名>

# 查看分支图
git log --graph --oneline --decorate --all

# 删除已经被合并的分支
# 删除分支的操作不会显示在分支图中，只能用git branch命令查看现有的分支进行判断
git branch -d <branch-name>

# 删除未合并的分支(不再被需要的功能)，强制删除
# 删除分支的操作不会显示在分支图中，只能用git branch命令查看现有的分支进行判断
git branch -D <branch-name>

# 恢复某个已经删除的分支
git checkout -b <branch> <branch-ID>
```

# 解决合并分支时的冲突

一般情况下，如果两个分支的修改内容没有重合的部分的话，Git会自动完成合并。

但如果两个分支修改了同一个文件的同一行代码，Git就不知道应该保留哪个分支的修改内容了，也就产生了冲突，这个时候就需要我们手动来解决冲突。

总结：

- 两个分支未修改同一个文件的同一处位置：Git自动合并

- 两个分支修改了同一个文件的同一处位置：产生冲突

- 解决方法:
  - Step1 - 手工修改冲突文件，合并冲突内容
  - Step2 - 添加暂存区	`git add <file-name>`
  - Step3 - 提交修改	`git commit -m "message"`

- 中止合并：当不想继续执行合并操作时可以使用下面的命令来中止合并过程:	`git merge --abort`

# 回退和rebase

rebase	变基

```shell
# 将当前分支的所有内容变基到目标分支
# 找到两个分支开始分开的节点
# 从此节点开始的所有分支内容
# 移植到目标分支后面
git rebase <target-branch>

# 恢复某个已经删除的分支
# 此时被恢复的分支会重新出现
# 并不影响其他分支的内容
# 其他分支并不会跟着回滚
git checkout -b <branch> <branch-ID>

# 想要当前分支回滚可以切换到当前分支
# 使用git reset命令回滚
git reset --hard <branch-ID>
```

# Rebase 和 Merge 有什么区别，如何区分使用？

## Merge

优点：

- 不会破坏原分支的提交记录，方便回溯和查看

缺点：

- 会产生额外的提交节点，分支图比较复杂。

## Rebase 

优点：

* 不会新增额外的提交记录，形成线性历史，比较直观和干净。

缺点：

* 会改变提交历史，改变了当前分支branch out的节点。避免在共享分支上使用。

# 分支管理和工作流模型

工作流模型：一些比较好的规范和流程，可以让我们的工作更高效，更有条理。

常见的工作流模型有：GitFlow模型和GithubFlow模型等。

GeekHour视频参考：

[19.分支管理和工作流模型](https://www.bilibili.com/video/BV1HM411377j?p=19&spm_id_from=pageDriver&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)