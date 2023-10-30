❤从master上拉取一个develop分支，在从develop分支拉取feature分支

1.从master拉取develop分支

```bash
1.在本地master分支上执行   git checkout -b develop
2.将develop推送到远程 git push origin develop(也可以合并后在更新)
3.在develop分支上创建feature git checkout -b feature
4.开发新功能并提交  git add . && git commit -m "Add new feature"
5.将feature分支提交到远程 git push origin feature
6.切换到develop分支合并feature  git checkout develop && git merge feature
7.切换到master分支合并develop git checkout master && git merge develop
8.更新master git push origin master(没打版本号)

9.更新的事项 
如果有冲突需要手动解决并提交，打上版本号提交到远程仓库
git tag -a v1.0.1 -m "Release version 1.0.1"
git push origin v1.0.1
git push –-tags(将本地的所有标签推送到远程仓库的命令)
```

切换到哪个分支，新建的分支就是基于该分支创建的。例如，如果你从master分支切换到develop分支，然后新建一个feature分支，这个feature分支就是基于develop分支创建的。同理，如果切换回master分支或其它任意分支，新建的分支仍然会基于相应的分支创建。



**常用的git命令**

![image-20231025142551568](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231025142551568.png)

![image-20231025142428994](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231025142428994.png)



**stackoverflow上关于如何在master上创建一个分支**

https://stackoverflow.com/questions/39478482/how-to-create-development-branch-from-master-on-github

https://www.coder.work/article/187885

 

**gitflow基本概念**

https://blog.csdn.net/lt6210925/article/details/131263986

```bash
1. master是线上运行的版本 最稳定的版本 每次更新需要打上tag，只接受其它分支合入，同时必须是hotfix或者release分支的代码
2. develop是主开发分支，这个分支可以合并一些feature，当要release的时候，就从这个分支上进行创建release分支。
3. feature 分支又叫功能分支，一般命名方法feature/xxx，用来开发版本或者未来要发布新的功能或者探索新功能。要基于develop拉取
4. release这个分支又叫预发布分支，一般命名为 release/1.1.x 这个分支转为发布做准备。允许小量级的bug修复。release分支只能从develop分支拉过来，用来修复一些bug。（不做feature相关的开发）
5. hotfix 叫热修复分支，一般命名为hotfix/4.1.3 为固定某个版本进行修复，当master上遇到严重问题需要修复的时候，就要从master上指定tag拉取。这样做就是为了隔离feature开发和bug修复。hotfix只能从master上拉去，测试通过之后合并会master和develop
```

 ![image-20231025144426424](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231025144426424.png)





**gitflow完整步骤**

```bash
1. 创建仓库

2. 创建develop分支 git checkout –b develop（-b表示创建分支）

3. 切换到develop分支 git checkout develop

4. 如果是别人更新了develop分支 可以拉取一下最新的 git pull origin develop

5. 创建feature/x分支 git checkout -b feature/x  origin/develop(切换到develop就是基于develop分支)

6. 完成feature/x分支开发 将其合并到develop分支 git merge feature/x

7. 如有冲突请收到解决并提交更改(git add . 和git commit –m ‘xxxx’)

8. 上传到远程develop分支  git push origin develop

9. 将develop分支合并到master分支中
git checkout master
git merge develop 

10. 如果有冲突手动解决并提交，打上版本号提交到远程仓库
git tag -a v1.0.1 -m "Release version 1.0.1"
git push origin v1.0.1
git push –-tags(将本地的所有标签推送到远程仓库的命令)
```





 

解决git冲突

https://blog.csdn.net/weixin_45597885/article/details/129464448

 

不建议这样拉取分支

![img](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/wps1.jpg) 



5.和耶哥合作的项目

```bash
1.建仓库

2.从master分支建立develop分支develop分支

3.在develop分支develop分支开发

4. 将develop分支合并到master分支中
git checkout master
git merge develop 

5. 如果有冲突手动解决并提交，打上版本号提交到远程仓库
git tag -a v1.0.1 -m "Release version 1.0.1"
git push origin v1.0.1
git push –-tags(将本地的所有标签推送到远程仓库的命令)
```

