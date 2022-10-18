
电脑上已经配置了一个公司的 github 账号，但是现在想把笔记都转到 `Obsidian` 上，而 `Obsidian` 可以关联 github 账号，自动备份笔记到 `github` 上，当然是备份到自己的 `github` 上，这个时候就需要在电脑上配置第二个 `github` 账号。

  

### 1. 生成密钥

  

在 `.ssh` 目录下，已经有了密钥  `id_rsa` ，这个是配置第一个账号时生成的，现在为第二个 `github` 账号生成密钥， 并且命名为 `id_oneredka`

  

```bash

ssh-keygen -t rsa -f ~/.ssh/id_oneredka -C "gg.hiloxx@gmail.com"

```

  

### 2. 将生成的公钥配置到自己的 `github` 账号

  

### 3. 关于**全局用户名和密码**

  

因为现在时多账户，如果有全局账号设置， 验证的时候总是去验证第一个，我们也可以每一次都在命令行执行新的 `agent` ，再指定私钥，这当然不是我们想要的，太麻烦。所以根据实际情况，我并没有删掉全局账号，因为第一个是公司账号，这个用的比较多，所以就没有取消全局设置，为自己的账号下的仓库单独设置用户就可以了。

  

```bash

# 设置全局用户名

git config --golbal user.name "XXX"

# 设置全局邮箱

git config --golbal user.email "xxx@aa.com"

# 查看全局用户名

git config --global user.name

# 查看全局邮箱

git config --global user.email

# 查看全局密码

git config --global user.password

移除全局配置的用户信息

# 移除全局配置账户

git config --global --unset user.name

# 移除全局配置邮箱

git config --global --unset user.email

# 移除全局密码

git config --global --unset user.passwor

```

  

### 4. 配置 config 文件

  

在 `.ssh` 目录下新建 `config` 文件， `config` 时全名，无后缀，内容如下

  

```bash

# one                                                                      

Host github.com

HostName github.com

User louis.yi

IdentityFile ~/.ssh/id_rsa

# second                                                                          

Host personal

HostName github.com

User oneredka

IdentityFile ~/.ssh/id_oneredka

```

  

多账号下我们使用 `ssh` 的方式 `clone` 代码，这个时候 `git` 就会根据 `config` 中的配置识别我们的账号，所以上面的文件内容就很重要。

  

**Host**  这个是账号别名，当 `HostName` 相同时，就需要通过它来识别账号。举个栗子，现在我个人  `github` 账号的仓库 `ssh` 克隆地址为 ： [`git@github.com](mailto:git@github.com):oneredka/obs.git` ，那么我在 `clone` 代码时，无多账号时，应运行的命令是 `git clone [git@github.com](mailto:git@github.com):oneredka/obs.git` , 多账号时，就要替换为 `git clone git@personal:oneeredka/obs.git` 。所以你可以发现到底替换了什么。

对于公司账号，因为用的比较频繁，所以 `Host` 被我 设置得跟 `HostName` 一样，这样克隆公司代码的时候就不用更改 `ssh` 的地址了。

  

**HostName** 代码托管平台地址， 取决于你是什么账号。

  

**IdentityFile** 私钥位置

  

### 为仓库配置用户

  

因为公司账号用得比较频繁，所以我就没有取消全局账号设置，所以需要为自己的个人账号仓库配置账号

  

```bash

git config  user.name "XXX"

git config  user.email "XXX"

```

  

配置完成之后，就可以正常提交代码了。

  

实际上到这里，多账号就配置完成了，可以正常使用了。

  

### 关于 **ssh-agent**

  

之前在整理的时候，有时候并没识别到私钥，我猜测是 `config` 文件没有写对，也没有理解对。 我们可以开启 **`ssh-agent` ,** 然后指定私钥，然后才可以提交代码。

  

将私钥`id_rsa_github`添加到ssh代理中

  

```

# ssh-add ~/.ssh/key_name

  

ssh-add ~/.ssh/id_oneredka

```

  

**每次必须添加ssh-add**

  

### 1. 原因

  

ssh-add 这个命令不是用来永久性的记住你所使用的私钥的。、实际上，它的作用只是把你指定的私钥添加到 ssh-agent 所管理的一个 session 当中。而 ssh-agent 是一个用于存储私钥的临时性的 session 服务，也就是说当你重启之后，ssh-agent 服务也就重置了。

  

### 2. 解决方法

  

在 git 的安装目录下的`bash.bashrc`文件，末尾添加

  

```

#ssh-add 改为你电脑的秘钥名称

eval "$(ssh-agent -s)"

ssh-add ~/.ssh/id_rsa_github

ssh-add ~/.ssh/id_rsa_gitLab

```

  

这样，每次打开都会自动执行

  

```

Agent pid 12280

Identity added: /c/Users/hong/.ssh/id_rsa (/c/Users/Thinkpad/.ssh/id_rsa)

Identity added: /c/Users/hong/.ssh/id_rsa_gitLab (/c/Users/Thinkpad/.ssh/id_oneredka)

```

  

我注释掉了 `bash.bashrc` 文件的更改，因为不需要执行 `ssh-agent` 也是 ok 的。