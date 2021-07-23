# Git是什么

## Git和其他版本控制工具的区别

- Git直接记录快照，而非差异比较
- Git近乎所有操作都是本地操作
- Git保证完整性（Git 中所有的数据在存储前都计算校验和，然后以校验和来引用）
- Git一般只添加数据（ 你执行的 Git 操作，几乎只往 Git 数据库中 **添加** 数据）

## Git的三种状态

-  **已提交（committed）：**已提交表示数据已经安全地保存在本地数据库中。
-  **已修改（modified）：**已修改表示修改了文件，但还没保存到数据库中。
-  **已暂存（staged）：**已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。



所以，Git项目有三个工作区:

1. 工作区
2. 暂存区
3. Git区



基本的 Git 工作流程如下：

1. 在**工作区**中修改文件。
2. 将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到**暂存区**。
3. 提交更新，找到暂存区的文件，将快照永久性存储到 **Git 仓库**。



## Git命令行

### 获取帮助

```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>
```

For example：获取git config 相关命令

```
$ git help config
```



### 获取Git仓库通常有两种获取 Git 项目仓库的方式：

1. 将尚未进行版本控制的本地目录转换为 Git 仓库；
2. 从其它服务器 **克隆** 一个已存在的 Git 仓库。



### 在已存在目录中初始化仓库： 

Windows上：先进入项目目录

```
 $ /c/user/my_project
```

 然后

```
$ git init
```

​	该命令将创建一个名为 `.git` 的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干.

​	但是，在这个时候，我们仅仅是做了一个初始化的操作，你的项目里的文件还没有被跟踪。

​	如果在一个已存在文件的文件夹（而非空文件夹）中进行版本控制，你应该开始追踪这些文件并进行初始提交。 可以通过 `git add` 命令来指定所需的文件来进行追踪，然后执行 `git commit` ：

```
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```



### 克隆现有的仓库

 克隆仓库的命令是 `git clone <url>` 。 比如，要克隆 Git 的链接库 `libgit2`，可以用下面的命令：

```
$ git clone https://github.com/libgit2/libgit2
```

这会在当前目录下创建一个名为 “libgit2” 的目录，并在这个目录下初始化一个 `.git` 文件夹， 从远程仓库拉取下所有数据放入 `.git` 文件夹，然后从中读取最新版本的文件的拷贝。 如果你进入到这个新建的 `libgit2` 文件夹，你会发现所有的项目文件已经在里面了，准备就绪等待后续的开发和使用。



## Git基础：记录每次更新到仓库

工作目录下的每一个文件都不外乎这两种状态：**已跟踪** 或 **未跟踪**。



**已跟踪**的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后， 它们的状态可能是未修改，已修改或已放入暂存区。简而言之，**已跟踪的文件就是 Git 已经知道的文件**。



其余所有都是未跟踪文件，它们既不存在于上次快照的记录中，也没有被放入暂存区。 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态，因为 Git 刚刚检出了它们， 而你尚未编辑过它们。



### 检查当前文件状态

```
$ git status
```

新创建一个readme文件，使用`git status`，他是untracked状态

### 跟踪新文件 

```
$ git add README
```

也可以通过`$ git add * `将所属目录下的所有文件跟踪

之后， 你修改其中的一个文件，再使用`$ git status`

会发现他会显示该文件已经被`modified`

### 暂存已修改的文件

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.txt
```

此时，Changes not staged for commit的意思是**已跟踪文件的内容发生了变化，但还没有放到暂存区。** 要暂存这次更新，需要运行 `git add` 命令。 这是个**多功能命令**：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。



将这个命令理解为“精确地将内容添加到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。



`$ git commit`的文件是`$ git add`后的文件，所以，运行了`$ git add`后又修改过的文件，需要重新`$ git add`



### 状态简览

```
git status -s
```

打印结果：

```
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt  

??:新添加的未跟踪文件
A:新添加到暂存区中的文件
M:修改过的文件

状态栏有两栏，左栏指明了暂存区的状态，右栏指明了工作区的状态
例如，上面的状态报告显示： README 文件在工作区已修改但尚未暂存，
而 lib/simplegit.rb 文件已修改且已暂存。 
Rakefile 文件已修，暂存后又作了修改，
因此该文件的修改中既有已暂存的部分，又有未暂存的部分。
```

### 忽略文件

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。

  在这种情况下，我们可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件的模式。 来看一个实际的 `.gitignore` 例子：

```
$ cat .gitignore
*.[oa]
*~
```

 第一行告诉 Git 忽略所有以 `.o` 或 `.a` 结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的。 第二行告诉 Git 忽略所有名字以波浪符（~）结尾的文件，许多文本编辑软件（比如 Emacs）都用这样的文件名保存副本。 



再看几个例子

```
# 忽略所有的 .a 文件
*.a

# 但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
!lib.a

# 只忽略当前目录下的 TODO 文件，而不忽略 subdir/TODO
/TODO

# 忽略任何目录下名为 build 的文件夹
build/

# 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
doc/*.txt

# 忽略 doc/ 目录及其所有子目录下的 .pdf 文件
doc/**/*.pdf
```

### 提交更新

```
$ git commit
```

### 跳过使用暂存区域

i.e. 跳过使用` $ git add `

因为这样看起来略显繁琐 

Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤

### 移除文件

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。 可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。



删除缓存区所有文件命令

```
git rm -r --cached .   #主要这个点一定要写
```



### git pull git fetch的区别

https://blog.csdn.net/weixin_41975655/article/details/82887273?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=1328689.11363.16165884492219105&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control