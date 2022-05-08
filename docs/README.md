# Headline

> An awesome project.

fdfdf

在创建站点之前，必须在 GitHub 上为站点提供一个存储库。

参考:

[Mac部署Hexo详细教程_一颗西蓝花的博客-CSDN博客_hexo mac](https://blog.csdn.net/weixin_41160054/article/details/89531921)

## 1.Github仓库建站

新建一个库，库名和github名字保持一致：
即如果我的账号为sunnyzhubuxin，那么我的库名就是sunnyzhubuxin.github.io

## 2.配置SSH keys

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
