# Hexo

## 01.Github仓库建站

参考:

[Mac部署Hexo详细教程](https://blog.csdn.net/weixin_41160054/article/details/89531921)

新建一个库，库名和github名字保持一致：
即如果我的账号为sunnyzhubuxin，那么我的库名就是sunnyzhubuxin.github.io

## 02.配置SSH-keys

接着需要SSH keys。打开mac终端，输入命令

```python
$ cd ~/.ssh #检查本机的ssh秘钥
```

如果提示 `No such file or directory`说明你是第一次使用 `git`。需要生成新的SSH keys:

```
$ ssh-keygen -t rsa -C "你的邮箱地址"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):<回车>
Enter passphrase (empty for no passphrase):<输入加密串><如不想设置密码可直接回车表示为空>
Enter same passphrase again:<再次输入加密串><接着回车确认>
Your identification has been saved in /Users/你的名字/.ssh/id_rsa).
Your public key has been saved in /Users/你的名字/.ssh/id_rsa.pub.
The key fingerprint is:
43:c5:5b:5f:b1:f1:50:43:ad:20:a6:92:6a:1f:9a:3a "你的邮箱地址"
```

最后出现类似长方形的字符画即表示成功。

如果已经有了的话，直接去查看，文件夹的名称为.ssh

如果无法看到.ssh 文件夹，显示隐藏文件（cmd+shift+.）即可。

接下来，将SSH key添加进GitHub：

打开.ssh文件夹下的id_rsa.pub（若看不到，则需显示隐藏文件）,全选复制文件中所有内容。

然后进入github主页，点击右上角头像进入settings，选择SSH and GPG keys，再点击New SSH Key。将刚才复制的内容粘贴进key，title可以为空。最后Add SSH key。

可以通过如下命令进行测试是否成功

```
$ ssh -T git@GitHub.com 
```

接下来出现：

```
The authenticity of host 'GitHub.com (207.97.227.239)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?<输入yes>
Hi 你的用户名! You've successfully authenticated, but GitHub does not provide shell acces
```

如果出现上述提示，则说明SSH Key成功啦

接下来在浏览器中输入 【你的名字】.github.io ，如果成功出现页面，并且页面上是你刚输入的地址，那么github pages配置成功。

## 03.Nodejs安装

切记：不要去下载pkg安装包安装，会报错

第一步：安装nvm和确认是否成功

```
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

然后，输入代码

```
~$ command -v nvm
```

会出现nvm。
如果没有，关掉`terminal`，重启一下

第二步：用`nvm`安装`node`

```python
$ nvm install node
```

## 04.Hexo安装

参考：

[利用Hexo搭建自己的个人博客(Mac)](https://www.bilibili.com/video/BV1Ux411H7iX?from=search&seid=5301818938814494583&spm_id_from=333.337.0.0)

```
$ npm install -g hexo-cli
```

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```
$ hexo init blog
```

（blog为新建在本地的文件夹名，可随意起名。）

此时文件夹内已经有了基本的文件结构。

之后：

```
$ cd blog
$ npm install
```

其中列举一些文件的功能：

- _config.yml 网站的配置文件，可以在此配置大部分参数

- source 资源文件夹是存放用户资源的地方。除 posts 文件夹之外，开头命名为 (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

- themes主题文件夹，后面我们使用的next主题即会存放在此。

- _posts存储你发表在博客上的文章，当Hexo 初始化一个站点时，里面会有一篇默认的博文。

此时可执行

```
$ hexo s
```

在本地的环境就搭建好了。

## 05.设置一键部署

参考：

- 官方：[部署 | Hexo](https://hexo.io/zh-cn/docs/one-command-deployment)

完成上面的操作后，需要将本地的文件推到github上。

Hexo 提供了快速方便的一键部署功能，只需一条命令就能将网站部署到服务器上。

1.必须先在本地 `_config.yml` 中修改参数，一个正确的部署配置中至少要有 `type` 参数。

```
deploy:  
 type: git
 repo: git@github.com:sunnyzhubuxin/sunnyzhubuxin.github.io.git
 branch: master
 message: 
```

其中：

repo：库地址

2.本地修改完文件之后，安装[hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git) 这个插件

```
$ npm install hexo-deployer-git --save
```

3.登入 Github在库设置（Repository Settings）中将默认分支也设置为master。

4.生成文件并推至远程

```
$ hexo clean && hexo deploy
```

## 06.如何更换hexo主题

参考：

[给hexo安装主题](https://blog.csdn.net/weixin_41160054/article/details/89473887)

第一步：下载next主题包。
使用terminal，进入到我们Hexo的安装包下面。我的安装包，叫做blog。因此，我输入下述代码

```
$ cd blog
```

然后进入themes包

```
$ cd themes
```

接着，我们输入下面的代码

```
$ git clone https://github.com/theme-next/hexo-theme-next 
```

提示我们done，就说明，这个步骤操作完成了。

第二步：修改config.yml文件内容。
在blog文件夹中找到_config.yml，用编译器打开（vs code或者sublime）。
command + F 查找 theme将原来默认的主题landscape改为 next即可

接下来，我们先来预览一下，我们主题更换的效果

```python
$ hexo s
```

注意一下，我们目前所在的目录，还是在`themes`目录下哦。预览没有问题，我们就可以发布该主题了。

```python
$ hexo d
```

## 07.如何发布文章

参考：

[Hexo发布文章](https://blog.csdn.net/zhangyu4863/article/details/80976738)

第一步：打开文件夹新建一个md文档

```
$ cd blog
$ hexo new title
```

title就是新建的文章的名字

之后看见如下提示

```
INFO  Created: ~\Desktop\blog\source\_posts\hello.md
```

然后在cmd中即可看到新建文章的路径，按路径找到、编辑保存即可

第二步：编辑好文章后，进行本地调试，命令如下：

```
$ hexo s
```

上面命令在cmd命令行执行后，打开 http://localhost:4000/ ,找到刚才编辑的文章，查看无误后执行下一步

生成静态网页

```
$ hexo g
```

发布网站（推送到github或者gitee）

```
$ hexo d
```

也可简写为（一起执行上边两个命令）

```
$ hexo clean && hexo g -d
```

或

$ hexo d -g

## 08.在博客中如何插入图片

参考：

[在Hexo博客中插入图片](https://blog.csdn.net/weixin_34348805/article/details/91389277)

**src 链接**

如果你要插入的图片，是一个外部的 src 链接地址，比如该图片存放在 CDN 上，或某某图床上面，那就使用 Markdown 默认的插入图片的方式，方法和插入链接很像，只是前面多了一个感叹号，如下：

```bash
![alt](https://ws3.sinaimg.cn/large/005BYqpgly1g29eohl7qhj31c00u0dkz.jpg)
```

**本地绝对路径**

当 Hexo 项目中只用到少量图片时，可以将图片统一放在 *source/images* 文件夹中，通过 Markdown 语法访问它们。

```bash
![alt](/images/test.jpg)
```

**本地相对路径**

图片除了可以放在统一的 images 文件夹中，还可以放在文章自己的目录中，文章的目录可以通过配置 *_config.yml* 来生成。配置如下：

```vbnet
post_asset_folder: true
```

将 *_config.yml* 文件中的配置项 *post_asset_folder* 设为 true 后，执行命令 `$ hexo new post_name`，在 *source/_posts* 中会生成文章 *post_name.md* 和同名文件夹 *post_name* 。将图片资源放在 *post_name* 中，文章就可以使用*相对路径*引用图片资源了。

```bash
![alt](test.jpg)
```
