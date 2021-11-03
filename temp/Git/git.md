# .git文件

[掘金资料](https://juejin.cn/post/6844903986839945229#heading-2)

## config

涵盖配置信息，项目配置[core]、用户配置[user]

直接修改 config 文件和使用命令行修改配置效果一样



## description

用于gitweb，让用户在web页面查看git内容



## hooks/

存放hook，hook钩子各自表示git命令前后的自定义动作



> 如何将hook行为同步给协作者以在项目中使用

借助Husky来配置hooks [实践例子](https://segmentfault.com/a/1190000022970270)





# git命令



## git status

- git status --short

https://zhuanlan.zhihu.com/p/144781678

## git diff

查看与已缓存文件的差别

- git diff

  尚未缓存文件的改动

- git diff --cached（同--staged）

  已缓存文件的改动

- git diff HEAD

  已缓存的与未缓存的所有改动

- git diff stat

  尚未缓存文件的摘要改动

