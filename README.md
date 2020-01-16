# 一、 客户端尽量安装Anaconda，如果内存不够可以安装miniconda
### 基本用法[Anaconda用法](https://www.jianshu.com/p/742dc4d8f4c5)

### 一、客户端用法
1. conda创建虚拟环境并安装python3
    + 创建虚拟环境

    ```
    conda create -n 环境名称
    ```

    + 查看本机虚拟环境

    ```
    > conda env list
    ```

    + 使用/切换环境

    ```
    > activate 环境名称
    ```

    + 退出环境

    ```
    > deactivate
    ```

    + -- linux和mac --用户的命令不一样
    
    ```
    source source activate 环境名
    source deactivate 环境名
    ```

2. 导入包目录【`适用于服务器`】：相当node中的npm i | yarn
    ```
    > activate 环境名称
    > conda install -n 环境名称 python
    > pip install -r package.txt
    ```

3. 启动服务
    ```
    > cd djangoproject/
    > python manage.py runserver
    ```
# 二、如何导出包目录、安装包
1. 导出包目录：相当node中的package.json
    ```
    > pip freeze > package.txt
    ```
2. 安装Django：`conda install -n 环境名称 包名` 
 + ##### `这样安装的包下可以在本环境下，否则将安装在全局，导出包将会超出使用到的包`
 + 安装
    ```
    > conda install -n 环境名称 django
    ```
 + 安装的是哪个版本
    ```
    > python -m django --version 
    ```
 + 创建测试项目
    ```
    > django-admin startproject 项目名
    ```

```CREATE database testdb DEFAULT CHARACTER SET utf8mb4 COLLATE utf8_general_ci```
+ makemigrations会在当前目录下生成一个migrations文件夹，该文件夹的内容就是数据库要执行的内容
    ```
    > python manage.py makemigrations
    ```
+ migrate就是执行之前生成的migrations文件，这一步才是操作数据库的一步
    ```
    > python manage.py migrate
    ```

# 二、 服务器python安装过程
参考:
> https://www.jianshu.com/p/c38e3121a201
> https://blog.csdn.net/liu246437/article/details/87723435
1. 安装miniconda
    [miniconda官网](https://docs.conda.io/en/latest/miniconda.html)
    + 下载
        ```
        wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
        ```
    + 安装
        ```
        sh Miniconda3-latest-Linux-x86_64.sh
        ```
    + 测试 `conda --version`
    + 如果不能调用conda， 需要激活 `source .bashrc`
    + 安装完成，网上的一些配置貌似没用到，默认输入`python`就是python3.7.5， `pip/yum` 也没有问题，所以没有进行其他操作
2. 服务进程后台化

   需要nohup命令，所以安装coreutils,参考 https://www.cnblogs.com/jinxiao-pu/p/9131057.html

   + `yum install coreutils`
   + `nohup python manage.py runserver > ../nohup.out 2>&1 &`
   + 该作业的所有输出被重定向到../nohup.out的文件中
   + `ps -aux|grep manage.py | grep -v grep` 查看进程 https://www.cnblogs.com/baby123/p/6477429.html
   + kill 或 kill -9 终止进程；一般情况下，-9可以马上杀死进程，没有任何阻塞

# 三、 接口返回格式