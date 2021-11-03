# git add

不同参数情况的比较

|            | New files | Modified Files | Deleted Files | 以 . 开头的根文件                                            | 只stage当前目录？ |
| ---------- | --------- | -------------- | ------------- | ------------------------------------------------------------ | ----------------- |
| git add *  | ☑️         | ☑️              | ☑️             | ❎ <br> **.** 开头文件没被加入.ignore中<br>使用git add * 会报错<br>因此用git add .更加 | ☑️                 |
| git add -A | ☑️         | ☑️              | ☑️             | ☑️                                                            | ❎                 |
| git add .  | ☑️         | ☑️              | ☑️             | ☑️                                                            | ☑️                 |



[参考第1个answer及评论](https://stackoverflow.com/questions/26042390/git-add-asterisk-vs-git-add-period)

[参考第2个answer及评论](https://stackoverflow.com/questions/572549/difference-between-git-add-a-and-git-add)