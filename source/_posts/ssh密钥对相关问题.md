---
title: ssh密钥对相关问题
date: 2024-01-18 09:45:04
tags: [ssh, keygen, timed out]
lang: zh-CN
cover:
---

可以在GitHub中添加多个公钥。这在你需要在多个设备（例如，你的个人电脑和工作电脑）上访问你的GitHub帐户时非常有用。每个设备都可以生成自己的一对SSH密钥，并将各自的公钥添加到Github账户的SSH keys设定中。这样，无论你使用哪台电脑，都可以安全地通过SSH访问你的GitHub帐户。

在GitHub的设置中，你可以看到“SSH and GPG keys"选项，在那里可以管理你的公钥。点击"New SSH key"按钮，你就可以添加新的公钥了。注意，每个公钥在GitHub上都应该是唯一的，这意味着你不能在多个帐户中使用同一个公钥。

在 "https://github.com/settings/keys" 这个页面中，应该会显示你的账户中的所有公钥，如果你添加了两个公钥，那么这两个公钥都应该出现在这个页面上。我在本地确实生成了多个密钥对，但这里只显示1个，一旦你要添加另2个公钥，这里又会显示 already in use。这是因为另2个公钥都保存到了个别 repo 的 Deploy keys 中，作为 repo 专用。

生成新的SSH密钥对来使用在你的新repository上是一个不错的选择。

1. 打开你的终端。
2. 输入 `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`。记住替换 "your_email@example.com"
3. 当系统提示你 "Enter a file in which to save the key"，你可以直接按回车。这将接受默认文件位置。既然我们要新增，就要改一下这个路径下的文件名，一般在最后面加个日期或单词标记即可。然后会在同一.ssh文件夹下新增你指定名称的密钥对。
4. 在下一步，系统会要求你输入一个密码。你可以选择输入也可以选择直接回车跳过。

完成以上步骤后，你就会得到新的SSH密钥对。然后你可以去到GitHub对应的repository里的Setting选项中的 "Deploy keys" 部分，点击右上角的 "Add deploy key"，把你新生成的公钥（默认位置为 ~/.ssh/id_rsa.pub）复制粘贴到Key输入框内，然后点击 "Add key"。

这样一来，你的新repository就可以利用新的SSH密钥对进行操作了。

**github ping不通**

这个现象可能是正常的，因为并非所有的服务器都会响应 ping 请求。许多服务器，包括一些网站，由于各种原因（如安全策略）选择屏蔽或忽略这类请求。

尤其是，GitHub 似乎默认就不响应所有的 ICMP（包括 ping） 请求。因此，当你尝试对其进行 ping 操作时，会收到一个超时错误，即使该网站完全可以访问。

访问网页使用的是 HTTP 或 HTTPS（基于 TCP 协议），这与用于 ping 命令的 ICMP 协议不同。这就是你可以正常访问 GitHub 网页，但不能 ping 到的原因。

如果你能够正常访问并使用 GitHub，那就没有必要担心 ping 的超时。这并不表明有任何问题。然而，如果你在使用 GitHub 时遇到了问题，那么可能需要进一步的故障排查。如果你需要帮助，随时告诉我！

---

**ssh: connect to host github.com port 22: Connection timed out**

