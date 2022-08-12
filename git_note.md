> ```
> Author:lgx
> Date:2022.08.12 11:31:21
> Email:geniuslgx@mail.ustc.edu.cn 
> 说明：[可选参数]  <必要参数>  a/b表示a或b
> ```

# 1. 仓库管理
>初始化、克隆、删除
## 1.1 git init

>```
>git init [local_path]
>```
>在下local_path/生成.git文件夹，local默认为当前目录。.git文件下包含分支信息等。

## 1.2 git clone

>```
>git clone <url>.git [local_path]
>```
>克隆url中的仓库到本地local_path，local默认为当前目录

## 1.3 删除仓库
>直接删除.git文件夹
## 1.4 仓库配置
>添加邮箱与用户名、代理、设置缓冲大小
### 1.4.1 添加邮箱与用户名
>```
>git config --global user.email "624120638@qq.com"
git config --global user.name "lgx"
>```
### 1.4.2 添加代理
>将本地1080端口添加为代理
>```
>git config --global http.proxy http://127.0.0.1:1080
>git config --global https.proxy https://127.0.0.1:1080
>```
### 1.4.3 设置缓冲区大小
>一次性添加的文件太多，超过缓冲大小，无法上传remote
>
>设置缓冲区大小为1GB：
>
>```
>git config --global http.postBuffer 1048576000
>```
# 2.修改与提交
>添加、删除、恢复、对比、提交、日志
## 2.1 git add 
>```
>git add <file1/dir1> [file2/dir2] …
>```
> 添加文件或文件夹到 <font color="#ff0000">**暂存区**</font>。支持<font color="#ff0000">**通配符**</font>，如*.png

## 2.2 git rm

> ```
> git rm [-rf] <file1/dir1> [file2/dir2] …
> ```
>
> 删除<font color="#ff0000">**工作区**</font>和<font color="#ff0000">**暂存区**</font>中的文件或文件夹。支持<font color="#ff0000">**通配符**</font>，如*.png
>
> 如果是手工(rm)删除文件，<font color="#ff0000">**只会删除工作区**</font>中的文件
>
> git mv 与mv 原理与上相同
## 2.3 git restore

> ```
> git restore [-staged] <file1/dir1> [file2/dir2] …
> ```
>
> 恢复<font color="#ff0000">**手动(rm)**</font>删除的<font color="#ff0000">**工作区**</font>文件
>
> <font color="#ff0000">**--staged**</font>，恢复git rm 删除的<font color="#ff0000">**暂存区**</font>的文件
>
> 先恢复暂存区，再恢复工作区

## 2.4 git diff

> ```
> git diff [file1/dir1] [file2/dir3] …
> ```
>
> 查看<font color="#ff0000">**暂存区**</font>文件/文件夹与<font color="#ff0000">**工作区**</font>的区别，暂存区中必须要有该文件才能比较。
>
> 新建文件后，应该通过git add 加入暂存区，方便后续比较。

## 2.5 git commit

> ```
> git commit [file1/dir1] [file2/dir3] … -m message
> ```
>
> 将<font color="#ff0000">**暂存区**</font>的文件/文件夹提交到<font color="#ff0000">**本地**</font>。
>
> <font color="#ff0000">**切换分支前**</font>前，一定要git commit

## 2.6 git status

> ```
> git status [file1/dir1] [file2/dir3]
> ```
>
> 比较<font color="#ff0000">**暂存区**</font>与<font color="#ff0000">**本地仓库**</font>的区别

## 2.7 git log

> ```
> git log
> ```
>
> 查看git commit的历史信息

## 2.8 git revert

> ```
> git revert <commit_id>
> ```
>
> 回退到commit_id时的环境

## 2.9 git show

> ```
> git show [commit_id]
> ```
>
> 查看指定commit_id的变动信息

# 3. 分支

> 添加、删除、重命名、合并

## 3.1 git branch

> ```
> git branch [-d/D][-m/M new_name][branch_name] 
> ```
>
> 查看所有分支，或者新建branch_name分支
>
> -d/D 删除branch_name分支
>
> -m/M 重命名当前分支

## 3.2 git checkout/switch

> ```
> git checkout/switch <branch_name>
> ```
>
> 切换到branch_name分支

