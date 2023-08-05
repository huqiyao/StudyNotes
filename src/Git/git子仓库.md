# git子仓库

[参考资料](https://juejin.im/post/5e09b706e51d45580359b367)

## 意义

将一个git仓库作为另一个git仓库的子目录，使得重复代码能够复用，而且两者保持独立提交



## 使用

### 两个仓库都刚开始写，新建的情况

- 创建两个独立的仓库(假设main、sub)

- 连接两个仓库，即，将子仓库引入主仓库中

  ```shell
  cd main
  git submodule add 子仓库地址 目标目录
  # 如果不写目标地址，则放在与子仓库同名的目录中
  ```

  此时，子仓库下创建了```.gitmodules``` 文件，保存子仓库在主仓库目录下的映射关系

  ```shell
  # 如：
  [submodule "src/.zj"]
  	path = src/.zj
  	url = http://xxx/jianguan/web-template.git
  	branch = master
  ```

- 相当于项目中新增了代码，所以```git add .``` ```git commit```  ```git push```



### clone一个包含了子仓库的主仓库的情况

