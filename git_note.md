> Author:lgx  
> Date:2022.08.12 11:31:21  
>Email:geniuslgx@mail.ustc.edu.cn  
>说明：[可选参数]  <必要参数>  

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
>设置缓冲区大小为1GB：
>
>```
>git config --global http.postBuffer 1048576000
>```
# 2.修改与提交
>添加、删除、恢复、对比、提交
## 2.1 git add 
>```
>git add [file1/dir1] [file2/dir2] …
>```
> 添加文件或文件夹到 ==暂存区==。支持通配符，如*.png