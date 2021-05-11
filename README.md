#### git设置

```
git config --global 
git config --system
git config --local

git config --local user.name 'RookieQi'
git config --local user.email '1119377355@qq.com'
```





#### 查看状态

```
git status

```





比较工作区中index.html和版本库中最新的index.html的差异





//将main.js从暂存区移出

git rm --cached main.js



//将所有文件从暂存区移出

git rm --cached .





 工作目录下的每一个文件都不外乎这两种状态：**已跟踪** 或 **未跟踪**。 已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后， 它们的状态可能是未修改，已修改或已放入暂存区 



 工作目录中除已跟踪文件外的其它所有文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有被放入暂存区。 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态，因为 Git 刚刚检出了它们， 而你尚未编辑过它们 



 编辑过某些文件之后，由于自上次提交后你对它们做了修改，Git 将它们标记为已修改文件。 在工作时，你可以选择性地将这些修改过的文件放入暂存区，然后提交所有已暂存的修改，如此反复 



  未跟踪的文件意味着 Git 在之前的快照（提交）中没有这些文件 



使用命令 `git add` 开始跟踪一个文件。 所以，要跟踪 `README` 文件，运行：

```console
$ git add README
```



此时再运行 `git status` 命令，会看到 `README` 文件已被跟踪，并处于暂存状态：

```console
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)

    new file:   README
```