## 3.3 git merge

> ```
> git merge <branch_name>
> ```
>
> 将brach_name分支，合并到当前分支
>
> merge原则：
>
> - 在main分支中输入`git branch b1` 创建b1分支，b1分支中会带有main分支中的所有文件，在b1分支中对这些文件修改、删除，最终合并到main分支中，也会对应修改、删除
> - b1分支中新建的文件，merge main分支和被main分支merge时，都会保留
> - main分支中新建的文件，merge b1分支和被b1分支merge时，都会保留
> - 若b1分支和main分支中，新建的文件名一样，则merge时会产生冲突

# 4. 远程

> 添加删除远程仓库、推送、拉取

## 4.1 git remote

>```
>git remote [-v][add shortname url][rm/remove shortname][rename old_name new_name]	
>```
>
>-v： 查看现有远程仓库
>
>add：将url取别名为shortname，并作为远程仓库
>
>rm/remove：删除远程名为shortname的远程仓库
>
>rename：将名为old_name的远程仓库重命名为new_name

## 4.2 git fetch

> ```
> git fetch <shortname><branch_name>
> ```
>
> 将远程仓库shortname中的branch_name分支的commit的信息放入<font color="#ff0000">**FETCH_HEAD**</font>中
>
> 可通过`git log FETCH_HEAD`来查看所获取分支的commit信息
>
> 可通过`git merge FETCH_HEAD`来merge所获取的分支 

## 4.3 git pull

> ```
> git pull <shortname> < remote_branch >[:local_branch]
> ```
>
> 如果local_branch== remote_branch，则remote_branch可以省略
>
> 等价于`git fetch shortname remote_branch`  + `git merge FETCH_HEAD`

## 4.4 git push

> ```
> git push <shortname> [-d][-f] <local_branch>[:remote_branch]
> ```
>
> 将本地local_branch分支下的文件上传到远程仓库shortname中的remote_branch分支，并<font color="#ff0000">**合并**</font>
>
> -d：删除远程仓库shortname中的remote_branch分支
>
> -f：local_branch与remote_branch信息不一致，强行合并

# 5. 忽略.gitignore

> 忽略某些文件，使其不加入到git仓库中，如动态环境、环境、模型、数据集等。有文件结构如下：
>
> ```
> .
> ├── folder
> │   └── file1
> └── src
>     ├── folder
>     └── utils
>         └── folder
> ```

## 5.1 使用要点

> - 空行不匹配任何文件
> - 一行只表示一个模式
> - git是记录并追踪文件，而不是目录。只有目录下有文件，该目录才会被追踪。
> - 如果文件已经被追踪，.gitignore会对该文件无效。<font color="#ff0000">**故要尽早建立.gitignore**</font>
> - .gitignore也应被上传到仓库中

## 5.2 例子

> 有如下文件结构：
>
> ```
> .
> ├── folder
> │   └── file1
> └── src
>     ├── folder
>     └── utils
>         └── folder
> ```

>- 注释：#
>
>- 忽略文件与目录：
>
>  > .gitignore中的一行写入`folder`，会忽略folder目录和folder文件，会自动搜索<font color="#ff0000">**多级目录**</font>，比如`./src/utils/folder`也会被忽略。
>
>- 忽略文件：.gitignore中的写入
>
>  > ```
>  > folder
>  > !folder/
>  > ```
>  >
>  > 显示忽略所有`folder`文件和目录，再通过`!folder/`取消对`folder`目录的忽略
>
>- 忽略目录：
>
>  > .gitignore中的一行写入`folder/`，只会忽略folder目录，会自动搜索<font color="#ff0000">**多级目录**</font>
>
>- 通配符：
>
>  > - 星号* ：匹配任意多个字符，如.gitignore中一行写入`*.pyc`，则忽略所有.pcy结尾的文件
>  > - 问号?：匹配除/以外的一个字符
>  > - 双星号** :表示多级目录，如`/src/**/folder`
>  > - 叹号!：表示之前忽略的匹配模式，再次包含在跟踪内容里。如忽略文件用法
>  > - 方括号[]：匹配[]中的一个字符，如[a-z]可以匹配a-z中的一个字符

