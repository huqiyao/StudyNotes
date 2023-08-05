## 查看仓库中某个软件/包的信息

```shell
aptitude show xxx
```



## 解压```tar.gz```文件

```shell
sudo tar -zxvf node-v12.14.1-linux-x64.tar.xz -C /usr/lib
```



## 解压```tar.xz```文件

```shell
sudo tar -xvJf node-v12.14.1-linux-x64.tar.xz -C /usr/lib
```





## 安装与配置环境变量

[参考资料](http://www.luyixian.cn/news_show_191345.aspx)

### 查看自带的jdk、jre

```shell
dpkg -l | grep openjdk
```

<div align="center"><img src='图片资料/查看已安装包信息.png'></div>


### 下载jdk安装包，解压到相应目录

```shell
sudo tar -zxvf jdk-8u231-linux-x64.tar.gz -C /usr/lib
```

<div align="center"><img src='图片资料/解压jdk安装包.png'></div>
-  -C 选项的作用是：指定需要解压到的目录

### ①配置环境变量

```shell
sudo vim /etc/profile
```

<div align="center"><img src='图片资料/配置java环境变量.png'></div>
<div align="center"><img src='图片资料/vim光标跳转.png'></div>
- 小写o：在这行下面插入一行
- gg：跳到第一行
- G：跳到最后一行



### ②创建链接

node安装可①可②

```shell
sudo ln -s /usr/lib/node-xxx/node /usr/local/bin/node
sudo ln -s /usr/lib/node-xxx/npm /usr/local/bin/npm
```



### 使配置文件生效

```shell
source /etc/profile
```

但遇到问题，切换回普通bash

<div align="center"><img src='图片资料/切换为普通bash.png'></div>
但只在当前终端生效

所以直接注销再打开就可以了





# 安装homebrew步骤

- 安装homebrew、homebrew-cask

  [csdn参考资料](https://blog.csdn.net/weixin_40879140/article/details/89963244)

  ```shell
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
  ```

  ```shell
  brew tap phinze/homebrew-cask
  brew install brew-cask
  ```



- 配置homebrew、homebrew-cask、homebrew-bottles、homebrew-core镜像

  [中科大镜像源配置](http://mirrors.ustc.edu.cn/help/homebrew-cask.git.html)

  ```shell
  cd "$(brew --repo)"
  git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
  ```

  ```shell
  cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
  git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
  ```

  ```shell
  echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
  source ~/.bash_profile
  ```

  ```shell
  cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
  git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
  ```

  

