# SSH Certification Change
如何清除前同事的信息、加入自己的certification，然后连接到gitlab。

## 步骤 1: 删除旧的 SSH 密钥

首先，删除现有的旧 SSH 私钥和公钥文件，以防它们被意外使用：

```bash
rm ~/.ssh/id_rsa
rm ~/.ssh/id_rsa.pub
```

## 步骤 2: 生成新的 SSH 密钥对

生成一个新的 SSH 密钥对：

```bash
ssh-keygen -t rsa -b 4096 -C "user_name@email_address"
```
ssh-keygen: 这是用于生成、管理和转换认证密钥的工具。<br>
- -t rsa: 指定密钥类型为 RSA（Rivest-Shamir-Adleman），这是一种广泛使用的加密算法。<br>
- -b 4096: 指定密钥长度为 4096 位。这决定了密钥的安全强度，通常 2048 位已经足够，但 4096 位更安全。<br>
- -C "xxx@xxx.com": 这是一个注释，通常用来标识这个密钥对的用途或所有者的电子邮件地址。这个注释会包含在生成的公钥文件中。

## 步骤 3: 查看新生成的公钥内容

查看新生成的公钥内容：

```bash
cat ~/.ssh/id_rsa.pub
```

## 步骤 4: 将新的公钥添加到 GitLab

登录到 GitLab。<br>
进入个人设置（Settings） -> SSH Keys。<br>
将新生成的公钥内容复制到输入框中，并添加一个标题来描述这个密钥（例如，“New Workstation Key”）。<br>
点击 Add key 按钮保存。

## 步骤 5: 确保正确配置 SSH

确保 SSH 配置文件 ~/.ssh/config 指向新的私钥：

```bash
vim ~/.ssh/config
```
在 vim 中按 i 键进入插入模式，添加或更新如下内容（如果文件不存在，可以新建）：
```bash
Host xxx
    HostName xxx
    User git
    IdentityFile ~/.ssh/id_rsa
```
'xxx'是your.gitlab.server，是git@后面的主机名，按 Esc 键退出插入模式，然后输入 :wq 保存并退出 vim。

### 解释配置文件的作用

#### SSH 配置文件 `~/.ssh/config`

这个配置文件用于告诉 SSH 客户端在连接特定主机时，使用哪个私钥进行身份验证。以下是每一行的作用：

- `Host your.gitlab.server`：指明这段配置适用于连接 `your.gitlab.server` 主机。
- `HostName your.gitlab.server`：指定实际连接的主机名。
- `User git`：指定连接时使用的用户名，在连接 GitLab 时通常是 `git`。
- `IdentityFile ~/.ssh/id_rsa`：指定用于连接的私钥文件路径。

请将 `your.gitlab.server` 替换为你实际使用的 GitLab 服务器地址。通过正确配置这个文件，可以确保 SSH 客户端使用正确的私钥进行身份验证。

## 步骤 6: 清除 SSH 代理中的所有密钥

清除 SSH 代理中所有已加载的密钥，然后添加新的私钥：

```bash
ssh-add -D
ssh-add ~/.ssh/id_rsa
```

## 步骤 7: 测试新的 SSH 连接

测试新的 SSH 连接，确保连接的账户是你的账户：

```bash
ssh -T git@your.gitlab.server
```

你应该看到类似以下的消息：

```bash
Welcome to GitLab, @xxx!
```

确认该信息是否和自己的identity符合（比如，工号一致）

## 步骤 8: 尝试克隆仓库

如果确认使用正确的私钥，尝试再次克隆仓库：

```bash
复制代码
git clone git@your.gitlab.server:xxx.git
```
