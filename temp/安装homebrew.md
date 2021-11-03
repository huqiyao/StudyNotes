# 步骤

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

  