> 昨天在使用[VsCode](https://so.csdn.net/so/search?q=VsCode&spm=1001.2101.3001.7020)向GitHub上传代码时，出现错误：（此前已经使用SSH的方式连接了GitHub仓库）



```bash
ssh: connect to host github.com port 22: Connection timed out
Please make sure you have the correct access rights
and the repository exists.
```

> 首先输入以下命令检查[SSH](https://so.csdn.net/so/search?q=SSH&spm=1001.2101.3001.7020)是否能够连接成功（ssh后面有空格）



```bash
ssh -T git@github.com
```

- 发现报错：



```bash
ssh: connect to host github.com port 22: Connection timed out
```

- 端口连接超时。

## 查阅资料后，找到解决办法:

> 解决方案（亲测有效）
> 在C盘——用户——你的主机名文件夹中找到.ssh文件夹；（此前配置SSH时会生成该文件夹）
> 在.ssh文件夹中新建文件 config,不带后缀（可以新建文本文档，去掉.txt后缀）
> 使用notepad++（或其他方式）打开config文件，输入以下内容，保存后即可

```bash
Host github.com
User YourEmail（你的邮箱）
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443
```

- 再次执行

```bash
ssh -T git@github.com
```

- 会出现以下提示，输入yes回车即可

```bash
The authenticity of host '[ssh.github.com]:443 ([192.30.255.123]:443)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[ssh.github.com]:443,[192.30.255.123]:443' (RSA) to the list of known hosts.
```

- 再次执行`ssh -T git@github.com`，发现验证通过

```bash
Hi Clare! You've successfully authenticated, but GitHub does not provide shell access.
```

- 完成以上步骤后，再次上传代码到[GitHub](https://so.csdn.net/so/search?q=GitHub&spm=1001.2101.3001.7020)就不会报错了
- 需要注意的是，**假如你的电脑上拥有多个github账户**，你可能事先修改过ssh的配置文件，你可能会将配置文件修改成这样子。

```crmsh
# For the account1
Host github_account1
HostName ssh.github.com
PreferredAuthentications publickey
Port 443
User git
IdentityFile ~/.ssh/id_rsa_account1

# For the account2
Host github_account2
HostName ssh.github.com
PreferredAuthentications publickey
Port 443
User git
IdentityFile ~/.ssh/id_rsa_account2
```

- 相比于普通只配置一个账户的用户，多账户用户在设置远程仓库连接时，往往设置成这个样子

```elixir
[remote "origin"]
    url = git@github_account1:account1/my_repo.git
```

你将通过配置文件中设置的`Host`别名`github_account1`代替`github.com`访问github，这意味着，如果你想要进行进行git clone操作，也应该通过别名访问，否则无法走443端口。假如你想clone `git@github.com:torvalds/linux.git`，你应该修改为`git@你设置的别名:torvalds/linux.git`。或者是，额外在配置文件里加上。

```crmsh
# Just for clone
Host github.com
HostName ssh.github.com
Port 443
User git
```



chatGPT问答

你在 GitHub 的两个不同仓库中使用了两个公钥，并且在 GitHub 用户设置中还有一个公钥。为了让所有的 SSH 交互都能正确进行，你需要在 `~/.ssh/config` 文件中为每个公钥配置一个对应的 Host 设置。

这里我提供一个基本的示例供你参考：

```bash
# 对应于 GitHub 用户设置中的公钥
Host github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github main

# 对应于第一个仓库的公钥
Host github.com-repo1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_repo1

# 对应于第二个仓库的公钥
Host github.com-repo2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_repo2
```

注意：`~/.ssh/id_rsa_github main`,`~/.ssh/id_rsa_repo1`,`~/.ssh/id_rsa_repo2`需要替换为你的私钥（即对应公钥的私钥）的实际路径。

然后你就可以使用 `git@github.com-repo1:` 或 `git@github.com-repo2:` 代替 `git@github.com:` 来操作你的仓库，这样 git 就会使用正确的私钥。一般来说，当你 clone 你的仓库的时候，也要使用新的地址。

另外，如果你的私钥设置了密码，你可能需要使用 ssh-agent 和 ssh-add 命令，这样在以后进行操作的时候就无需再输入密码。

> *git@github.com-repo1中间必须是 - 符号？*

在 SSH Config 文件中，Host 后面所定义的名字是你自己选择的标识符，可以是任何你喜欢的字符串，没有硬性要求一定用 "-"。

我在这个例子中使用 "-" 是为了清楚地表达这个是针对的 GitHub 的仓库，并且让其看起来像一个 FQDN (Fully Qualified Domain Name)，但实际上你可以根据你的需求自定义。

不过需要注意的是，这个 Host 的名字会被用在 Git 命令中，替换 "[github.com](https://github.com/)"。如：`git clone git@your_host:user/repo.git` 所以请确保这个名字在命令行中可用，最好避免使用可能引起混淆的字符。

> 哦？可以替换掉github.com？

是的，当你在SSH Config 文件中为一个 Host 定义了一个别名（比如 `github.com-repo1`），那么在 Git 命令中，你就可以使用这个别名来代替实际的 Hostname （`github.com`）。Git 会通过 SSH 去查看你的 SSH Config 文件，找到对应的别名，并使用对应的私钥进行认证。

例如，如果你的 SSH Config 文件中写了如下配置：

```bash
Host github.com-repo1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_repo1
```

那么，当你使用如下命令时：

```bash
git clone git@github.com-repo1:username/repo.git
```

Git 会查看你的 SSH Config 文件，发现 `github.com-repo1` 对应的实际 Hostname 是 `github.com`，并且知道应当使用 `~/.ssh/id_rsa_repo1` 这个私钥进行认证。

所以，把 `github.com-repo1` 看成是 `github.com` 的别名即可，你可以自由地定义别名，只要在 SSH Config 文件中与相应的 Hostname 和私钥匹配即可。
