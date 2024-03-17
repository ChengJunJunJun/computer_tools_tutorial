# 关于远程服务器连接的ssh

## 什么是ssh

SSH（Secure Shell）实际上在建立一种安全的网络连接，允许你在两个计算机之间进行加密的通信和数据传输。SSH的原理涉及加密、身份验证和安全传输。

你自己需要知道的就是，ssh可以用来连接服务器！

## .ssh文件夹下面的文件

1. **authorized_keys:**
   
   - **位置：** `~/.ssh/authorized_keys`（在用户的家目录下的.ssh文件夹中）
   - **作用：** 这个文件包含了允许访问该用户账户的公钥列表。当你通过SSH连接到服务器时，系统会检查你的私钥是否与`authorized_keys`文件中的某个公钥匹配。如果匹配成功，你将被允许登录。
   
   tips：如果你要连接一个服务器，就要确保这个服务器的authorized_keys文件有你的公钥！
   
2. **id_rsa:**
   - **位置：** `~/.ssh/id_rsa`
   - **作用：** 这是SSH密钥对中的私钥文件。SSH使用公钥加密的方式，而私钥用于解密。当你连接到远程服务器时，私钥会与服务器上的公钥进行匹配，以验证你的身份。

3. **id_rsa.pub:**
   - **位置：** `~/.ssh/id_rsa.pub`
   - **作用：** 这是SSH密钥对中的公钥文件。当你连接到远程服务器时，这个公钥会添加到服务器上的`authorized_keys`文件中。这样，服务器可以使用你的公钥对数据进行加密，而只有拥有相应私钥的用户才能解密。

4. **known_hosts:**
   - **位置：** `~/.ssh/known_hosts`
   - **作用：** 这个文件包含了你连接过的远程主机的公钥信息。当你第一次连接到一个远程主机时，其公钥会被保存到这个文件中。下次连接时，系统会检查该主机的公钥是否与`known_hosts`中存储的一致。这有助于防止中间人攻击。

这些文件一起协作，提供了安全的远程访问方式。私钥和公钥的配对使得数据能够安全地在客户端和服务器之间传输，而`authorized_keys`和`known_hosts`文件则用于管理信任关系和防范潜在的安全风险。

## 如何用ssh连接远程服务器？

### 自己的终端建立ssh

1. **检查是否已有SSH密钥：**
   
   首先，检查你的计算机上是否已经存在SSH密钥。默认情况下，SSH密钥对的私钥和公钥存储在用户的家目录下的 `~/.ssh/` 文件夹中。

   ```bash
   ls ~/.ssh
   ```

   如果已经存在密钥对（通常是 `id_rsa` 和 `id_rsa.pub`），你可以选择备份或删除它们。

2. **生成新的SSH密钥：**

   使用以下命令生成新的SSH密钥对。在这个过程中，你可以选择性地添加密码来保护私钥。

   ```bash
   ssh-keygen -t rsa -b 4096 -C "cj-miracle@outlook.com"
   ```

   - `-t rsa`: 指定密钥的类型为RSA。
   - `-b 4096`: 指定密钥的位数，4096位是一种较安全的选择。
   - `-C "your_email@example.com"`: 添加一个注释，通常是你的电子邮件地址。

   按照提示，选择密钥保存的位置（默认为 `~/.ssh/id_rsa`），以及是否设置密码。

3. **添加SSH密钥到SSH代理（可选）：**

   如果你使用SSH代理，你可能需要将新生成的密钥添加到代理中。使用以下命令：

   ```bash
   ssh-add ~/.ssh/id_rsa
   ```

4. **将公钥添加到远程服务器：**(一般执行此步骤，就不需要输入服务器用户密码了)

   将新生成的公钥（通常是 `~/.ssh/id_rsa.pub`）的内容复制到你希望连接的远程服务器上。你可以使用 `ssh-copy-id` 命令，或者手动将公钥内容添加到远程服务器的 `~/.ssh/authorized_keys` 文件中。

   ```bash
   ssh-copy-id username@remote_server_ip
   ssh-copy-id -p 29050 chengjun@i38944o710.goho.co 
   ssh-copy-id -p 49919 cj@i38944o710.goho.co （或者）
   ```
   
   或者手动：
   
   ```bash
   cat ~/.ssh/id_rsa.pub | ssh username@remote_server_ip 'cat >> ~/.ssh/authorized_keys'
   ```
   
   替换 `username` 和 `remote_server_ip` 为远程服务器上的用户名和IP地址。

现在，你应该拥有一个新生成的SSH密钥对，并且可以使用它们进行连接。确保你在重新生成密钥后更新任何需要使用SSH密钥的地方，例如GitHub、Bitbucket等。

### 连接服务器ssh

就是下面的命令：

```
ssh -p 49919 cj@i38944o710.goho.co 123456
ssh -p 29050 cj@i38944o710.goho.co 12345678
ssh -p 49919 chengjun@i38944o710.goho.co 123456
ssh -p 29050 chengjun@i38944o710.goho.co 123456

ssh -p 29050 chengjun@192.168.3.37 123456

ssh-copy-id -p 49919 chengjun@i38944o710.goho.co

ssh-copy-id -p 29050 chengjun@i38944o710.goho.co
```

**手动添加服务器的公钥：** 如果你确信服务器的指纹是正确的，你可以手动将服务器的公钥添加到你的 `known_hosts` 文件中。运行以下命令：（此步骤如果有报错，可选，不过还是要明白ssh的原理）

```bash
ssh-keyscan -p 49919 i38944o710.goho.co >> ~/.ssh/known_hosts
```

## 出现的常见error 及解决办法

问题1:远程主机关闭连接

```bash
kex_exchange_identification: Connection closed by remote host
Connection closed by 198.18.0.19 port 49919

sudo useradd chengjun
```

出现上述问题，一般需要解决一下问题：

1. **检查网络连接：** 确保你的网络连接正常，而且没有任何中断。如果是在局域网内，也要确保局域网设置正确。
2. **检查权限：** 确保你有足够的权限连接到远程主机。检查你使用的用户账户是否具有足够的权限进行连接。
3. **检查远程主机设置：** 查看远程主机的设置，确保它允许连接，并且没有特殊的配置导致连接被关闭。
4. **防火墙设置：** 如果你使用防火墙，确保防火墙允许连接。有时候防火墙设置会导致连接被拒绝。

提醒：部分学校校园网不支持外网域名的连接，你可以自己开一个热点或者使用VPN代理进行连接，二号基地的服务器不能用校园网连接！

我已修改3090服务器上root和hust用户的密码，新密码为Amax1979!!!，现在已经可以用校园网络连接了

```
scp crnn.pytorch.zip chengjun@i38944o710.goho.co:/home/chengjun
hust    ALL=(ALL)       ALL

```