只要在 `Changes to be committed` 这行下面的，就说明是已暂存状态。 如果此时提交，那么该文件在你运行 `git add` 时的版本将被留存在后续的历史记录中



 `git add` 命令。 这是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，  还能用于合并时把有冲突的文件标记为已解决状态等 ， 这个命令可以理解为“精确地将内容添加到下一次提交中 





 ![Git 下文件生命周期图。](https://git-scm.com/book/en/v2/images/lifecycle.png) 



#### git log 

 显示所有提交过的版本信息 

![image-20210426112013397](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426112013397.png)



查看最近n次提交

```
git log n
```





#### git reflog

 可以查看所有分支的所有操作记录 

![image-20210509234759809](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210509234759809.png)



git checkout b1dc588 -- index.js

用b1dc588 版本的index.js覆盖本地工作区的index.js





git reset --hard HEAD^

移动HEAD指针到上一个快照，工作区同步回退



git reset --hard HEAD^^

移动HEAD指针到上上个快照，工作区同步回退



git reset --hard b1dc588版本

![image-20210509234636785](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210509234636785.png)







#### 显示目前所处分支

```shell
git branch
```

![image-20210510001900681](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210510001900681.png)



```
git branch -av
* master 				59389f5
  remotes/origin/master 59389f5 third..
```





#### 创建分支

```shell
git branch dev
```



#### 切换分支

```shell
git checkout dev
```



创建并切换分支

```
git checkout -b dev
```



删除分支

```
git branch -d dev
```



#### 合并分支

```shell
//当前处于master分支，要合并bug分支
git merge bug
```



假如Master分支分出dev分支，刚开始就是一个新的dev指针与master指向同一个快照版本，随着在dev分支上的开发，dev分支会不断产生新的快照版本，也就是说dev指针是一直在向前移动的，指向的快照版本一定比master指针指向的快照版本新



不管是dev分支合并master分支还是master分支合并dev分支，都是快照版本低的指针重新指向快照版本新的指针



#### 查看差异

良好习惯：在commit前比较暂存区和最新提交的差异



比较暂存区与当前分支最新提交的差异

git diff --cached



比较工作区和暂存区的差异

git diff



比较工作区和暂存区中readme.md文件的差异

git diff -- readme.md





使工作区内容和暂存区一致（撤销工作区修改）

- 先讲a.txt加入暂存区

```
git add a.txt
```

- 编辑工作区a.txt，加入一些代码

```
echo "hello" >> a.txt
```

- 现在后悔了添加了代码，想撤销添加的代码

```
git checkout a.txt
```











#### 使暂存区和HEAD所指提交一致（撤销暂存区修改）

- git reset HEAD



- git reset -- files 使用当前分支上的修改覆盖暂存区，用来撤销最后一次 git add files



使工作区和暂存区一致（撤销工作区修改）

git checkout -- index.html





#### 三区一致(慎用)

git reset --hard 555777

将head指针指向555777，并使工作区和暂存区的所有内容都与555777一致



#### 比较分支

比较master和dev分支的差异（默认比较的是各自的最新提交）

diff master dev



比较master和dev分支的index.html文件的差异

diff master dev -- index.html



#### 删除暂存区文件

git rm readme.md

之后的commit就不包括readme.md





#### 储藏

在一个分支上操作之后，如果还没有将修改提交到分支上，此时进行切换分支，那么另一个分支上也能看到新的修改。这是因为所有分支都共用一个工作区的缘故。

可以使用 git stash 将当前分支的修改储藏起来，此时当前工作区的所有修改都会被存到栈中，也就是说当前工作区是干净的，没有任何未提交的修改。此时就可以安全的切换到其它分支上了。



```
保存当前工作区状态到栈中
git stash 

git stash list
stash@{0}: WIP on dev: c22dc01 dev2

弹出栈顶 的工作区状态并恢复工作区
git stash pop

git stash list
//无现场

git stash apply 获得栈顶的工作区状态并恢复工作区

//指定获得名为stash@{0}的现场
git stash apply stash@{0}


```







git stash drop stash@{0} 删除0号栈帧



##### fastfoward

![image-20210510081835283](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210510081835283.png)	



#### 版本穿梭

![image-20210510094252614](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210510094252614.png)





#### 分支冲突



 当两个分支都对同一个文件的同一行进行了修改，在分支合并时就会产生冲突 



#### 差异化比较

- 工作区和暂存区比较

```
git diff
```

- 工作区和版本库比较

```
git diff 23DF24
git diff HEAD
```

- 暂存区和版本库比较

```
git diff --cached 23DF24
git diff --cached HEAD
```





#### 推送代码

- 给远程仓库取别名

```
git remote add origin https://github.com/...git
```

- 第一次push

```
//推送本地master到远程仓库
git push -u origin master
```

- 后续push

```
git push
```





```shell
git pull origin 分支名
```



#### 拉取代码

```shell
git pull origin dev	//将远程仓库上dev分支的代码拉取到本地工作区

git pull origin dev可拆分成两条命令：

git fetch origin dev	将远程仓库上dev分支的代码拉取到本地commit区
git merge origin/dev	将commit区的代码merge到工作区

```



#### 添加版本标签



```shell
git tag - a v1 -m "第一版"

//查看标签
git tag

//删除标签
git tag -d '标签名'

git tag -l "v*"
```

为本地项目当前版本打上一个标签，标签名v1，标签描述为"第一版"



#### 同步标签到远程仓库

```shell
git push origin --tags
```











#### bug修复方案

![image-20210426120132177](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426120132177.png)





![image-20210426221838534](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426221838534.png)







#### 团队协同开发

- Leader(RookieQi)要招揽团队开发项目，项目名为Research
- 1.创建组织，Mysterious-Research, 将成员RookieQitwo邀请进组织
- 创建Research项目，进入项目的设置，将成员RookieQitwo邀请进项目，并赋予对项目的Write权限



进入Research项目的Setting页



![image-20210426230713427](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426230713427.png)



邀请RookieQitwo加入项目，赋予写权限

![image-20210426230643549](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426230643549.png)



RookieQitwo开始参与项目开发，假设RookieQitwo接收到了开发订单(Order)模块的任务，则开发步骤如下

- 将项目clone到本地
- 切换到项目的dev分支，并创建order分支
- 进入order分支，在此分支下编写订单模块代码
- 本地开发完订单模块后，push到远程仓库的order分支
- 接下来发送pull request请求将order分支merge到dev分支

![image-20210426234301719](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426234301719.png)



![image-20210426234455930](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426234455930.png)



- leader接受到pull request，开始code review，如果没有问题，则可以将order分支merge到dev分支

![image-20210426233521774](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426233521774.png)



![image-20210426234830825](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426234830825.png)



![image-20210426235044667](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426235044667.png)



可以看到，员工RookieQitwo编写的order模块代码成功加入到了dev分支



![image-20210426235111646](C:\Users\11193\AppData\Roaming\Typora\typora-user-images\image-20210426235111646.png)



#### 增加RELEASE

在本地和远程仓库都添加RELEASE分支