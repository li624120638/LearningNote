# 1.nvidia-docker安装

> windows暂不支持nvidia-docker，以下为linux下的安装方式
>
> - [安装教程](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
>
> - step1 Setting up Docker
>
>   ``` bash
>   curl https://get.docker.com | sh \
>     && sudo systemctl --now enable docker
>   ```
>
> - step2 Setting up NVIDIA Container Toolkit
>
>   ``` bash
>   distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
>         && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
>         && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
>               sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
>               sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
>
> - step3 Install
>
>   ``` bash
>   sudo apt-get update
>   sudo apt-get install -y nvidia-docker2
>   sudo systemctl restart docker
>   ```

# 2. 镜像

## 2.1 docker commit

> ```
> docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
> ```
>
> 使用现有容器制作镜像
>
> OPTIONS:
>
> - **-a :**提交的镜像作者；
>
>   
>
> - **-c :**使用Dockerfile指令来创建镜像；
>
>   
>
> - **-m :**提交时的说明文字；
>
>   
>
> - **-p :**在commit时，将容器暂停。
>
> CONTAINER：可以是容器名，可以是容器ID

## 2.2 docker save

> ```bash
> docker save [OPTIONS] IMAGE
> ```
>
> 将镜像保存为文件(压缩)
>
> OPTIONS ：
>
> - **-o :**输出到的文件。

## 2.1 docker load

> ```bash
> docker load [OPTIONS]
> ```
>
> OPTIONS：
>
> - **-i :**  指定导入的文件，代替 STDIN。
>
>   
>
> - **-q :** 精简输出信息。

## 2.3 Dockerfile

TODO:

# 3. 容器

>```bash
>ctname='lgx_tensorrt'
>imagename='lgx_tersorrt:trt8016'
>mountpath='/home/imagexx/lgx'
>docker run -itd -u $(id -u):$(id -g) --gpus all --mount type=bind,source=$mountpath,target=$mountpath --name $ctname --net=host $imagename bash
>docker start $ctname
>docker exec -it -u root $ctname bash
>...
>exit
>docker stop $ctname
>docker container rm $ctname
>```
>
>- docker run
>  - -itd：交互式，伪终端，后台运行
>  - -u：使用什么身份创建终端（不再是root）
>  - --gpus all：使用所有显卡
>  - --mount：挂在
>  - --name $ctname：所创建的容器名
>  - --net：使用什么网络
>  - $imagename：指定镜像名
>  - bash：进入容器后使用的命令
>- docker exec
>  - -it：同上
>  - -u：在容器中的身份
>  - $ctname：执行的容器名
>  - bash：进入容器后的第一条命令