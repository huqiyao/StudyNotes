# git flow

[参考资料](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

<div align='center'><img src='../图片资料/gitflow.png'/></div>

## 创建develop分支

```shell
git flow init
// ⬇
git branch develop
git push -u origin develop
```



## 从develop切出feature分支

```shell
git flow feature start feature_branch
// ⬇
git checkout develop
git checkout -b feature_branch
```



## 结束feature，合并进develop分支

```shell
git flow feature finish feature_branch
// ⬇
git checkout develop
git merge feature_branch
```



## 切出release分支

```shell
git flow release start x.x.x
// ⬇
git checkout develop
git checkout -b 'release/x.x.x'
```



## 结束release分支，合并进develop、master分支

```shell
git flow release finish 'x.x.x'
// ⬇
git checkout master
git merge release/x.x.x
```



## 切出hotfix分支

```shell
git flow hotfix start
// ⬇
git checkout master
git checkout -b hotfix_branch
```



## 结束hotfix分支，合并进develop、master分支

```shell
git flow finish hotfix_branch
// ⬇
git checkout master
git merge hotfix_branch
git checkout develop
git merge hotfix_branch
git branch -D hotfix_branch
```



# 关于删除分支

## ``` -D```

## ```-d```