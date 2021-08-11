第一步： 切换到你的项目文件下

第二步： 通过使用 `git init` 把这个文件夹变成Git可管理的仓库

这个时候会看到项目下多了一个.git文件夹 （因为他是默认隐藏文件，所以你可能需要设置一个让隐藏文件可见）

第三步： 可以使用 `git status` 来看一下当前的状态 然后通过 `git add .` (把所有的文件添加到仓库)，之后再使用 `git status` 查看一下

第四步： 用 `git commit` 把项目提交到仓库，记得写上注释如 git commit -m "first commit"

第五步： 创建SSH KEY。可以看一下home下有没有.ssh目录，检查一下里面是否包含id_rsa和id_rsa.pub这两个文件，有就跳下一步，没有就按下面命令创建

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

 一路回车，就可得到上面所说的两个文件。

第六步： 登录Github，右上角点击头像，再点击Settings，然后在找到 SSH and GPG keys

![image-20210713170404795](/home/q123/.config/Typora/typora-user-images/image-20210713170404795.png)

![image-20210713170427366](/home/q123/.config/Typora/typora-user-images/image-20210713170427366.png)

第七步： 在Github上创建一个Git仓库

点击右上角的+号 new repository来创建

![image-20210713170912308](/home/q123/.config/Typora/typora-user-images/image-20210713170912308.png)



第八步： 把Github上的仓库和本地的进行关联

在本地仓库的命令行输入：

```
git remote add origin https://github.com/william-1121/unname.git
```

![image-20210713171421215](/home/q123/.config/Typora/typora-user-images/image-20210713171421215.png)

origin后面的是你在Github上创建好的仓库的地址。

第九步： 关联完成，就可把本地仓库的所有内容推送到远程仓库（Github）上

```
$ git push -u origin master
```

因为远程仓库刚开始是空的，所以加了参数 -u ，后面就不用加了

上传完成应该是这样的：

![image-20210713172014728](/home/q123/.config/Typora/typora-user-images/image-20210713172014728.png)



总结：

+ `git init`

+ `git add .`

+ `git commit  -m  " "`

+ `git remote add origin XXXXXXXXXX`

+ `git push origin master`

  

