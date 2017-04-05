
## 探究git的基础工作原理
[简书地址](http://www.jianshu.com/p/9524e1aebc23)

git基本命令还可以参考Pro Git;
以下是mac系统终端操作，常用命令可以参考http://www.jianshu.com/p/3291de46f3ff


** 附上方便操作的终端快捷键**
> Command + K 清屏
Command + T 新建标签
Command +W  关闭当前标签页
Command + S  保存终端输出
Command + D  垂直分隔当前标签页
Command + Shift + D 水平分隔当前标签页
Command + shift +  {或}向左/向右切换标签

## git基本操作流程
1. 创建测试文件夹，名字我命名为JHGit;
```
mkdir JHGit
```

![目录下的文件](http://upload-images.jianshu.io/upload_images/2310905-e095c1f9e86bf2de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.切换到JHGit文件夹下
```
cd JHGit
```
3.初始化git
```
git init
```

![初始化后的文件夹目录](http://upload-images.jianshu.io/upload_images/2310905-6718bd704f46561d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.先查看下.git文件内容
```
vi .git   //或者  
cd .git
```

![vim编辑器下的内容](http://upload-images.jianshu.io/upload_images/2310905-ee7298fa651bdf27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**也可以使用tree命令!
温馨提示：mac下默认是没有 tree命令！！！**下面几个方法可以试试
> 1.可以使用find命令模拟出tree命令的效果
```
find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'
```
2.手动alias一下，在你的.bash_profile或者.zshrc中添加:(前提你已经安装了oh-my-zash)
```
alias tree="find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'"
```
3.可以使用 homebrew 安装 tree 命令行：
```
brew install tree
```

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2310905-2c82be011e5cce15.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.HEAD

![当前所在分支](http://upload-images.jianshu.io/upload_images/2310905-d1d40069251cc0fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6.查看下config里面的东西：设置了一些默认的参数之类的
```
cat .git/config
```
![config](http://upload-images.jianshu.io/upload_images/2310905-5d0b12ad1a8e76cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7.description是描述文件

![对当前库的描述](http://upload-images.jianshu.io/upload_images/2310905-4e6d6cf6fc7cca61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


8.根据HEAD打印的路径提示找到refs/heads/下

![HEAD路径](http://upload-images.jianshu.io/upload_images/2310905-21754eee17dcc2fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

9.hooks(脚本文件夹)，具体了解可以参考[GIt Hooks](http://www.jianshu.com/p/79c05c103bdd)

![Paste_Image.png](http://upload-images.jianshu.io/upload_images/2310905-9aba70c7151abc44.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10.info里面的exclude   objects里面的info和pack目前都是空文件

11.和远程仓库建议联系
```
git remote add origin https://github.com/Shenjinghao/JHGit
```

** 注意：连接简历后，可以正常git pull代码，但是如果不做修改，是无法git push提交代码，原因是此时的master的分支不指向任何commit。**

其实这里也可以通过git clone命令跳过和远程仓库连接这一步！

```
git clone https://github.com/Shenjinghao/JHGit.git
```
连接后config内容变为下图
![连接后的config内容](http://upload-images.jianshu.io/upload_images/2310905-a468aada7cd7ca26.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


12.使用touch命令创建个test1文件，工作区会提示，通过命令
```
git add test1
```
将test1添加到暂存区,也可以跳过add阶段,既跳过使用暂存区域，直接把已经跟踪的文件暂存起来一起提交。
```
git commit -am“xx”  ||   git commit -a -m“xx”
```
![创建commit](http://upload-images.jianshu.io/upload_images/2310905-9d73748018edd745.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![添加暂存区](http://upload-images.jianshu.io/upload_images/2310905-7c12d5640141f189.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![提交commit](http://upload-images.jianshu.io/upload_images/2310905-c7d826fb3d0e1ec5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

然后此时的.git变化如下

![变化后的.git](http://upload-images.jianshu.io/upload_images/2310905-f244e1f9807f4edb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![变化的.git](http://upload-images.jianshu.io/upload_images/2310905-f10d91871c881fdd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用log命令可以看到最近的log日志
```
git log
```
![git log](http://upload-images.jianshu.io/upload_images/2310905-8531ddfc8a478b97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![.git的新增内容](http://upload-images.jianshu.io/upload_images/2310905-69bfcdad0f19cf3d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![对应关系](http://upload-images.jianshu.io/upload_images/2310905-9c3f66ff7dc16407.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

从上面几幅图可以看出，提交的commit消息，最新的commit id和origin的commit id都会被保存

## 下面引入git的主要工作方式
##### 三个区域
- 工作区
- 暂存区
- git仓库
##### Three Sections

![](https://git-scm.com/book/en/v2/images/areas.png)

##### 四种状态
已跟踪(tracked)已提交（commited） 已修改（modified） 已缓存（staged）

- 在工作目录中修改某些文件
- 对修改的文件做快照，并保存到暂存区
- 提交更新，将保存在暂存区的文件快照储存到git目录中

- changed but not updated：已跟踪文件内容发生改变，并没有放入缓存区

- Changes to be committed：已存入缓存状态

- Untracked files： git  不会自动将之纳入跟踪范围
##### Four States

![](https://git-scm.com/book/en/v2/images/lifecycle.png)

#### git 原理工作图
![](https://git-scm.com/images/reset/ex3.png)
![](https://git-scm.com/images/reset/ex4.png)
![](https://git-scm.com/images/reset/ex5.png)
![](https://git-scm.com/images/reset/ex6.png)
![](https://git-scm.com/images/reset/ex7.png)

#### 暂存区index
index文件是个二进制文件，用cat命令是无法打开的

![index 一堆乱码](http://upload-images.jianshu.io/upload_images/2310905-e9b732b9de00e9c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


使用
```
hexdump -C index 
```

![index内部数据](http://upload-images.jianshu.io/upload_images/2310905-83518bb0e6ee6875.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

具体数据代表的意义可以参考[git index data format](https://github.com/git/git/blob/master/Documentation/technical/index-format.txt)


![](http://upload-images.jianshu.io/upload_images/2310905-fd73050103fdd428.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 总结


先打印log

![git log](http://upload-images.jianshu.io/upload_images/2310905-86032bc464955259.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过命令
```
git cat-file -p <commit id>
```

![git cat-file](http://upload-images.jianshu.io/upload_images/2310905-4539b9a158c0d523.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



![](https://cbx33.github.io/gitt/images/chaps/f-af2-d1.png)
![](https://git-scm.com/book/en/v2/images/commit-and-tree.png)

##### 通过以上数据可以发现git所有功能都基于三棵树。
- 第一棵树：所有提交的commit组成一棵树，分别指向不同版本的提交
- 第二棵树：每个commit代表一棵树，里面包含所有指向子树的commit（tree），指向上一次的commit id（parent），每个tree里面有包含下一级的tree，blob文件的快照。
- 第三课树：index暂存区

**综上所述，git的实现都是通过比较遮三棵树而进行工作的。**

[![git-fire](https://camo.githubusercontent.com/3ab8156bb4d519275f021d79a92a04674dc56594/68747470733a2f2f692e696d6775722e636f6d2f33504f747665432e6a7067)](https://github.com/qw3rtman/git-fire)


## References
1. [Git 官方文档](https://git-scm.com/doc)
2. Git man page
2. [A Little Of Git's Internals](https://cbx33.github.io/gitt/afterhours2-1.html)
1. [sed编辑二进制文件](https://www.zhihu.com/question/19703679)
2. [git index data format](https://github.com/git/git/blob/master/Documentation/technical/index-format.txt)
