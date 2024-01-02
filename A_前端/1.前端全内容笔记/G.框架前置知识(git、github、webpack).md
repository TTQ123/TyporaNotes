**win10文件夹快速进入终端**

![uTools_1679719473463](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679719473463.png)

![uTools_1679719410190](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679719410190.png)

**快速访问github >>> fastGithub**

**点击release发布  选择对应的操作系统版本**   下载地址:[Releases · dotnetcore/FastGithub · GitHub](https://github.com/dotnetcore/FastGithub/releases)

**git的vscode插件gitlens**



# Vue 课程

## 第一部分 预备知识 —— git

### 1.命令及简介

1. ![uTools_1679716378440](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679716378440.png)

    ![uTools_1679716355280](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679716355280.png)

    **早期的版本控制工具例如svn和git最大的区别在于：svn是基于中央服务器的，而git是分布式的**

    **git国内下载路径:[CNPM Binaries Mirror (npmmirror.com)](https://registry.npmmirror.com/binary.html?path=git-for-windows/)**

    

2. 配置

    1. 配置 name 和 email

        ```bash
        git config --global user.name "xxxx"
        // confi修改配置 global全局修改
        git config --global user.email "xxx@xxx.xxx"
        ```

    

3. 使用 git：

    - 查看当前仓库的状态

        ```bash
        git status
        ```

    - 初始化仓库(学习的时候 公司的一般是直接克隆公司的仓库)

        ```bash
        git init
        ```

    - 文件状态：

        1. 未跟踪
        2. 已跟踪
        3. 暂存
        4. 未修改(本地和仓库代码一致)
        5. 已修改(本地修改，仓库未修改)
        6. ![uTools_1679721063406](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679721063406.png)

    - 未跟踪 → 暂存

        ```bash
        git add <filename> 将文件切换到暂存的状态
        git add * 将所有已修改（未跟踪）的文件暂存
        ```

    - 暂存 → 未修改

        ```bash
        git commit -m "xxxx" 将暂存的文件存储到仓库中
        //-m 后面跟的字符串相当于是提交日志的功能
        git commit -a -m "xxxx" 提交所有已修改的文件（未跟踪的文件不会提交）
        ```

    - 未修改 → 修改

        - 修改代码后，文件会变为修改状态

    

    完整操作文件的流程：

    - 1.对文件夹的文件进行修改(此时文件是已修改状态)
    - 2.执行git add *，此时是将未跟踪和上一次已修改的文件切换为暂存状态
    - 3.执行git commit -a -m "提交信息"，提交所有已修改的文件到仓库中（未跟踪的文件不会提交）
    - 4.此时一次完整的修改代码结束，文件此时是未修改状态，文件和仓库一致。
    - ![uTools_1679721520210](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679721520210.png)
    - git log 查看日志
    - ![image-20230325131922714](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230325131922714.png)

    

4. 常用的命令(使用vscode)

    1. 重置文件

    ```bash
    git restore <filename> # 恢复文件
    git restore --staged <filename> # 取消暂存状态
    ```

    2. 删除文件

    ```bash
    git rm <filename> # 删除文件 删除以后还要提交才会在仓库层面也一起删除
    git rm <filename> -f # 强制删除  文件修改后要删除需要加 -f
    ```

    3. 移动文件

    ```bash
    git mv from to # 移动文件（重命名文件)
    ```

     ![uTools_1679726651480](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679726651480.png)

      4.使用

    ```bash
    1.点击vscode的git图形化页面
    2.点击install
    ```
    
    
    
    
    
    **分支**

    git 在存储文件时，每一次代码的提交都会创建一个与之对应的节点，git 就是通过一个一个的节点来记录代码的状态的。节点会构成一个树状结构，树状结构就意味着这个树会存在分支，默认情况下仓库只有一个分支，命名为 master。在使用 git 时，可以创建多个分支，分支与分支之间相互独立，在一个分支上修改代码不会影响其他的分支。

    ```bash
    git branch # 查看当前分支
    git branch <branch name> # 创建新的分支
    git branch -d <branch name> # 删除分支
    git switch <branch name> # 切换分支
    git switch -c <branch name> # 创建并切换分支(新创建的这个分支设为默认分支)
    git merge <branch name> # 和并分支(快速合并)
    ```
    
    在开发中，都是在自己的分支上编写代码，代码编写完成后，在将自己的分支合并到主分支中。
    
    需要修改bug或者新建功能，创建自己的分支，测试完毕以后在合并到主分支上。
    
    ![uTools_1679734942724](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679734942724.png)

    **bug1是继承master的，此时bug1在master后面(一条线一起的)，此时可以快速合并**

    **合并之后，可以通过图形化界面的commit details中看到节点树**

    ![uTools_1679735036289](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679735036289.png)

    **这种情况下不能进行快速合并**

    ![uTools_1679735231132](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679735231132.png)

    **此时俩个分支修改同一个文件，无法进行快速合并，需要我们手动修改**
    
    ![uTools_1679735521503](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679735521503.png)
    
    **原始处理方法我们要打开文件自己调整(head,update那俩条线自己改)，在vscode中可以点击上面的四个选项选择合并的方式**
    
    **保留当前 | 保留后来 | 俩个都保留 | 比较变化保留**
    
    **合并以后保存提交commit，视图中节点树合并了**
    
    ![uTools_1679735850368](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679735850368.png)
    
    **合并示例(update应该指向C9，画错了)**
    
    ![uTools_1679808948224](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679808948224.png)
    
    

    

    **场景怎么模拟出来的:master先被update继承，update增加功能，master被bug1继承，bug1增加代码，master合并bug1，此时master和update不是平行线，合并会产生冲突，我们要自己调整**

    ![uTools_1679736377236](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679736377236.png)
    
    **还有一种情况是两个分支修改的是俩个不同的文件，这时候合并也不会冲突。**
    
    
    
    ### 变基（rebase）
    
    在开发中除了通过 merge 来合并分支外，还可以通过变基来完成分支的合并。
    
    我们通过 merge 合并分支时，在提交记录中会将所有的分支创建和分支合并的过程全部都显示出来，这样当项目比较复杂，开发过程比较波折时，我必须要反复的创建、合并、删除分支。这样一来将会使得我们代码的提交记录变得极为混乱。
    
    原理（变基时发生了什么）：
    
    1. 当我们发起变基时，git 会首先找到两条分支的**最近的共同祖先**
    2. ![uTools_1679809349837](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809349837.png)
    3. 对比当前分支相对于祖先的历史提交，并且将它们的不同提取出来存储到一个临时文件中
    4. 对比![uTools_1679809441117](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809441117.png)
    5. 提取![uTools_1679809564910](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809564910.png)
    6. 将当前部分指向目标的基底
    7. ![uTools_1679809617057](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809617057.png)
    8. 以当前基底开始，重新执行历史操作
    9. ![uTools_1679809635344](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809635344.png)
    10. 此时update这条分支指向C6，其实master也是了(因为合并的操作完成了)
    11. ![uTools_1679809704341](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809704341.png)
    
    
    
    ```bash
    1.在次分支上执行变基
    git rebase master(把当前分支的基变为主分支master的)
    2.切换视图
    git switch master
    3.变基以后执行合并
    git merge iss2
    ```
    
    **变基前**
    
    ![uTools_1679809910537](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809910537.png)
    
    **处理冲突**
    
    ![uTools_1679809959452](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809959452.png)
    
    **变基后**
    
    ![uTools_1679809988581](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679809988581.png)
    
    
    
    **变基和 merge 对于合并分支来说最终的结果是一样的！但是变基会使得代码的提交记录更整洁更清晰！注意！大部分情况下合并和变基是可以互换的，但是如果分支已经提交给了远程仓库，那么这时尽量不要变基。**
    
    **变基这种操作一定是在本地变完基在上传的，我们不能把服务器上运行的代码分支直接拿来变基(这会使得版本变得混乱)**
    
    
    
    
    
    ### 远程仓库（remote）
    
    目前我对于 git 所有操作都是在本地进行的。在开发中显然不能这样的，这时我们就需要一个远程的 git 仓库。远程的 git 仓库和本地的本质没有什么区别，不同点在于远程的仓库可以被多人同时访问使用，方便我们协同开发。在实际工作中，git 的服务器通常由公司搭建内部使用或是购买一些公共的私有 git 服务器。我们学习阶段，直接使用一些开放的公共 git 仓库。目前我们常用的库有两个：GitHub 和 Gitee（码云）
    
    将本地库上传 git：
    
    ```bash
    git remote add origin(远程分支的名字，默认为这个) https://github.com/lilichao/git-demo.git
    # git remote add <remote name> <url>
    
    git branch -M main(本地分支的名字)
    # 修改分支的名字的为main
    
    git push -u origin main(本地分支的名字)
    # git push 将代码上传远程库上
    # 经常出网络问题，你就多传几次
    
    #如果没改本地分支名字那默认就是git push -u origin master
    ```
    
    将本地库上传 gitee：
    
    ```bash
    git remote add gitee(远程库的名字，要和github不一样) https://gitee.com/ymhold/vue-course.git
    git push -u gitee main
    ```
    
    **本地仓库和远程仓库是相互独立的，远程仓库也有它自己的分支**
    
    
    
    ### 远程库的操作的命令
    
    ```bash
    git remote # 列出当前的关联的远程库
    
    git remote add <远程库名> <url> # 关联远程仓库
    
    git remote remove <远程库名>  # 删除远程库
    
    git push -u <远程库名> <分支名(本地分支的名字)> # 向远程库推送代码，把本地的分支推送给远程的分支
    # 这样在远程库也会创建一个一样的分支(本地分支和远程分支关联)
    
    git push -u gitee main#本地分支和远程分支同名本地代码main分支传给gitee远程库的main分支
    git push -u gitee main:hello#表示把本地的main分支和远程的hello分支关联
    
    
    git push  <远程库>  <本地分支>:<远程分支>#把本地分支推送到指定的远程分支
    
    git clone <url> # 从远程库下载代码
    git clone <url> <文件名>#本地已经有这个文件夹了 可以命名一个文件名来存放克隆的代码
    
    git push # 如果本地的版本低于远程库，push默认是推不上去
    
    git fetch # 要想推送成功，必须先确保本地库和远程库的版本一致，fetch它会从远程仓库下载所有代码，但是它不会将代码和当前分支自动合并
             # 使用fetch拉取代码后，必须要手动对代码进行合并
             
    git pull  # 从服务器上拉取代码并自动合并
    ```
    
    注意：推送代码之前，一定要先从远程库中拉取最新的代码(否则无法提交代码)g'i't
    
    **场景模拟**
    
    ```css
    1.用命令行时，我们本地有3.txt文件(刚创建的，之前只有1.2俩个文件)，远程仓库(123文件)也有3.txt文件。
    2.此时我们没法直接push提交，本地版本低于远程仓库，会报错。
    3.先fetch下载远程仓库的最新文件。
    4.此时因为俩个文件产生了冲突，我们调用merge合并本地和远程的3.txt文件，打开txt文件 手动操作合并。
    5.合并以后再次push提交。
    ```
    
    **❤❤❤用vscode就更方便，fetch以后可以直接选择合并方式 然后上传 也可以直接同步更改**
    
    
    
    **本地分支和远程分支合并的写法：远程库名/本地分支**
    
    
    
    ![uTools_1679837533317](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679837533317.png)
    
    
    
    **关联了github和gitee 向这个俩个分支分别进行提交**
    
    ![uTools_1682517765854](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1682517765854.png)
    
    
    
    ### 日志
    
    ```bash
    git log #查看日志
    q 退出页面
    ```
    
    
    
    
    
    ### tag 标签

-   当头指针没有指向某个分支的头部时，这种状态我们称为分离头指针（HEAD detached），分离头指针的状态下也可以操作操作代码，但是这些操作(代码)不会出现在任何的分支上，所以注意不要再分离头指针的状态下来操作仓库，在分支上再去操作。

-   此时操作代码，可能出现在master后也可能出现在update后，所以不要这样操作![image-20230326225614120](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230326225614120.png)

- **头指针就是我们代码当前显示的样子(所处的位置)**

- 如何切换头指针![image-20230326225850006](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230326225850006.png)

- 如果非得要回到前边的节点(C2)对代码进行操作，则可以选择创建分支后再操作

  ```bash
  git switch -c <分支名> <提交id>
  ```



- 可以为提交记录设置标签，设置标签以后，可以通过标签快速的识别出不同的开发节点(相当于时间回溯到以前去开发)：

  ```bash
  git tag #查看标签
  git tag 版本 #为当前节点贴标签
  git tag 版本 提交id #为指定id(日志中的commit)的节点贴标签
  git push 远程仓库 标签名 #提交标签
  git push 远程仓库 --tags #提交所有标签到远程
  git tag -d 标签名 # 删除标签
  git push 远程仓库 --delete 标签名 # 删除远程标签
  
  回到以前进行操作
  1.git switch v1.0.1 #切换到1.0.1版本下
  2.git switch -c update v1.0.1 #创建一个分支来改代码
  ```

  

  **补充: 文件夹命令行模式下  code .可以快速打开vscode**

  **typora `xxx` 可以变黑体**

  

  ### gitignore

- 默认情况下，git 会监视项目中所有内容，但是有些内容比如 node_modules 目录中的内容，我们不希望它被 git 所管理。我们可以在项目目录中添加一个`.gitignore`文件，来设置那些需要 git 忽略的文件。

- ![image-20230327211208839](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230327211208839.png)

### 2.github 的静态页面

- 在 github 中，可以将自己的静态页面直接部署到 github 中，它会给我们提供一个地址使得我们的页面变成一个真正的网站，可以供用户访问。

-   要求：
    - 静态页面的分支必须叫做：gh-pages
    
    - 如果希望页面可以通过 xxx.github.io 访问，则需要将库的名字配置为 xxx.github.io
    
    - 主页面必须要叫index.html
    
    - 老师说面试直接把简历写成一个页面发给面试官
    
      





### 3.docusaurus(部署静态网站)

-   facebook 推出的开源的静态的内容管理系统，通过它可以快速的部署一个静态网站

-   使用：

    -   网址：

        -   https://docusaurus.io/

    -   安装

        -   `npx create-docusaurus@latest my-website classic`

    -   启动项目

        -   `npm start`或`yarn start`

    - 构建项目

      -   `npm run build`或`yarn build`
      -   打包以后的项目在build里 这个可以用来接私活给别人改一下官网什么的
      -   注意:这种构建URL要设置对应的自己的服务器URL  要发布到github上就用github的
      -   ![image-20230327221944799](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230327221944799.png)

    -   配置项目：

        -   docusaurus.config.js 项目的配置文件

    - 添加页面：

      在 docusaurus 框架中，页面分成三种：

      -   1.创建page页面(src下的pages)   访问 **url/js文件名**
      -   创建js文件， react的写法  在layout(默认布局组件)里面直接写网页![uTools_1679927104694](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679927104694.png)
      -   创建md文件，在md文件下直接写![uTools_1679927319874](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679927319874.png)
      -   2.创建blog(blog文件夹下) 访问 直接点blog
      -   直接以md文档写法![uTools_1679927475490](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1679927475490.png)
      -   3.doc(docs文件夹) 新建文件夹 node官网就是这个布置的 访问直接点Tutorial![image-20230327223357867](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230327223357867.png)
    
    -   案例地址：
    
        -   https://github.com/lilichao/lilichao.github.io









## 第二部分 预备知识 —— 构建工具

-   当我们习惯了在 node 中编写代码的方式后，在回到前端编写 html、css、js 这些东西会感觉到各种的不便。比如：不能放心的使用模块化规范（浏览器兼容性问题）、即使可以使用模块化规范也会面临模块过多时的加载问题(js引入的模块太多了，一个模块需要发一次请求，浪费的时间太多了)。
-   我们就迫切的希望有一款工具可以对代码进行打包，将多个模块打包成一个文件。这样一来即解决了兼容性问题，又解决了模块过多的问题(打包以后发送的请求次数就减少了很多，加载速度就快了)。
-   构建工具(相当于进行了编译)就起到这样一个作用，通过构建工具可以将使用 ESM 规范编写的代码转换为旧的 JS 语法，这样可以使得所有的浏览器都可以支持代码。
-   ![uTools_1680095904382](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680095904382.png)



### 1.Webpack(旧)

**webpack是用node写的，只能打包node的项目**

**webpack打包的时候会智能的识别哪些代码会执行哪些不会执行，没用到的不会打包进项目**

**问题 : m1.js中引入了jQuery，但是没有使用jQuery的功能，此时主文件调用m1，jQuery也会被打包进去，这是因为jQuery中有自己必须要执行的函数(jQuery的内部调用)，所以weboack要把jQuery一起打包进项目，因为在webpack看来jQuery在项目中是有执行的，所以要打包**

#### 1.使用步骤：

1. 初始化项目`yarn init -y`
2. 安装依赖`webpack`(核心代码模块)、`webpack-cli`(cli表示能在命令行下使用webpack)
3. yarn add -D webpack webpack-cli  **-D表示的是开发依赖 不是项目必须的依赖 主要是方便我们开发人员进行区分**
4. 在项目中创建`src`目录，然后编写代码（index.js是主文件默认，可以创建其它文件）
5. 执行`yarn webpack`来对代码进行打包（打包后观察 dist 目录  默认所有文件会打包成main.js文件）

- 问题：src和src文件夹以外使用的规范是不一样的，src要使用前端规范，src以外的是给node识别的，要使用node的规范

- src下![uTools_1680101200033](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680101200033.png)

- src外![uTools_1680101172461](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680101172461.png)



#### 2.配置文件（webpack.config.js）

```javascript
const path = require("path")
module.exports = {
    mode: "production",//生产模式   "development" //开发模式
    entry: "./src/index.js",
    output: {},
    module: {
        rules: [
            {
                test: /\.css$/i,
                use: ["style-loader", "css-loader"]
            }
        ]
    }
}
```

- entry入口![image-20230401115630709](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230401115630709.png)
- output![uTools_1680323335370](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680323335370.png)
- **Loader加载器(webpack默认只能打包js文件)**  想要处理什么就安装什么loader就好了
- ![uTools_1680326174600](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680326174600.png)
- ![image-20230401131723263](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230401131723263.png)





- 在编写 js 代码时，经常需要使用一些 js 中的新特性，而新特性在旧的浏览器中兼容性并不好。此时就导致我们无法使用一些新的特性。

- 但是我们现在希望能够使用新的特性，我们可以采用折中的方案。依然使用新特性编写代码，但是代码编写完成时我们可以通过一些工具将新代码转换为旧代码。

- babel 就是这样一个工具，可以将新的 js 语法转换为旧的 js，以提高代码的兼容性。(在一些情况下，有些代码无法直接转化，babel会自己添加一个js脚本进浏览器，以使得我们代码可以运行)

- 我们如果希望在 webpack 支持 babel，则需要向 webpack 中引入 babel 的 loader

- 使用步骤

  1. 安装 `npm install -D babel-loader @babel/core @babel/preset-env`

  2. 配置：

      ```javascript
      module: {
          rules: [
              {
                  test: /\.m?js$/,
                  //exclude 不处理的文件
                  exclude: /(node_modules|bower_components)/,
                  use: {
                      loader: "babel-loader",
                      options: {
                          //预设环境 提前帮我们安装一些插件(一种转换就是一种插件)
                          presets: ["@babel/preset-env"]
                      }
                  }
              }
          ]
      }
      ```

  3. 在 package.json 中设置兼容列表

      ```json
      "browserslist": [
          	//设置兼容的浏览器
              "defaults"//defaults默认
       ]
      ```
      
      https://github.com/browserslist/browserslist   **配置的参考**
      
      

**loader会编译代码，插件只是一些辅助的功能**

**code安装格式化插件后 全选 ctrl+s可以直接格式化**



- 插件（plugin）

  -   插件用来为 webpack 来扩展功能

  -   html-webpack-plugin

      -   这个插件可以在打包代码后，自动在打包目录生成 html 页面

      -   使用步骤：

          1. 安装依赖![uTools_1680342073670](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680342073670.png)
          2. 引入![uTools_1680341731498](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680341731498.png)
          3. 配置插件
          
          ```javascript
          plugins: [
              //调用构造函数创建一个对象
              new HTMLPlugin({
                  // title: "Hello Webpack", 网页标题
                  //模板 以该网页为模块创建页面，但是会自己引入脚本等文件
                  template: "./src/index.html"
              })
          ]
          ```



自动进行打包(实时刷新)

1.传统方法![uTools_1680344063966](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680344063966.png)

2.开发服务器（webpack-dev-server）

-   安装：
    -   `yarn add  -D webpack-dev-server`
    -   启动：`yarn webpack server --open`
    -   ![uTools_1680344635425](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680344635425.png)
    -   用服务器模式开发完以后要自己手动yarn webpack一下，保证代码是最新的

- `devtool:"inline-source-map"`配置源码的映射(devtool表示开发工具)
- 运行是打包后的代码，但是会产生一个文件夹让我们进行调试
- ![uTools_1680347282110](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680347282110.png)
- 配置以后打开开发者工具  可以看见产生了一个新的demo_01文件夹 在里面可以调试![uTools_1680347331438](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680347331438.png)



### 3.webpack工作原理

![image-20231229172242433](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231229172242433.png)





### 2.Vite（新）

-   Vite 也是前端的构建工具

-   相较于 webpack，vite 采用了不同的运行方式：

    -   开发时，并不对代码打包，而是直接采用 ESM(ES模块化) 的方式来运行项目
    -   在项目部署时，在对项目进行打包

-   除了打包速度外，vite 使用起来也更加方便

-   ![uTools_1680351755028](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680351755028.png)

-   一定要打包，因为多个js脚本要发送多次请求，浏览器加载速度就很慢

- 基本使用：

  1. 安装开发依赖 vite

  2. vite 的源码目录就是项目根目录(他会自动找到index.html 下引用的js文件)

  3. 开发命令：

      vite 启动开发服务器

      vite build 打包代码

      vite preview 预览打包后代码
      
      ```bash
      1.安装
      yarn add -D vite
      2.开发模式下运行(启动了一个内置服务器，代码随着修改而更新)，会给我们一个http://localhost:5174/)
      yarn vite
      3.打包(开发模式是以esm来打包的，不能直接运行)
      [ESM必须通过url的形式来加载，此时我们通过静态页面访问(alt+b和live serve)是不行的，只能放在服务器运行或者yarn vite preview来预览]
      yarn vite build
      4.预览打包后代码(执行的是打包后的代码)
      yarn vite preview 
      
      vite和vite preview的区别
      1.vite是直接执行的，没有对代码进行打包
      2.vite preview是预览打包后的代码
      3.都是不能直接以静态页面运行的，要用它的服务器来查看，或者把打包后的代码放到我们的服务器上运行。
      ```
      
      ![uTools_1680355003565](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680355003565.png)
      
      **vite --open**也可以启动

  

  

- 使用命令构建

  ```bash
  会自动给我们构建一个vite项目
  npm create vite@latest
  yarn create vite
  pnpm create vite
  ```

  

  

-   配置文件：`vite.config.js`

-   格式：

    ```javascript
    //要使用ESM  webpack用的是node默认的commonjs
    import { defineConfig } from "vite"
    //安装yarn add @vitejs/plugin-legacy
    import legacy from "@vitejs/plugin-legacy"//兼容性插件，相当于webpack的babel(解决兼容性)
    
    //使用legacy要装一个terser(压缩代码的插件)
    //yarn add -D terser
    export default defineConfig({  //defineConfig加上有提示
        plugins: [
            legacy({
                targets: ["defaults","ie 11"]//配置支持的浏览器
            })
        ]
    })
    
    //打包以后会出现俩个js 带legac的js文件就是兼容性的文件,还有一个正常的js
    //webpack是打包成一个文件，vite打包成俩个  在index.html中会引入支持moudle和不支持moudle的代码
    ```

![uTools_1680357911146](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1680357911146.png)

![image-20230401220532344](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20230401220532344.png)





## 第三部分 Vue

### 1.vue

-   vue 是一个前端的框架，主要负责帮助我们构建用户的界面
-   MVVM：Model - View - View Model
-   vue 负责 vm 的工作（视图模型），通过 vue 可以将视图和模型相关联。
    -   当模型发生变化时，视图会自动更新
    -   也可以通过视图去操作模型
-   vue 思想：
    -   组件化开发
    -   声明式的编程

### 2.HelloWorld

1. 直接在网页中使用（像 jQuery 一样）

    - `        <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>`

2. 使用 vite

    - `yarn add vite -D`

3. 代码：

    ```javascript
    // 组件，就是一个普通js对象
    const App = {}

    // 创建应用
    const app = createApp(App)

    // 挂载到页面
    app.mount("#root")
    ```

4. 自动创建项目
    - `npm init vue@latest`
    - `yarn create vue`



## 网页的渲染

-   浏览器在渲染页面时，做了那些事：

    1. 加载页面的 html 和 css（源码）
    2. html 转换为 DOM，css 转换为 CSSOM
    3. 将 DOM 和 CSSOM 构建成一课渲染树
    4. 对渲染树进行 reflow（回流、重排）（计算元素的位置）
    5. 对网页进行绘制 repaint（重绘）

-   渲染树（Render Tree）

    -   从根元素开始检查那些元素可见，以及他们的样式
    -   忽略那些不可见的元素（display:none）

-   重排、回流

    -   计算渲染树中元素的大小和位置
    -   当页面中的元素的大小或位置发生变化时，便会触发页面的重排（回流）
    -   width、height、margin、font-size ......
    -   注意：每次修改这类样式都会触发一次重排！所以如果分词修改多个样式会触发重排多次，而重排是非常耗费系统资源的操作（昂贵），重排次数过多后，会导致网页的显示性能变差，在开发时我们应该尽量的减少重排的次数
    -   在现代的前端框架中，这些东西都已经被框架优化过了！所以使用 vue、react 这些框架这些框架开发时，几乎不需要考虑这些问题，唯独需要注意的时，尽量减少在框架中直接操作 DOM

-   重绘

    -   绘制页面
    -   当页面发生变化时，浏览器就会对页面进行重新的绘制

-   例子：

    ```html
    <!DOCTYPE html>
    <html lang="zh">
        <head>
            <meta charset="UTF-8" />
            <meta http-equiv="X-UA-Compatible" content="IE=edge" />
            <meta
                name="viewport"
                content="width=device-width, initial-scale=1.0"
            />
            <title>Document</title>
            <style>
                .box1 {
                    width: 200px;
                    height: 200px;
                    background-color: orange;
                }
    
                .box2 {
                    background-color: tomato;
                }
    
                .box3 {
                    width: 300px;
                    height: 400px;
                    font-size: 20px;
                }
            </style>
        </head>
        <body>
            <button id="btn">点我一下</button>
            <hr />
            <div id="box1" class="box1"></div>
            <script>
                btn.onclick = () => {
                    // box1.classList.add("box2")
                    // 可以通过修改class来间接的影响样式，来减少重排的次数
                    // box1.style.width = "300px"
                    // box1.style.height = "400px"
                    // box1.style.fontSize = "20px"
                    // box1.classList.add("box3")
                    // box1.style.display = "none"
                    // box1.style.width = "300px"
                    // box1.style.height = "400px"
                    // box1.style.fontSize = "20px"
                    // div.style.display = "block"
                }
            </script>
        </body>
    </html>
    ```